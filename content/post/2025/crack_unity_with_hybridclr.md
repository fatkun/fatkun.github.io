---
title: "逆向使用HybridCLR热更新的Unity游戏"
date: 2025-09-27T10:55:33+08:00
tags: [逆向]
categories: [逆向]
author: "fatkun"
draft: false
typora-root-url: ./..\..\..\static
---

# 声明
仅用于学习记录，请勿用于非法用途。

# 分析
这个游戏使用了il2cpp，首先想到的是用Il2CppDumper反编译，找到GameAssembly.dll和global-metadata.dat。
```bash
mkdir -p out
Il2CppDumper GameAssembly.dll global-metadata.dat out
```
还好这两个文件都没有加密，但发现在DummyDll没找到核心的代码，但找到HybridCLR.Runtime.dll，这个应该是用了热加载功能。

尝试使用 `frida-il2cpp-bridge` trace 代码, 同时也可以dump代码出来
```ts
Il2Cpp.perform(() => {
    console.log(Il2Cpp.unityVersion);
    Il2Cpp.dump("dump.cs", "./");
}
```
从dump.cs看出，多出了一个Game.dll，看了一下方法确实是核心代码。尝试对Game里面的代码进行trace，但是发现不是所有的方法都可以trace到。
```ts
Il2Cpp.perform(() => {
    console.log(Il2Cpp.unityVersion);
    Il2Cpp.trace(false).classes(Il2Cpp.domain.assembly("Game").image.class("Tower.NetworkManager")).and().attach();
}
```
从dump.cs看到，有些方法的地址是一样的，应该是由于动态加载的问题，找到的地址是错误的，这样就导致无法通过trace。

回到前面看到的HybridCLR.Runtime.dll，用dnSpy查看方法
```c#
    public static extern LoadImageErrorCode LoadMetadataForAOTAssembly(byte[] dllBytes, HomologousImageMode mode);
```
可以看到这个方法是传入了一个dllBytes参数，我们要找到这个bytes是如何传入进来的。
这里我们要用到ida pro，加载GameAssembly.dll，并且使用script和Il2CppDumper反编译的内容把方法名称补充进来（可以看之前的文档操作）
找到LoadMetadataForAOTAssembly这个方法，然后在方法名上面按X，查找引用，F5分析伪代码

```C
    s_assetDatas = (System_Collections_Generic_Dictionary_object__object__o *)DllManager_TypeInfo->static_fields->s_assetDatas;
    if ( !s_assetDatas )
      sub_180332070(0, v3);
    Item = (System_Byte_array *)System_Collections_Generic_Dictionary_object__object___get_Item(
                                  s_assetDatas,
                                  key,
                                  Method_System_Collections_Generic_Dictionary_string__byte____get_Item__);
    MetadataForAOTAssembly = HybridCLR_RuntimeApi__LoadMetadataForAOTAssembly(Item, 1, 0);
```

可以看到是从s_assetDatas这个List里面获取的，继续跟踪这个s_assetDatas如何获取。另外看到这个类DllManager不是动态加载的，这时候我们可以使用frida来trace代码。
```ts
Il2Cpp.perform(() => {
    const ScriptMain = Il2Cpp.domain.assembly("ScriptMain").image;
    Il2Cpp.trace(false).classes(ScriptMain.class("DllManager")).and().attach();
    // Il2Cpp.trace(true).methods(ScriptMain.class("DllManager").method("GetWebRequestPath")).and().attach();
})
```
trace有个参数可以指定为true，打印参数，但是经常出错，目前不知道怎么解决，可以针对局部方法开启。
从上面的trace看，dll文件是从.ab文件读取出来的，找到对应的ab文件，使用AssetStudioModGUI解包获取DLL文件，把文件丢到dnSpy里，发现代码完全没有混淆和加密。