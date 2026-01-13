---
title: "某云盘脱壳"
date: 2026-01-12T10:22:01+08:00
tags: [android, 逆向]
categories: [逆向]
author: "fatkun"
draft: false
typora-root-url: ./..\..\..\static
---
这个云盘使用梆*加固企业版，记录一下如何脱壳。

这个加固会检测frida，暂时不知道怎么绕过frida检测，也不知道怎么把dex dump出来。找到一个网站 [APK加固安全测试](https://56.al/upload.php) ，上传APK，等待一段时间后，它就帮你把dex dump出来了。

有了dex文件之后，怎么脱壳呢？可以看[这个视频](https://www.bilibili.com/video/BV13EjdziE6c/) 。

首先要还原AndroidManifest.xml文件，首先是这两个需要修改
```xml
<application
    android:name="com.secneo.apkwrapper.AW"
    android:appComponentFactory="com.secneo.apkwrapper.AP"
>
```

那改成什么值呢？找到 com.secneo.apkwrapper.H 这个类查看
```java
public static String APPNAME = "com.*******.client.CCloudApplication"; // 对应 android:name
public static String ACFNAME = "androidx.core.app.CoreComponentFactory"; // 对应 android:appComponentFactory
```

然后拉到最后，去掉这个provider
```xml
<provider
    android:name="com.secneo.apkwrapper.CP"
    android:exported="false"
    android:authorities="com.*****.CP"
    android:initOrder="2147483647"/>
```
如果在windows上修改，可以用APK.Tool.GUI解包后直接修改文件再打包。

然后是要把dex塞回apk里面。塞回之前，需要先用MT管理器修复dex文件。另外apk里面已经有了一个classes.dex，如果直接覆盖，启动时会退出，使用android studio看日志报了一个NullPointer错误，原因是里面的代码还是要依赖classes.dex。所以得用MT管理器重命名文件，把classes2.dex开始重命名，然后把它们塞进去。

最后使用MT管理器去掉签名验证后安装，然后运行。但是发现这个软件还做了检测，告诉我这个版本有问题，点击后进程就退出了。使用 android studio 查看日志可以看到退出堆栈，这里就能看到点击按钮的回调方法。

使用frida hook这个方法，直接跳过退出代码。

```js
Java.perform(function () {
  const ClsName = 'com.******.client.ui.MenuActivity$28';
  const C = Java.use(ClsName);
  C.cancel.implementation = function () {
    console.log('[+] bypass ' + ClsName + '.cancel()');
    // 不调用原 cancel()，直接返回
    return;
  };
  C.submit.implementation = function () {
    console.log('[+] bypass ' + ClsName + '.submit()');
    // 不调用原 submit()，直接返回
    return;
  };
  console.log('[+] hooked ' + ClsName + '.cancel/submit as no-op');
});
```