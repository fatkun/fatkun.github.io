---
title: "破解某金融终端APK"
date: 2025-09-16T10:55:33+08:00
tags: [逆向]
categories: [逆向]
author: "fatkun"
draft: false
typora-root-url: ./..\..\..\static
---

# 背景
这个软件查看深度资料需要开户才可以，但看到实际是后台已经加载数据了，但是会弹一个对话框提示要开户。
本文仅用于记录学习，隐藏部分细节。

# 操作
使用MT管理器查看没有加固，然后使用MT管理器2.15.0学习版去掉签名校验（如果不去掉，后面改完代码签名后，启动会马上退出）。

使用jadx反编译代码，搜索对话框里面的内容，记得要勾选资源文件。刚好在strings资源里面找到文字，然后根据变量(fund_auth_tip)找到使用的地方。

对应的代码在 smali_classes3\l30\m0.smali ，可以看到里面的代码就是创建一个对话框提醒，我们只要在这个方法最开始直接return就可以去掉弹窗了。

使用APK.Tool.GUI.v3.3.1.6（最新版本可能会反编译报错，可以试一下这个版本）反编译代码，修改上面的smali文件。直接在方法最开始加一个 return-void 就行了。

```
.method public static final g(Ll30/m0;)V
    .locals 3

    return-void

    .line 1
    :try_start_0
    const-string v0, "this$0"

    .line 2
    .line 3
    invoke-static {p0, v0}, Lkotlin/jvm/internal/Intrinsics;->checkNotNullParameter(Ljava/lang/Object;Ljava/lang/String;)V

    .line 4
    .line 5
    .line 6
    sget v0, Lk30/l;->warm_reminder:I
```

改完之后，重新编译回去，安装软件即可。安装后验证确实不再弹窗了。
