---
title: XDoclet – discriminator标签（子类，同一个表）
author: fatkun
type: post
date: 2010-09-13T12:11:29+00:00
url: /2010/09/xdoclet-discriminator.html
duoshuo_thread_id:
  - 6300408770182775553
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:744:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">@hibernate.<span style="color: #000000; font-weight: bold;">class</span>
    @hibernate.<span style="color: #006633;">discriminator</span> column<span style="color: #339933;">=</span><span style="color: #0000ff;">&quot;ftype&quot;</span> type<span style="color: #339933;">=</span><span style="color: #0000ff;">&quot;string&quot;</span> length<span style="color: #339933;">=</span><span style="color: #0000ff;">&quot;50&quot;</span></pre></td></tr></table><p class="theCode" style="display:none;">@hibernate.class
    @hibernate.discriminator column=&quot;ftype&quot; type=&quot;string&quot; length=&quot;50&quot;</p></div>
    ";i:2;s:466:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">@hibernate.<span style="color: #006633;">subclass</span> discriminator<span style="color: #339933;">-</span>value <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;AAA&quot;</span></pre></td></tr></table><p class="theCode" style="display:none;">@hibernate.subclass discriminator-value = &quot;AAA&quot;</p></div>
    ";}
categories:
  - J2EE
tags:
  - discriminator
  - hibernate
  - XDoclet

---
使用XDoclet生成子类映射配置， 简单说一下，只当自己记录了。  
这是一个“每棵继承树映射成一张表”的方法，也就是在这个表里加一个字段来区分子类  
在父类加入
<pre escaped="true" lang="java">@hibernate.class
@hibernate.discriminator column="ftype" type="string" length="50"</pre>
在子类中加入
<pre escaped="true" lang="java">@hibernate.subclass discriminator-value = "AAA"</pre>
更多的你可以参考以下网址：
### [<span style="font-weight: normal;">XDoclet &#8211; discriminator标签</span>][1]

[XDoclet &#8211;hibernate标签 简单介绍][2]

 [1]: http://conkeyn.javaeye.com/blog/349258
 [2]: http://blog.csdn.net/chenjyuj/archive/2007/04/11/1561342.aspx