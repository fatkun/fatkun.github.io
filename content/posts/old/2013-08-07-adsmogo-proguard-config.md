---
title: 芒果广告平台混淆代码后不显示广告解决方法
author: fatkun
type: post
date: 2013-08-06T17:37:59+00:00
url: /2013/08/adsmogo-proguard-config.html
duoshuo_thread_id:
  - 6300410024472609537
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:1360:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="other" style="font-family:monospace;">#The below is used for AdsMOGO_Android_SDK_1.3.4 settings
    -dontwarn android.support.v4.**
    -libraryjars libs/android-support-v4.jar
    -libraryjars libs/AdsMOGO_Android_SDK_1.3.4.jar
    -libraryjars libs/Baidu_MobAds_SDK_Agg_3.2.jar
    -libraryjars libs/domob_android_sdk_v3.3.4.jar
    &nbsp;
    -keep class uk.** {*;} 
    -keep class org.** {*;} 
    -keep class android.support.** {*;} 
    -keep class com.adsmogo.** {*;} 
    -keep class com.baidu.** {*;} 
    -keep class cn.domob.** {*;} 
    -keep class net.youmi.android.** {*;} 
    -keep class com.anwo.adsdk.** {*;} 
    -keep class com.suizong.** {*;}</pre></td></tr></table><p class="theCode" style="display:none;">#The below is used for AdsMOGO_Android_SDK_1.3.4 settings
    -dontwarn android.support.v4.**
    -libraryjars libs/android-support-v4.jar
    -libraryjars libs/AdsMOGO_Android_SDK_1.3.4.jar
    -libraryjars libs/Baidu_MobAds_SDK_Agg_3.2.jar
    -libraryjars libs/domob_android_sdk_v3.3.4.jar
    
    -keep class uk.** {*;} 
    -keep class org.** {*;} 
    -keep class android.support.** {*;} 
    -keep class com.adsmogo.** {*;} 
    -keep class com.baidu.** {*;} 
    -keep class cn.domob.** {*;} 
    -keep class net.youmi.android.** {*;} 
    -keep class com.anwo.adsdk.** {*;} 
    -keep class com.suizong.** {*;}</p></div>
    ";}
categories:
  - Android
tags:
  - adsmogo
  - proguard
  - proguard.cfg
  - 混淆代码
  - 芒果
  - 芒果广告平台

---
使用芒果广告平台(adsmogo)混淆代码后广告不显示，我试了N次打包。。。o(╯□╰)o
## 解决方法

新建proguard.cfg文件，不要用芒果提供的那份配置了。。我打死搞不定。。囧  
-libraryjars 不知道有没有用，加了再说，把放到libs下的lib都加进来吧  
然后把你用到的class都不混淆，除了自己的代码, -keep class 表示保留这个类不混淆。
参见以下例子
<pre escaped="true" lang="other">#The below is used for AdsMOGO_Android_SDK_1.3.4 settings
-dontwarn android.support.v4.**
-libraryjars libs/android-support-v4.jar
-libraryjars libs/AdsMOGO_Android_SDK_1.3.4.jar
-libraryjars libs/Baidu_MobAds_SDK_Agg_3.2.jar
-libraryjars libs/domob_android_sdk_v3.3.4.jar

-keep class uk.** {*;} 
-keep class org.** {*;} 
-keep class android.support.** {*;} 
-keep class com.adsmogo.** {*;} 
-keep class com.baidu.** {*;} 
-keep class cn.domob.** {*;} 
-keep class net.youmi.android.** {*;} 
-keep class com.anwo.adsdk.** {*;} 
-keep class com.suizong.** {*;} 
</pre>