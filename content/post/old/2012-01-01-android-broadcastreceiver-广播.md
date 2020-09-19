---
title: Android BroadcastReceiver 广播
author: fatkun
type: post
date: 2012-01-01T08:44:20+00:00
url: /2012/01/android-broadcastreceiver-广播.html
duoshuo_thread_id:
  - 6300408820107576066
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:1538:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;receiver</span> <span style="color: #000066;">android:name</span>=<span style="color: #ff0000;">&quot;clsReceiver2&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>  
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;intent-filter<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>  
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;action</span> <span style="color: #000066;">android:name</span>=<span style="color: #ff0000;">&quot;com.testBroadcastReceiver.Internal_2&quot;</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>  
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/intent-filter<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>  
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/receiver<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">&lt;receiver android:name=&quot;clsReceiver2&quot;&gt;  
        &lt;intent-filter&gt;  
            &lt;action android:name=&quot;com.testBroadcastReceiver.Internal_2&quot;/&gt;  
        &lt;/intent-filter&gt;  
    &lt;/receiver&gt;</p></div>
    ";i:2;s:725:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #666666; font-style: italic;">//动态注册广播消息  </span>
            registerReceiver<span style="color: #009900;">&#40;</span>bcrIntenal1, <span style="color: #000000; font-weight: bold;">new</span> IntentFilter<span style="color: #009900;">&#40;</span>INTENAL_ACTION_1<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span></pre></td></tr></table><p class="theCode" style="display:none;">//动态注册广播消息  
            registerReceiver(bcrIntenal1, new IntentFilter(INTENAL_ACTION_1));</p></div>
    ";i:3;s:501:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #666666; font-style: italic;">//取消广播接收器</span>
            unregisterReceiver<span style="color: #009900;">&#40;</span>rhelper<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span></pre></td></tr></table><p class="theCode" style="display:none;">//取消广播接收器
            unregisterReceiver(rhelper);</p></div>
    ";}
categories:
  - Android
tags:
  - Android
  - BroadcastReceiver
  - 广播

---
总结如下：  
广播可用于Service与Activity的之间的通信，也可用于接收一些系统的事件，例如收到短信，电量等信息。
有两种方法注册，静态注册和动态注册
## 静态注册

创建一个类继承BroadcastReceiver，然后在AndroidManifest.xml 添加
<pre escaped="true" lang="xml">&lt;receiver android:name="clsReceiver2"&gt;  
    &lt;intent-filter&gt;  
        &lt;action android:name="com.testBroadcastReceiver.Internal_2"/&gt;  
    &lt;/intent-filter&gt;  
&lt;/receiver&gt;  
</pre>
## 动态注册

继承BroadcastReceiver类，实现onReceive方法。然后registerReceiver它。同一个Receiver还可以“听多个广播”，可以在IntentFilter加多个action。  
主要通过IntentFilter，别人用sendBroadcast(intent)发广播，如果频率一样（IntentFilter里的Action一样）就可以听到广播。
<pre escaped="true" lang="java">//动态注册广播消息  
        registerReceiver(bcrIntenal1, new IntentFilter(INTENAL_ACTION_1));  </pre>
<pre escaped="true" lang="java">//取消广播接收器
        unregisterReceiver(rhelper);</pre>
两篇参考文章：
<a href="http://blog.csdn.net/hellogv/article/details/5999170" target="_blank">http://blog.csdn.net/hellogv/article/details/5999170</a>  
<a href="http://www.cnblogs.com/jico/articles/1838293.html" title="http://www.cnblogs.com/jico/articles/1838293.html" target="_blank">http://www.cnblogs.com/jico/articles/1838293.html</a>