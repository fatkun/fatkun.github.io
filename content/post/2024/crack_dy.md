---
title: "去除某直播平台广告"
date: 2024-08-05T14:51:54+08:00
tags: [android, 逆向]
categories: [android]
author: "fatkun"
draft: false
typora-root-url: ./..\..\..\static
---

# 声明

仅用于学习用途，不可用作非法用途。

# 工具

- jadx
- mt工具箱
- apktool

# 分析

软件版本：7.7.8

这个直播平台的广告主要有开屏广告和在后台播放一段时间后，切回应用时会跳出广告。由于其他的广告干扰不大，所以只去掉这两种广告。

首先用MT工具箱记录Activity，看看有没有启动的Activity。完全关闭应用后，重新打开。发现开屏广告没有新的Activity，不过知道了首页的Activity是什么。

再来测试切回应用的广告，这时就看到有新的Activity(`HotStartSplashActivity`)了。同时在同一个Package里面也有一个 `ColdStartSplashAd`，猜测是开屏广告。

找到Activity后，就找哪里启动这个Activity的。用MT工具看没有加固，直接用jadx分析代码。

```java
        public final void m22715a(@NotNull Context context) {
            if (PatchProxy.proxy(new Object[]{context}, this, f28598a, false, "686f70ac", new Class[]{Context.class}, Void.TYPE).isSupport) {
                return;
            }
            Intrinsics.checkNotNullParameter(context, "context");
            Intent intent = new Intent(context, (Class<?>) HotStartSplashActivity.class);
            if (!(context instanceof Activity)) {
                intent.addFlags(CommonNetImpl.FLAG_AUTH);
            }
            try {
                context.startActivity(intent);
            } catch (Exception e7) {
                DYInstantLog.m11921a(DYLogFirstTagEnum.DY_LOG_Action_ShowHotAD, "热启动广告activity启动异常：" + e7.getMessage());
            }
        }
```

找到调用链路，HotStartSplashAd代码里面

```java
public final void a(SplashAdInfo splashAdInfo) {
    if (PatchProxy.proxy(new Object[]{splashAdInfo}, this, f28605c, false, "7a93ae5a", new Class[]{SplashAdInfo.class}, Void.TYPE).isSupport) {
        return;
    }
    HotStartSplashAd hotStartSplashAd = HotStartSplashAd.f28604d;
    HotStartSplashAd.mSplashAdInfo = SplashAdManager.this.getSplashAdInfo();
    if (splashAdInfo.getAdBean() != null) {
        SplashAdDot.f28661z.m22780g(SplashAdPos.f28774h.m22912a(), "0", "1");
        DYInstantLog.m11925e(DYLogFirstTagEnum.DY_LOG_Action_ShowHotAD, "热启动广告数据获取成功");
        HotStartSplashActivity.INSTANCE.m22715a(context);
    }
}
```

这里在判断不为空的时候，启动Activity。找到代码里，修改也很容易，直接返回就好了。

找到对应方法的smali代码，插入 `return-void`，注意这个是匿名方法，在一个$的文件里面。

再来分析冷启动的代码，这里主要是找有没有一些关键字，AD、广告之类的，最终看到是这里的代码。

```java
    /* renamed from: A */
    public final Observable<Boolean> m22662A() {
        PatchProxyResult proxy = PatchProxy.proxy(new Object[0], this, f28551k, false, "55b00877", new Class[0], Observable.class);
        if (proxy.isSupport) {
            return (Observable) proxy.result;
        }
        f28552l.m22902n();
        MADProviderUtils.m22425a(LaunchAnalyzerConstant.f7610f);
        SplashAdDot.f28661z.m22769C(System.currentTimeMillis());
        OperationInfoPreload operationInfoPreload = OperationInfoPreload.f28825d;
        OperationInfo m22958c = operationInfoPreload.m22958c();
        DYLogSdk.m11965e("launcher", "检查是否有运营图:" + m22958c.getHasOperation() + "  运营图数据加载过？ " + operationInfoPreload.m22957b());
        if (m22958c.getHasOperation()) {
            m22675P(m22958c);
        } else {
            MonitorLog.f30456c.m24217b(LaunchStageLog.NO_LAUNCH_OPERATION);
            m22664C();
        }
        return this.homeObservable;
    }
```

这里代码是检查是否有运营图，如果有就展示运营图，没有就展示广告。我都不想展示，直接跳过好了。

![image-20240805152554462](/img/crack_dy/image-20240805152554462.png)

在if之前直接使用goto 跳到最后的返回。



