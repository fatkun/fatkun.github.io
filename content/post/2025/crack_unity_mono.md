---
title: "破解Unity游戏联网验证(Mono)"
date: 2025-11-02T10:55:33+08:00
tags: [逆向]
categories: [逆向]
author: "fatkun"
draft: false
typora-root-url: ./..\..\..\static
---

# 背景
一个windows unity游戏，代码没有加密，没有热加载，使用UnityPlayer.dll。名字是：哎呦,xxxxx。
这个没逆向成功，只是提供一些思路。

# 目标
游戏启动后，界面停留在连接中，该游戏有联网验证。那这部分的代码是哪个类呢？我们需要找出对应的代码。

# 尝试
首先从网络请求入手，猜测它会有网络请求，所以使用了Reqable这类http/https抓包工具，但是没有任何请求。
又尝试使用Proxifier拦截请求，但是还是没能抓取到http/https请求，但是在关闭游戏的时候，看到请求了某个域名。（后面查看代码知道实际上是TCP请求，但这个时候我不是太懂，如果知道域名后，应该可以使用tcp的抓包工具筛选请求）

由于这个游戏没有用IL2CPP，直接用dnspy反编译***Data/Managed目录的dll文件就可以看到完整的代码。

从网络这边无法入手，继续尝试能不能通过frida来hook代码，发现之前主要是hook il2cpp 的代码，mono的反而不知道怎么操作。咨询AI说使用frida-mono-api，但实际使用下来比较老旧了，几年前的代码，最终这条路还是走不通。

那还有种办法通过Debug.Log写日志，日志路径在`C:\Users\用户名\AppData\LocalLow\公司名\游戏名\Player.log`。但是呢，一般Release版本是不会输出debug日志的。所以我跟了一下Debug.Log的代码看哪里可以修改可以输出。然而呢，我看了一下日志居然是输出的，那就可以插入日志来跟踪代码。

前面浏览代码发现一个可疑的类，SteamManger。其中有一段代码涉及到SetCallback方法，我想用dnspy的分析功能，但找不到调用方。（这里是dnspy的局限，如果代码使用实例的方式调用，就找不到谁调用它，而且搜索字符串也不好用，不能全局搜索代码，只能在一个类内搜索。后面可能要先导出所有代码，然后在vscode搜索。）
当时想看谁调用了SetCallback，我需要打印一下堆栈。

使用dnspy右键编辑方法，增加以下代码，点击编译（如果编译失败，请尝试把目录下的所有dll文件都拖入dnspy），然后在文件-》保存模块。
```
		string stack = Environment.StackTrace;
		Debug.Log("SetCallback" + stack);
```

查看日志，这时就可以找对应代码了。
```
SetCallback  at System.Environment.get_StackTrace () [0x00000] in <0de99929796b4095b47389e59e446fbd>:0 
  at PlatformSteam.SetCallback (EventCallbackDelegate callback) [0x00000] in <749c0f0f9b7e45cbb9255a71a40a8e11>:0 
  at PlatformManager.SetCallback (EventCallbackDelegate callback) [0x00000] in <749c0f0f9b7e45cbb9255a71a40a8e11>:0 
  at MainGame.StartPlatform (PlatformType platformType) [0x00000] in <749c0f0f9b7e45cbb9255a71a40a8e11>:0 
  at Loading.Init () [0x00000] in <749c0f0f9b7e45cbb9255a71a40a8e11>:0 
  at Loading.Start () [0x00000] in <749c0f0f9b7e45cbb9255a71a40a8e11>:0 EventCallbackDelegate
```

跟踪代码，最后发现有一个NetWork类。前面其实发现了一个域名，其实也可以尝试根据字符串查询，域名可能是在代码里面或者读取外部配置。在dnspy搜索字符串时，记得在搜索程序集，选择字符串（默认是以上所有，搜不到字符串）。

到这里可以看到这是一个TCP的连接，使用TCP倒是很少见，一般都用HTTPS。
```
this.m_Socket = new Socket(SocketType.Stream, ProtocolType.Tcp);
this.m_Socket.Connect(this.ServerAddress, 7788);
```

对这种TCP二进制通信还是比较烦，粗略看了代码，没有加密内容，理论上抓包分析二进制可以写个程序解包。
看了一下游戏对视频做了加密，而且key是通过上面的网络请求获取的，不过这里没加密，如果有正版游戏，应该能提取出来，并且日志也会输出。

```c#
	public void OnRecvVideoKey(string name, VideoKey key)
	{
		Debug.Log("------------->OnRecvVideoKey:" + name);
		Dictionary<string, VideoKey> videoKeys = this.m_VideoKeys;
    }
```
看起来这个游戏反逆向做的还好，每个视频的key可能不一样，都需要通过服务器获取。看到这里，不继续进行下去了，已经基本分析清楚，如果要完全破解，就要有正版账号，分析TCP请求，完成模拟发送和接收。

# 总结
总结一下优势劣势

优势
- 这个游戏使用TCP请求来代替https请求，提高了一点难度，当前https很容易使用本地ca证书分析密文，除非在代码中做证书校验。但是就算做了证书校验，实际上也是可以分析去掉的。
- 从服务端获取key等

缺点
- 没有使用IL2CPP，导致代码完全暴露。如果使用IL2CPP就要使用汇编方式分析了，难度更大一些。不过也可以用frida来分析代码
- TCP明文通信？不过暴露代码了，是否明文也不重要，而且也是二进制的

