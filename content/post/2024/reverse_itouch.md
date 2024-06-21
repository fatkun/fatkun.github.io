---
title: "逆向某电新闻"
date: 2024-06-21T14:22:01+08:00
tags: [android, 逆向]
categories: [android]
author: "fatkun"
draft: false
typora-root-url: ./..\..\..\static
---

# 声明

仅用于学习用途，不可用作非法用途。

以下操作参考这篇文章 [安卓逆向--某c电新闻x-itouchtv-ca-signature参数分析](https://blog.wen2go.site/2022/04/21/20220421/) 实现。

# 操作

## 前提要求

- 一台root的机器（我使用真机，从刷机包找到boot.img，使用magisk给boot.img打补丁，最后使用fastboot刷人boot_patch.img）

## 脱壳静态分析

由于apk用了360加固（可以使用`PKID`查看），所以得先把代码dump出来。

安装`frida`, `objection ` 等软件

```
pip3 install frida
pip3 install frida-tools
pip3 install objection
```

安装ADB工具，确保 `adb devices` 能够列出机器，如果没有列出

- 在电脑管理设备页面检查驱动是否安装了
- 在手机检查开发者选项里，USB调试是否已经打开

原文是用 objection 配合 frida_dexdump 使用，但是我没法使用，可能是 frida_dexdump 已经不更新了。

```
pip3 install frida_dexdump
```

[下载frida_server](https://github.com/frida/frida/releases)文件放到手机目录下

```
adb push .\frida-server /data/local/tmp
adb shell
```

进入shell之后

```bash
su
cd /data/local/tmp
chmod +x frida-server
./frida-server
```

另外我尝试单独用 frida_dexdump ，能导出dex文件，但是导出的不是我想要的代码

```bash
frida-hexdump -U -f com.touchtv.touchtv
```

这里找到[一篇文章](https://www.kancloud.cn/ay947528/aypy/2837384)，发现可以导出dex

脚本地址：https://github.com/r0ysue/frida_dump 

```bash
frida -U --no-pause -f com.touchtv.touchtv -l dump_dex.js
```

执行之后，结果在手机的`/data/data/{包名}/files/`目录下

dump_dex.js 内容如下

```javascript
function get_self_process_name() {
    var openPtr = Module.getExportByName('libc.so', 'open');
    var open = new NativeFunction(openPtr, 'int', ['pointer', 'int']);

    var readPtr = Module.getExportByName("libc.so", "read");
    var read = new NativeFunction(readPtr, "int", ["int", "pointer", "int"]);

    var closePtr = Module.getExportByName('libc.so', 'close');
    var close = new NativeFunction(closePtr, 'int', ['int']);

    var path = Memory.allocUtf8String("/proc/self/cmdline");
    var fd = open(path, 0);
    if (fd != -1) {
        var buffer = Memory.alloc(0x1000);

        var result = read(fd, buffer, 0x1000);
        close(fd);
        result = ptr(buffer).readCString();
        return result;
    }

    return "-1";
}

function dump_dex() {
    var libart = Process.findModuleByName("libart.so");
    var addr_DefineClass = null;
    var symbols = libart.enumerateSymbols();
    for (var index = 0; index < symbols.length; index++) {
        var symbol = symbols[index];
        var symbol_name = symbol.name;
        //这个DefineClass的函数签名是Android9的
        //_ZN3art11ClassLinker11DefineClassEPNS_6ThreadEPKcmNS_6HandleINS_6mirror11ClassLoaderEEERKNS_7DexFileERKNS9_8ClassDefE
        if (symbol_name.indexOf("ClassLinker") >= 0 && 
            symbol_name.indexOf("DefineClass") >= 0 && 
            symbol_name.indexOf("Thread") >= 0 && 
            symbol_name.indexOf("DexFile") >= 0 ) {
            console.log(symbol_name, symbol.address);
            addr_DefineClass = symbol.address;
        }
    }
    var dex_maps = {};

    console.log("[DefineClass:]", addr_DefineClass);
    if (addr_DefineClass) {
        Interceptor.attach(addr_DefineClass, {
            onEnter: function (args) {
                var dex_file = args[5];
                //ptr(dex_file).add(Process.pointerSize) is "const uint8_t* const begin_;"
                //ptr(dex_file).add(Process.pointerSize + Process.pointerSize) is "const size_t size_;"
                var base = ptr(dex_file).add(Process.pointerSize).readPointer();
                var size = ptr(dex_file).add(Process.pointerSize + Process.pointerSize).readUInt();

                if (dex_maps[base] == undefined) {
                    dex_maps[base] = size;
                    var magic = ptr(base).readCString();
                    if (magic.indexOf("dex") == 0) {
                        var process_name = get_self_process_name();
                        if (process_name != "-1") {
                            var dex_path = "/data/data/" + process_name + "/files/" + base.toString(16) + "_" + size.toString(16) + ".dex";
                            console.log("[find dex]:", dex_path);
                            var fd = new File(dex_path, "wb");
                            if (fd && fd != null) {
                                var dex_buffer = ptr(base).readByteArray(size);
                                fd.write(dex_buffer);
                                fd.flush();
                                fd.close();
                                console.log("[dump dex]:", dex_path);

                            }
                        }
                    }
                }
            }, onLeave: function (retval) {
            }
        });
    }
}

var is_hook_libart = false;

function hook_dlopen() {
    Interceptor.attach(Module.findExportByName(null, "dlopen"), {
        onEnter: function (args) {
            var pathptr = args[0];
            if (pathptr !== undefined && pathptr != null) {
                var path = ptr(pathptr).readCString();
                //console.log("dlopen:", path);
                if (path.indexOf("libart.so") >= 0) {
                    this.can_hook_libart = true;
                    console.log("[dlopen:]", path);
                }
            }
        },
        onLeave: function (retval) {
            if (this.can_hook_libart && !is_hook_libart) {
                dump_dex();
                is_hook_libart = true;
            }
        }
    })

    Interceptor.attach(Module.findExportByName(null, "android_dlopen_ext"), {
        onEnter: function (args) {
            var pathptr = args[0];
            if (pathptr !== undefined && pathptr != null) {
                var path = ptr(pathptr).readCString();
                //console.log("android_dlopen_ext:", path);
                if (path.indexOf("libart.so") >= 0) {
                    this.can_hook_libart = true;
                    console.log("[android_dlopen_ext:]", path);
                }
            }
        },
        onLeave: function (retval) {
            if (this.can_hook_libart && !is_hook_libart) {
                dump_dex();
                is_hook_libart = true;
            }
        }
    });
}


setImmediate(hook_dlopen);
```

可能会有出错，先忽略，先用`jadx`分析。

搜索关键字找到生成header的地方，有多个位置有类似的代码，可以静态分析一下哪个是app调用的。

![image-20240621145718722](/img/reverse_itouch/image-20240621145718722.png)

里面还可以找到是怎么签名的，签名方式不变，还是`HMAC`，里面有些内容是base64后的，需要decode。



## 动态分析

由于我已经有了之前别人的php，我这里不需要抓包分析，我只需要分析header信息是什么。

```bash
objection -g  com.touchtv.touchtv explore -s "android sslpinning disable --quiet"
```

使用objection hook功能，但是我这里会提示找不到类，可能app新版本禁止了

```
android hooking watch class com.touchtv.internetSDK.network.d
```

换了一种方式去hook，但我对objection不熟，能用就行

把以下脚本保存1.js

```javascript
function foo(clz){
    console.log("--------", clz)
    clz.v.implementation = function ( url,  body,  method,  extraParams) {
        send("arg0:" + url)
        send("arg1:" + body)
        send("arg2:" + method)

        var Map = Java.use('java.util.HashMap');
        var map = this.v(url,  body,  method,  extraParams)
        var res_map = Java.cast(map, Map);
        send("map:" + res_map.toString())

    }
}

Java.perform(function(){
    Java.choose("dalvik.system.PathClassLoader",{
        onMatch: function(instance){
            console.log(instance)
            console.log(Java.ClassFactory)
            var factory = Java.ClassFactory.get(instance)
            try{
                var myClass = factory.use("com.touchtv.internetSDK.network.d")
                foo(myClass)
                return "stop"
            }catch(e){
                console.log("next")
                console.log(e)
            }
        },
        onComplete:function(){
            console.log("Done")
        }
    })
})
```

在objection里引入这个js（如果要更新js，则需要退出objection重新import）

```
import ./1.js
```

代码会报错，不过无所谓(对objection不熟)，这段代码是hook `com.touchtv.internetSDK.network.d` 的 v 方法，拿到输入参数和输出结果。

执行完之后，回到手机上，点击APP的页面，然后可以在CMD看到hook的输出。

![image-20240621151358272](/img/reverse_itouch/image-20240621151358272.png)

这样我们就拿到所有header信息了，幸运的是，这里我发现只要拿其中一个header就能够请求成功了。



# 参考

[安卓逆向--某c电新闻x-itouchtv-ca-signature参数分析](https://blog.wen2go.site/2022/04/21/20220421/)

[看雪dump dex](https://www.kancloud.cn/ay947528/aypy/2837384)
