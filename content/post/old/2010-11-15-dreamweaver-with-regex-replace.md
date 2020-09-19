---
title: 在Dreamweaver使用正则表达式替换
author: fatkun
type: post
date: 2010-11-15T13:12:18+00:00
url: /2010/11/dreamweaver-with-regex-replace.html
duoshuo_thread_id:
  - 6300408776956576514
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:674:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="html" style="font-family:monospace;">&lt;body&gt;
    	&lt;td style=&quot; background:#ccc;&quot;&gt;&lt;/td&gt;
    	&lt;td class=&quot;td&quot; style=&quot; background:#ccc; color:#ccc;&quot;&gt;&lt;/td&gt;
    	&lt;td style=&quot; width:100%;&quot;&gt;&lt;/td&gt;
    &lt;/body&gt;</pre></td></tr></table><p class="theCode" style="display:none;">&lt;body&gt;
    	&lt;td style=&quot; background:#ccc;&quot;&gt;&lt;/td&gt;
    	&lt;td class=&quot;td&quot; style=&quot; background:#ccc; color:#ccc;&quot;&gt;&lt;/td&gt;
    	&lt;td style=&quot; width:100%;&quot;&gt;&lt;/td&gt;
    &lt;/body&gt;</p></div>
    ";}
categories:
  - 网页前端
tags:
  - Dreamweaver
  - regex
  - 替换
  - 正则表达式

---
有时我们需要比较复杂的替换文本，这时要用到正则表达式来进行替换。你可以使用其他可以使用正则表达式的替换工具，这里以Dreamweaver为例子。
## 应用场景

例如有个场景，这里有一段html
<pre escaped="true" lang="html">&lt;body&gt;
	&lt;td style=" background:#ccc;"&gt;&lt;/td&gt;
	&lt;td class="td" style=" background:#ccc; color:#ccc;"&gt;&lt;/td&gt;
	&lt;td style=" width:100%;"&gt;&lt;/td&gt;
&lt;/body&gt;</pre>
需要在style属性内加入一个值height:20px;  
（当然这个例子有点奇怪，暂时不过，我只是想说明要在某个属性加入某值）
## 实现方法

记得勾上“**使用正则表达式**”查找
在查找框输入**<td([\s\S]\*?)style=&#8221;([\s\S]\*?)&#8221;**
在替换框输入**<td$1style=&#8221;$2height:20px;&#8221;**
试试查找看看，能否正常匹配？如果能匹配，一个个替换\全部替换即可。
  1. 查找框中的()括号，和替换框中的$1，$2一一对应，表示引用括号匹配的内容
  2. [\s\S]*?表示任意字符，？问号是指匹配模式是非贪婪的，尽量少的匹配字符
更多的正则表达式内容你可以搜索一下，相信聪明的你很容易就能找到的！