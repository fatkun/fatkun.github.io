---
title: Hive为什么会创建DELETEME表
author: fatkun
type: post
date: 2012-04-10T16:16:45+00:00
url: /2012/04/hive-deleteme-table.html
duoshuo_thread_id:
  - 6300408840877769474
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:1340:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
     <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>datanucleus.fixedDatastore<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
     <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>true<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">&lt;property&gt;
     &lt;name&gt;datanucleus.fixedDatastore&lt;/name&gt;
     &lt;value&gt;true&lt;/value&gt;
    &lt;/property&gt;</p></div>
    ";i:2;s:1346:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
     <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>datanucleus.autoCreateSchema<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
     <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>false<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">&lt;property&gt;
     &lt;name&gt;datanucleus.autoCreateSchema&lt;/name&gt;
     &lt;value&gt;false&lt;/value&gt;
    &lt;/property&gt;</p></div>
    ";}
categories:
  - J2EE
tags:
  - hive

---
在Hive中会去取schme name和catalog（暂时不知道这个东西有什么用）  
是第三方的库datanucleus在操作，  
可以看到它创建DELETEME123213一些随机数字的表，然后删掉。。目的就为了去获取schme name和catalog
可以在hive-site.xml配置，不让做这个操作&#8230;
<pre escaped="true" lang="xml">&lt;property&gt;
 &lt;name&gt;datanucleus.fixedDatastore&lt;/name&gt;
 &lt;value&gt;true&lt;/value&gt;
&lt;/property&gt;</pre>
这样会导致的结果暂时未知。。。o(╯□╰)o  
另外，最好把datanucleus.autoCreateSchema设为false  
官方的注释中表明，如果你第一次已经建好了表，就把这个设回false，为了方便第一次创建表结构。
<pre escaped="true" lang="xml">&lt;property&gt;
 &lt;name&gt;datanucleus.autoCreateSchema&lt;/name&gt;
 &lt;value&gt;false&lt;/value&gt;
&lt;/property&gt;</pre>