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

## 右侧浮动广告
右侧浮动广告，代码在`com.****.module.player.p092p.adfloatball.AdFloatBallNeuron`里。

AdFloatBallNeuron类里面有三个匿名类，`AdFloatBallView$bindData$1`、`AdFloatBallView$bindData$2`、`AdFloatBallView$bindData$3`，可以在call方法里面直接返回。

其中有一个是返回Boolean对象，在smali语法里面是这样写
```
    sget-object v0, Ljava/lang/Boolean;->FALSE:Ljava/lang/Boolean;
    return-object v0
```


## 中部横幅广告
如何找到对应的代码？我是先用autojs分析布局，找出对应控件的id，但是由于id是混淆的，有重复的，只能一个个找，看看在某个layout里面是否都有这些id。但是找到layout好像也没用，在代码中没有找到对应layout。

之后通过搜索R.id.xxx 找到相关的代码。
``` java
        View.inflate(context, R.layout.f264114j0, this);
        View findViewById = findViewById(R.id.a5n);
        Intrinsics.checkNotNullExpressionValue(findViewById, "findViewById(R.id.bg_view_for_rambo)");
        this.ivViewBackground = findViewById;
        findViewById.setBackgroundColor(((Number) com.*****.sdk.apkdownload.ExtensionsKt.m123158n(RoomUtil.m60539s(this), Integer.valueOf(BaseThemeUtils.m14626b(context, R.attr.f258987f9)), 0)).intValue());
        View findViewById2 = findViewById(R.id.erx);
        Intrinsics.checkNotNullExpressionValue(findViewById2, "findViewById(R.id.iv_game_bg)");
        this.ivGameBackground = (DYImageView) findViewById2;
        View findViewById3 = findViewById(R.id.erz);
        Intrinsics.checkNotNullExpressionValue(findViewById3, "findViewById(R.id.iv_game_icon)");
        this.ivGameIcon = (DYImageView) findViewById3;
        View findViewById4 = findViewById(R.id.el2);
        Intrinsics.checkNotNullExpressionValue(findViewById4, "findViewById(R.id.iv_close)");
        ImageView imageView = (ImageView) findViewById4;

```

代码在`XHCommonPlayerBannerView`和`XHCommonPlayerBannerView2`里面，可以在bindData里面拦截。

以XHCommonPlayerBannerView2举例，在匿名类`class XHCommonPlayerBannerView2$bindData$1`里面，在run方法里面拦截
```java
public final class XHCommonPlayerBannerView2$bindData$1 implements Runnable {

    /* renamed from: c */
    public static PatchRedirect f76594c;

    /* renamed from: b */
    public final /* synthetic */ XHCommonBannerStyleData f76596b;

    public XHCommonPlayerBannerView2$bindData$1(XHCommonBannerStyleData xHCommonBannerStyleData) {
        data = xHCommonBannerStyleData;
    }

    @Override // java.lang.Runnable
    public final void run() {
        if (PatchProxy.proxy(new Object[0], this, f76594c, false, "7ca8490d", new Class[0], Void.TYPE).isSupport) {
            return;
        }
        XHCommonBannerStyleData xHCommonBannerStyleData = data;
        if (xHCommonBannerStyleData instanceof DefaultStyle) {
            XHCommonPlayerBannerView2.m56696Jc(XHCommonPlayerBannerView2.this, (DefaultStyle) xHCommonBannerStyleData);
        }
        Activity m14684a = DYActivityUtils.m14684a(XHCommonPlayerBannerView2.this);
        if (m14684a != null) {
            ThemeResBean m75780c = RamboSkinProviderUtil.INSTANCE.m75780c(m14684a);
            int m74739g = RamboProviderUtil.m74739g(m14684a);
            XHCommonPlayerBannerView2.this.mo56399J7(m74739g, ThemeResBeanKt.m75790a(m74739g, m75780c));
        }
    }
}
```

如果只是上面拦截，广告不加载了，但是有一个空白的框，找到调用它的上一层方法，从这里拦截。
`com.*****.module.player.p106p.animatedad.widget.commonbanner.NewGamePlayerAdPresenter`
```java
    /* renamed from: n */
    private final void m56626n(Context context, String bizType) {
        ILandHalfContentProvider iLandHalfContentProvider;
        if (PatchProxy.proxy(new Object[]{context, bizType}, this, f76460h, false, "ab81d0c2", new Class[]{Context.class, String.class}, Void.TYPE).isSupport) {
            return;
        }
        if (RoomUtil.m60538r(context)) {
            RamboXHAnimatedAdCompatNeuron ramboXHAnimatedAdCompatNeuron = (RamboXHAnimatedAdCompatNeuron) Hand.m132371l(DYActivityUtils.m14690g(context), RamboXHAnimatedAdCompatNeuron.class);
            if (ramboXHAnimatedAdCompatNeuron != null) {
                ramboXHAnimatedAdCompatNeuron.m74770tI(m56629q());
            }
        } else if (RoomUtil.m60535o(context) && (iLandHalfContentProvider = (ILandHalfContentProvider) DYRouter.getInstance().navigationLive(context, ILandHalfContentProvider.class)) != null) {
            iLandHalfContentProvider.mo67745c1(m56629q().mo56402j());
            iLandHalfContentProvider.mo67754n0(0L, 0);
        }
        IXHCommonBannerView m56629q = m56629q();
        XHCommonBannerStyleData xHCommonBannerStyleData = null;
        XHCommonPlayerBannerView xHCommonPlayerBannerView = (XHCommonPlayerBannerView) (!(m56629q instanceof XHCommonPlayerBannerView) ? null : m56629q);
        if (xHCommonPlayerBannerView != null) {
            xHCommonPlayerBannerView.setGifFrequencyController(new FrequencyControlGif(this.mFreq));
            xHCommonPlayerBannerView.setMp4FrequencyController(new FrequencyControlMp4(this.mFreq));
        }
        IAbsAdBean iAbsAdBean = this.mRealGameData;
        if (iAbsAdBean instanceof StarSeaDataBean) {
            if (!(iAbsAdBean instanceof StarSeaDataBean)) {
                iAbsAdBean = null;
            }
            StarSeaDataBean starSeaDataBean = (StarSeaDataBean) iAbsAdBean;
            if (starSeaDataBean != null) {
                xHCommonBannerStyleData = XHCommonBannerStyleKt.m56671d(starSeaDataBean, bizType);
            }
        } else if (iAbsAdBean instanceof CommonAdBean) {
            if (!(iAbsAdBean instanceof CommonAdBean)) {
                iAbsAdBean = null;
            }
            CommonAdBean commonAdBean = (CommonAdBean) iAbsAdBean;
            if (commonAdBean != null) {
                xHCommonBannerStyleData = XHCommonBannerStyleKt.m56670c(commonAdBean);
            }
        }
        m56629q.mo56398C8(xHCommonBannerStyleData);
    }

```

## 其他广告
`com.*****.module.yuba2.dynamic.hometab.follow.DynamicVideoAdManager`
不知道是什么广告

## 通用广告
`com.*****.sdk.ad.AdView`
能够屏蔽首页的一些广告，但会导致部分地方空白。能够屏蔽热议首页广告（不完全）。

```java
    public void bindAd(AdBean adBean) {
        IAdView iAdView;
        if (PatchProxy.proxy(new Object[]{adBean}, this, patch$Redirect, false, "8331d9cb", new Class[]{AdBean.class}, Void.TYPE).isSupport || (iAdView = this.mAdView) == null) {
            return;
        }
        iAdView.b(adBean);
    }

    public void bindAdByJson(String str) {
        IAdView iAdView;
        if (PatchProxy.proxy(new Object[]{str}, this, patch$Redirect, false, "a5187cea", new Class[]{String.class}, Void.TYPE).isSupport || (iAdView = this.mAdView) == null) {
            return;
        }
        iAdView.b((AdBean) Utils.t(str, AdBean.class));
    }
```

## 关播广告
找到一个类似播放广告视频的类`com.*****.sdk.ad.douyu.video.AdVideoPlayerPresenter`，使用frida监控这个类的所有方法，可以看到有一个是从这个类请求的。`com.*****.module.player.p.liveclose.rambo.widget.CloseRoomAdViewFullscreen`

```java
    public final void Bd(@Nullable AdBean adBean) {
        final DyAdBean dyAdBean;
        boolean z7 = true;
        if (PatchProxy.proxy(new Object[]{adBean}, this, f50296r, false, "5d1c3069", new Class[]{AdBean.class}, Void.TYPE).isSupport || adBean == null || (dyAdBean = adBean.getDyAdBean()) == null) {
            return;
        }
        if (dyAdBean.localIsPlayedCompleted) {
            DYInstantLog.e("关播广告", "已经播放完成了，不再播放");
            return;
        }
        if (this.currentDyAdBean != null) {
            DYInstantLog.e("关播广告", "已经有广告数据了，不再重复播放");
            return;
        }
        省略...
    }
```