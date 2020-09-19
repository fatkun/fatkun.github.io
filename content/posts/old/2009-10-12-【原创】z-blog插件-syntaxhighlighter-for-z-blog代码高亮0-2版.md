---
title: 【原创】Z-blog插件-SyntaxHighlighter for Z-blog代码高亮0.2版
author: fatkun
type: post
date: 2009-10-13T02:27:45+00:00
url: /2009/10/【原创】z-blog插件-syntaxhighlighter-for-z-blog代码高亮0-2版.html
views:
  - 4
duoshuo_thread_id:
  - 6300408687882142465
categories:
  - 网页前端
tags:
  - SyntaxHighlighter
  - Z-Blog
  - 代码高亮
  - 插件

---
Z-blog里面的代码高亮插件(Highlight)已经是很久以前的了，作为一个写代码的人怎么可以没有代码高亮，让看代码的人舒服一点。现在是0.2版，可能还有很多问题。插件是把Highlight改的，改了来适应SyntaxHighlighter的使用，才用Z-BLOG差不多一个月，还没研究过怎么写插件，不过使用起来已经很好了。
<!--more-->

  
**SyntaxHighlighter**是一个很多人使用的代码高亮JS工具，项目地址是<a href="http://code.google.com/p/syntaxhighlighter/" target="_blank">http://code.google.com/p/syntaxhighlighter/</a>，本插件使用的是2.0版本。  
Z-blog里面的代码高亮插件(Highlight)已经是很久以前的了，作为一个写代码的人怎么可以没有代码高亮，让看代码的人舒服一点。现在是0.2版，一堆语言解析，好强大，可是做插件时累坏我，文件太多了可能还有问题。插件是把Highlight改的，改了来适应SyntaxHighlighter的使用，才用Z-BLOG差不多一个月，还没研究过怎么写插件。  
以前也写过<a href="http://blog.fatkun.com/view.asp?id=12" target="_blank">在Z-Blog上使用SyntaxHighlighter1.5（代码高亮，不复制行号）修改方法</a>，但是不是插件，修改起来麻烦，也不方便。  
**更新后记住要“文件重建”**  
<a href="http://blog.fatkun.com/SyntaxHighlighter.rar" target="_blank"><font size="4"><b>0.2版点击此下载</b></font></a>  
**更新信息**  
0.2 版  
+ 管理页面，能选择需要解析的语言。  
0.1 alpha版  
基础版本  
**当前已知的问题**
> 1，插件没有配置页面，所以把所有JS都加载（0.2版已解决）
**使用方法**  
**[<span />code=**这里填写语言，例如html、C#等**]**这里写代码**[/code]**  
**下面是代码演示**
<pre class="brush:html;">&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd"&gt;&lt;html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en"&gt;&lt;head&gt;	&lt;meta http-equiv="Content-Type" content="text/html; charset=UTF-8" /&gt;	&lt;title&gt;SyntaxHighlighter Build Test Page&lt;/title&gt;	&lt;script type="text/javascript" src="scripts/shCore.js"&gt;&lt;/script&gt;	&lt;script type="text/javascript" src="scripts/shBrushBash.js"&gt;&lt;/script&gt;	&lt;script type="text/javascript" src="scripts/shBrushCpp.js"&gt;&lt;/script&gt;	&lt;script type="text/javascript" src="scripts/shBrushCSharp.js"&gt;&lt;/script&gt;	&lt;script type="text/javascript" src="scripts/shBrushCss.js"&gt;&lt;/script&gt;	&lt;script type="text/javascript" src="scripts/shBrushDelphi.js"&gt;&lt;/script&gt;	&lt;script type="text/javascript" src="scripts/shBrushDiff.js"&gt;&lt;/script&gt;	&lt;script type="text/javascript" src="scripts/shBrushGroovy.js"&gt;&lt;/script&gt;	&lt;script type="text/javascript" src="scripts/shBrushJava.js"&gt;&lt;/script&gt;	&lt;script type="text/javascript" src="scripts/shBrushJScript.js"&gt;&lt;/script&gt;	&lt;script type="text/javascript" src="scripts/shBrushPhp.js"&gt;&lt;/script&gt;	&lt;script type="text/javascript" src="scripts/shBrushPlain.js"&gt;&lt;/script&gt;	&lt;script type="text/javascript" src="scripts/shBrushPython.js"&gt;&lt;/script&gt;	&lt;script type="text/javascript" src="scripts/shBrushRuby.js"&gt;&lt;/script&gt;	&lt;script type="text/javascript" src="scripts/shBrushScala.js"&gt;&lt;/script&gt;	&lt;script type="text/javascript" src="scripts/shBrushSql.js"&gt;&lt;/script&gt;	&lt;script type="text/javascript" src="scripts/shBrushVb.js"&gt;&lt;/script&gt;	&lt;script type="text/javascript" src="scripts/shBrushXml.js"&gt;&lt;/script&gt;	&lt;link type="text/css" rel="stylesheet" href="styles/shCore.css"/&gt;	&lt;link type="text/css" rel="stylesheet" href="styles/shThemeDefault.css"/&gt;	&lt;script type="text/javascript"&gt;		SyntaxHighlighter.config.clipboardSwf = 'scripts/clipboard.swf';		SyntaxHighlighter.all();	&lt;/script&gt;&lt;/head&gt;&lt;body &gt;&lt;h1&gt;SyntaxHihglighter Test&lt;/h1&gt;&lt;p&gt;This is a test file to insure that everything is working well.&lt;/p&gt;&lt;pre class="brush: c-sharp;"&gt;function test() : String{	return 10;}&lt;/pre&gt;&lt;/html&gt;</pre>