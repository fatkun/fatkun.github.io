---
title: 在Z-Blog上使用SyntaxHighlighter1.5（代码高亮，不复制行号）修改方法
author: fatkun
type: post
date: 2009-09-20T04:44:52+00:00
url: /2009/09/在z-blog上使用syntaxhighlighter1-5（代码高亮，不复制行号）修改方.html
views:
  - 6
duoshuo_thread_id:
  - 6300408667980169985
categories:
  - 网页前端
tags:
  - SyntaxHighlighter
  - Z-Blog
  - 代码高亮

---
这里我是使用了SyntaxHighlighter1.51版本来修改的，到目前为止已经有SyntaxHighlighter2.0版本了。可以到这里下载：http://code.google.com/p/syntaxhighlighter/  
至于选择1.5版本修改的其中一个原因是1.5版本前面的行号是用CSS实现的，直接复制代码时不会把前面的行号复制，这是我选择它的一个重要原因。
<!--more-->

  
有插件了，看看这里<a href="http://fatkun.com/post/2009/10/SyntaxHighlighter2_Z-blog.html" target="_blank">【原创】Z-blog插件-SyntaxHighlighter for Z-blog代码高亮</a>  
这里我是使用了SyntaxHighlighter1.51版本来修改的，到目前为止已经有SyntaxHighlighter2.0版本了。可以到这里下载：http://code.google.com/p/syntaxhighlighter/  
至于选择1.5版本修改的其中一个原因是1.5版本前面的行号是用CSS实现的，直接复制代码时不会把前面的行号复制，这是我选择它的一个重要原因。由于flash10不允许直接操作剪贴板，必须由用户激活falsh才能使用“复制按钮”，故1.5版使用复制的方法已经失效了。我参考了javaeye.com的修改方法，直接用一个flash为复制按钮（当然还有更好的方法，例如SyntaxHighlighter2.0已经实现了，还有我前面提到的<a href="http://blog.fatkun.com/view.asp?id=9" target="_blank">Zero Clipboard项目</a>）  
我修改的这个版本可以在Z-Blog很好的使用~在下面我会打包发上来~  
由于Z-Blog会把转行改为<BR>，所以我们要转换回来  
废话少说，贴部分主要代码  
在shCore.js找到下面这句代码
<pre class="brush:&quot;js&quot;;">this.originalCode=code;this.code=Chop(Unindent(code));</pre>
改为：(也就是说把<BR>给替换回转行了)
<pre class="brush:&quot;js&quot;;">code=code.replace(/&lt;BR&gt;/ig, "\n");this.originalCode=code;this.code=Chop(Unindent(code));</pre>
**上面是主要的修改方法，下面说使用方法**  
最后我喜欢把这些代码写在网站设置管理版权申明那里，比较方便修改，你也可以写在模板里（注意下面的路径根据具体目录更换，最好用绝对路径）
<pre class="brush:&quot;js&quot;;">&lt;link type="text/css" rel="stylesheet" href="/zb/highlight/SyntaxHighlighter.css"&gt;&lt;/link&gt;&lt;script language="javascript" src="/zb/highlight/shCore.js"&gt;&lt;/script&gt;&lt;script language="javascript" src="/zb/highlight/shBrushCSharp.js"&gt;&lt;/script&gt;&lt;script language="javascript" src="/zb/highlight/shBrushJScript.js"&gt;&lt;/script&gt;&lt;script language="javascript" src="/zb/highlight/shBrushSql.js"&gt;&lt;/script&gt;&lt;script language="javascript" src="/zb/highlight/shBrushJava.js"&gt;&lt;/script&gt;&lt;script language="javascript" src="/zb/highlight/shBrushXml.js"&gt;&lt;/script&gt;&lt;script language="javascript"&gt;window.onload = function () {dp.SyntaxHighlighter.ClipboardSwf = '/zb/highlight/clipboard_new.swf';dp.SyntaxHighlighter.ClipboardImg = '/zb/highlight/icon_copy.gif';dp.SyntaxHighlighter.HighlightAll();}&lt;/script&gt;</pre>
使用方法，在内容中加入：
<pre class="brush:&quot;xml&quot;;">&lt;pre class="这里写你代码所用的语言，如js,c#,java"&gt;这里贴代码！注意如果有&lt;BR&gt;记得要用转义（&amp;lt;）&lt;/pre&gt;</pre>
打包下载啦，猛击这里：<a href="http://fatkun.com/upload/2009/9/dp.SyntaxHighlighter-zblog@fatkun.rar" target="_blank">dp.SyntaxHighlighter-zblog@fatkun.rar</a>