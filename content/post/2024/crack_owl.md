---
title: "逆向某某鹰文件，破解VIP功能"
date: 2024-07-19T14:22:01+08:00
tags: [android, 逆向]
categories: [android]
author: "fatkun"
draft: false
typora-root-url: ./..\..\..\static
---

# 声明

仅用于学习用途，不可用作非法用途。

# 软件

- [APKToolGUI](https://github.com/AndnixSH/APKToolGUI)
- jadx
- frida



我下载的app版本是13.1.1



# 分析过程

这个软件没有加壳，直接用jadx查看源码。代码被混淆了，可以在工具->反混淆勾选，代码相对容易分析一点。先尝试搜索vip之类的字符串，字符串搜索到一些，但是没看到代码引用。

只能无目的浏览一下代码，看到包名有些没有混淆，例如 `com.****.fileexplorer.purchase`，在里面找到一系列的`OWLFILES_MEMBER` 开头的变量，其中有个LEVEL的变量特别在意。

搜索`OWLFILES_MEMBER_LEVEL`找到一处代码，在`com/***/fileexplorer/purchase/account/a0`，这段代码看起来是读取这个值，如果没有则返回0。

```java

    /* renamed from: g */
    public static long m6862g(Context context) {
        Long l10 = f4784b;
        if (l10 != null) {
            return l10.longValue();
        }
        C5997g c5997g = new C5997g(context);
        if (m6864i(context)) {
            f4784b = Long.valueOf(c5997g.m8776c("OWLFILES_MEMBER_LEVEL", 0L));
        } else {
            f4784b = 0L;
        }
        return f4784b.longValue();
    }
```

我们可以使用frida hook查看返回值。使用右键“复制为frida片段”，把复制的片段嵌套在`Java.perform(function(){代码...}`里。

```javascript
Java.perform(function(){
    let AbstractC5530a0 = Java.use("com.*****.fileexplorer.purchase.account.a0");
    AbstractC5530a0["g"].implementation = function (context) {
        console.log(`AbstractC5530a0.m6862g is called: context=${context}`);
        let result = this["g"](context);
        console.log(`AbstractC5530a0.m6862g result=${result}`);
        return result;
    };
})
```

frida 具体用法不说了，自己搜索，frida 执行命令

```bash
frida -U -f com.***.apps.fileexplorerfree -l .\t.js
```

可以看到值都是0。这里可以把 `return result;` 直接改成 `return 1;`尝试一下，发现可以使用VIP功能了。

# 修改

使用APK Tool GUI，拖入APK，点击`反编译`。

<img src="/img/crack_owl/image-20240719173605333.png" alt="image-20240719173605333" style="zoom:50%;" />

使用vscode打开smali文件，从上面代码看我们要返回一个long类型的数字。我对smali语法不熟，直接问AI还挺方便的。直接在代码开头返回1。

```smali
.method public static g(Landroid/content/Context;)J
    .locals 3
    
    // 添加下面两行
    const-wide/16 v0, 0x1L
    return-wide v0

    // 省略其他代码
.end method
```

修改保存后，点击`编译` 重新编译成APK文件，编译后会自动签名，就可以把app传到手机上安装了。
