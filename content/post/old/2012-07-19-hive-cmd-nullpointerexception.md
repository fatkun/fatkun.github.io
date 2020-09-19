---
title: hive命令行抛NullPointerException
author: fatkun
type: post
date: 2012-07-18T16:11:23+00:00
url: /2012/07/hive-cmd-nullpointerexception.html
duoshuo_thread_id:
  - 6300408865863238401
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:386:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">create temporary function strip as <span style="color: #0000ff;">'com.fatkun.Strip'</span><span style="color: #339933;">;</span></pre></td></tr></table><p class="theCode" style="display:none;">create temporary function strip as 'com.fatkun.Strip';</p></div>
    ";i:2;s:4748:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">hive<span style="color: #339933;">&gt;</span> create temporary function strip as <span style="color: #0000ff;">'com.fatkun.Strip'</span><span style="color: #339933;">;</span>
    OK
    <span style="color: #003399;">Exception</span> in thread <span style="color: #0000ff;">&quot;main&quot;</span> java.<span style="color: #006633;">lang</span>.<span style="color: #003399;">NullPointerException</span>
    	at org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">hadoop</span>.<span style="color: #006633;">hive</span>.<span style="color: #006633;">cli</span>.<span style="color: #006633;">CliDriver</span>.<span style="color: #006633;">processCmd</span><span style="color: #009900;">&#40;</span>CliDriver.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">221</span><span style="color: #009900;">&#41;</span>
    	at org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">hadoop</span>.<span style="color: #006633;">hive</span>.<span style="color: #006633;">cli</span>.<span style="color: #006633;">CliDriver</span>.<span style="color: #006633;">processLine</span><span style="color: #009900;">&#40;</span>CliDriver.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">286</span><span style="color: #009900;">&#41;</span>
    	at org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">hadoop</span>.<span style="color: #006633;">hive</span>.<span style="color: #006633;">cli</span>.<span style="color: #006633;">CliDriver</span>.<span style="color: #006633;">main</span><span style="color: #009900;">&#40;</span>CliDriver.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">516</span><span style="color: #009900;">&#41;</span>
    	at sun.<span style="color: #006633;">reflect</span>.<span style="color: #006633;">NativeMethodAccessorImpl</span>.<span style="color: #006633;">invoke0</span><span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">Native</span> <span style="color: #003399;">Method</span><span style="color: #009900;">&#41;</span>
    	at sun.<span style="color: #006633;">reflect</span>.<span style="color: #006633;">NativeMethodAccessorImpl</span>.<span style="color: #006633;">invoke</span><span style="color: #009900;">&#40;</span>NativeMethodAccessorImpl.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">39</span><span style="color: #009900;">&#41;</span>
    	at sun.<span style="color: #006633;">reflect</span>.<span style="color: #006633;">DelegatingMethodAccessorImpl</span>.<span style="color: #006633;">invoke</span><span style="color: #009900;">&#40;</span>DelegatingMethodAccessorImpl.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">25</span><span style="color: #009900;">&#41;</span>
    	at java.<span style="color: #006633;">lang</span>.<span style="color: #006633;">reflect</span>.<span style="color: #003399;">Method</span>.<span style="color: #006633;">invoke</span><span style="color: #009900;">&#40;</span><span style="color: #003399;">Method</span>.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">597</span><span style="color: #009900;">&#41;</span>
    	at org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">hadoop</span>.<span style="color: #006633;">util</span>.<span style="color: #006633;">RunJar</span>.<span style="color: #006633;">main</span><span style="color: #009900;">&#40;</span>RunJar.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">197</span><span style="color: #009900;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">hive&gt; create temporary function strip as 'com.fatkun.Strip';
    OK
    Exception in thread &quot;main&quot; java.lang.NullPointerException
    	at org.apache.hadoop.hive.cli.CliDriver.processCmd(CliDriver.java:221)
    	at org.apache.hadoop.hive.cli.CliDriver.processLine(CliDriver.java:286)
    	at org.apache.hadoop.hive.cli.CliDriver.main(CliDriver.java:516)
    	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
    	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:39)
    	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:25)
    	at java.lang.reflect.Method.invoke(Method.java:597)
    	at org.apache.hadoop.util.RunJar.main(RunJar.java:197)</p></div>
    ";i:3;s:1336:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>hive.cli.print.header<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>false<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">&lt;property&gt;
      &lt;name&gt;hive.cli.print.header&lt;/name&gt;
      &lt;value&gt;false&lt;/value&gt;
    &lt;/property&gt;</p></div>
    ";}
categories:
  - hadoop
tags:
  - hadoop

---
我只是执行了一下这个代码
<pre escaped="true" lang="java">create temporary function strip as 'com.fatkun.Strip';</pre>
就抛出异常
<pre escaped="true" lang="java">hive&gt; create temporary function strip as 'com.fatkun.Strip';
OK
Exception in thread "main" java.lang.NullPointerException
	at org.apache.hadoop.hive.cli.CliDriver.processCmd(CliDriver.java:221)
	at org.apache.hadoop.hive.cli.CliDriver.processLine(CliDriver.java:286)
	at org.apache.hadoop.hive.cli.CliDriver.main(CliDriver.java:516)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:39)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:25)
	at java.lang.reflect.Method.invoke(Method.java:597)
	at org.apache.hadoop.util.RunJar.main(RunJar.java:197)</pre>
从代码中看CliDriver.java:221，  
原来和print header有关系。。。囧之前是为了打印header  
默认这个是false的，所以把它去掉或者在hive-site置为false即可
<pre escaped="true" lang="xml">&lt;property&gt;
  &lt;name&gt;hive.cli.print.header&lt;/name&gt;
  &lt;value&gt;false&lt;/value&gt;
&lt;/property&gt;
</pre>