---
title: android PopupWindow
author: fatkun
type: post
date: 2012-06-24T05:28:13+00:00
url: /2012/06/android-popupwindow.html
duoshuo_thread_id:
  - 6300408859097826049
wp-syntax-cache-content:
  - |
    a:4:{i:1;s:2716:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #003399;">View</span> loadingView <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">getLayoutInflater</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">inflate</span><span style="color: #009900;">&#40;</span>R.<span style="color: #006633;">layout</span>.<span style="color: #006633;">loading</span>, <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    PopupWindow loaddingPopup <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> PopupWindow<span style="color: #009900;">&#40;</span>loadingView, LayoutParams.<span style="color: #006633;">MATCH_PARENT</span>, LayoutParams.<span style="color: #006633;">MATCH_PARENT</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    loaddingPopup.<span style="color: #006633;">setAnimationStyle</span><span style="color: #009900;">&#40;</span>R.<span style="color: #006633;">style</span>.<span style="color: #006633;">popupWindow</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">//配置动画</span>
    loaddingPopup.<span style="color: #006633;">update</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    loaddingPopup.<span style="color: #006633;">showAtLocation</span><span style="color: #009900;">&#40;</span>findViewById<span style="color: #009900;">&#40;</span>R.<span style="color: #006633;">id</span>.<span style="color: #006633;">btnRefresh</span><span style="color: #009900;">&#41;</span>, Gravity.<span style="color: #006633;">CENTER</span>, <span style="color: #cc66cc;">0</span>, <span style="color: #cc66cc;">0</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">//显示在中间</span></pre></td></tr></table><p class="theCode" style="display:none;">View loadingView = this.getLayoutInflater().inflate(R.layout.loading, null);
    PopupWindow loaddingPopup = new PopupWindow(loadingView, LayoutParams.MATCH_PARENT, LayoutParams.MATCH_PARENT);
    loaddingPopup.setAnimationStyle(R.style.popupWindow); //配置动画
    loaddingPopup.update();
    loaddingPopup.showAtLocation(findViewById(R.id.btnRefresh), Gravity.CENTER, 0, 0); //显示在中间</p></div>
    ";i:2;s:2252:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;?xml</span> <span style="color: #000066;">version</span>=<span style="color: #ff0000;">&quot;1.0&quot;</span> <span style="color: #000066;">encoding</span>=<span style="color: #ff0000;">&quot;utf-8&quot;</span><span style="color: #000000; font-weight: bold;">?&gt;</span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;set</span> <span style="color: #000066;">xmlns:android</span>=<span style="color: #ff0000;">&quot;http://schemas.android.com/apk/res/android&quot;</span> <span style="color: #000000; font-weight: bold;">&gt;</span></span>
    &nbsp;
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;alpha</span></span>
    <span style="color: #009900;">        <span style="color: #000066;">android:duration</span>=<span style="color: #ff0000;">&quot;500&quot;</span></span>
    <span style="color: #009900;">        <span style="color: #000066;">android:fromAlpha</span>=<span style="color: #ff0000;">&quot;0.0&quot;</span></span>
    <span style="color: #009900;">        <span style="color: #000066;">android:interpolator</span>=<span style="color: #ff0000;">&quot;@android:anim/accelerate_interpolator&quot;</span></span>
    <span style="color: #009900;">        <span style="color: #000066;">android:toAlpha</span>=<span style="color: #ff0000;">&quot;1.0&quot;</span> <span style="color: #000000; font-weight: bold;">/&gt;</span></span>
    &nbsp;
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/set<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot;?&gt;
    &lt;set xmlns:android=&quot;http://schemas.android.com/apk/res/android&quot; &gt;
    
        &lt;alpha
            android:duration=&quot;500&quot;
            android:fromAlpha=&quot;0.0&quot;
            android:interpolator=&quot;@android:anim/accelerate_interpolator&quot;
            android:toAlpha=&quot;1.0&quot; /&gt;
    
    &lt;/set&gt;</p></div>
    ";i:3;s:2095:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;?xml</span> <span style="color: #000066;">version</span>=<span style="color: #ff0000;">&quot;1.0&quot;</span> <span style="color: #000066;">encoding</span>=<span style="color: #ff0000;">&quot;utf-8&quot;</span><span style="color: #000000; font-weight: bold;">?&gt;</span></span>  
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;resources<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>  
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;style</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;popupWindow&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>  
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;item</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;android:windowEnterAnimation&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>@anim/popupwindow<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/item<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>  
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/style<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>  
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/resources<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot;?&gt;  
    &lt;resources&gt;  
        &lt;style name=&quot;popupWindow&quot;&gt;  
            &lt;item name=&quot;android:windowEnterAnimation&quot;&gt;@anim/popupwindow&lt;/item&gt;  
        &lt;/style&gt;  
    &lt;/resources&gt;</p></div>
    ";i:4;s:625:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">popupWindow.<span style="color: #006633;">setAnimationStyle</span><span style="color: #009900;">&#40;</span>R.<span style="color: #006633;">anim</span>.<span style="color: #006633;">popupwindow</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>  <span style="color: #666666; font-style: italic;">// 错误写法</span></pre></td></tr></table><p class="theCode" style="display:none;">popupWindow.setAnimationStyle(R.anim.popupwindow);  // 错误写法</p></div>
    ";}
categories:
  - Android
tags:
  - Android
  - popwindow

---
<pre escaped="true" lang="java">View loadingView = this.getLayoutInflater().inflate(R.layout.loading, null);
PopupWindow loaddingPopup = new PopupWindow(loadingView, LayoutParams.MATCH_PARENT, LayoutParams.MATCH_PARENT);
loaddingPopup.setAnimationStyle(R.style.popupWindow); //配置动画
loaddingPopup.update();
loaddingPopup.showAtLocation(findViewById(R.id.btnRefresh), Gravity.CENTER, 0, 0); //显示在中间
</pre>
配置一个animate, popupwindow.xml
<pre escaped="true" lang="xml">&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;set xmlns:android="http://schemas.android.com/apk/res/android" &gt;

    &lt;alpha
        android:duration="500"
        android:fromAlpha="0.0"
        android:interpolator="@android:anim/accelerate_interpolator"
        android:toAlpha="1.0" /&gt;

&lt;/set&gt;</pre>
除了要配置一个animate外，还需要配置style
<pre escaped="true" lang="xml">&lt;?xml version="1.0" encoding="utf-8"?&gt;  
&lt;resources&gt;  
    &lt;style name="popupWindow"&gt;  
        &lt;item name="android:windowEnterAnimation"&gt;@anim/popupwindow&lt;/item&gt;  
    &lt;/style&gt;  
&lt;/resources&gt;  </pre>
容易犯错的地方是，这里的setAnimationStyle是指style，不是动画
<pre escaped="true" lang="java">popupWindow.setAnimationStyle(R.anim.popupwindow);  // 错误写法 </pre>
popwindow通过setAnimationStyle(int animationStyle)函数来设置动画效果  
android:windowEnterAnimation表示进入窗口动画  
android:windowExitAnimation表示窗口退出动画 
更多信息：[android PopupWindow 以及activity切换的动画效果对比][1]

 [1]: http://lipeng88213.iteye.com/blog/1115014