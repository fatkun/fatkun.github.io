---
title: 用js+flash复制文本（支持flash10） – Zero Clipboard项目
author: fatkun
type: post
date: 2009-09-17T06:56:03+00:00
url: /2009/09/用jsflash复制文本（支持flash10）-zero-clipboard项目.html
views:
  - 30
duoshuo_thread_id:
  - 6300408667762066178
categories:
  - 电脑知识
tags:
  - Clipboard JS

---
web开发中常常要实现“复制到剪切板”功能。这个功能很实用，但是由于安全问题，浏览器的限制越来越严，实现的方法也越来越有限了。 Firefox 默认下不能直接通过Javascript操作剪切板，必须开启相关的设置才行。想只通过Javascript技术实现跨浏览器的剪切板是行不通的。现在常用的方法是利用JavaScript+Flash实现，普遍流传的办法是\_clipboard.swf，这是国外最早实现的（著名的Clipboard Copy解决方案:　http://www.jeffothy.com/weblog/clipboard-copy/）。但是很可惜，\_clipboard.swf在新出来的flash10中无效，因为flash10中规定了只有在swf上进行了实际的操作（比如鼠标点击）才能启动剪切板。而_clipboard.swf方法的swf是隐藏的，通过JavaScript来操作flash的剪切板，显然没有对swf进行实际的用户操作。  
&#8230;
<!--more-->

  
web开发中常常要实现“复制到剪切板”功能。这个功能很实用，但是由于安全问题，浏览器的限制越来越严，实现的方法也越来越有限了。 Firefox 默认下不能直接通过Javascript操作剪切板，必须开启相关的设置才行。想只通过Javascript技术实现跨浏览器的剪切板是行不通的。现在常用的方法是利用JavaScript+Flash实现，普遍流传的办法是\_clipboard.swf，这是国外最早实现的（著名的Clipboard Copy解决方案:　http://www.jeffothy.com/weblog/clipboard-copy/）。但是很可惜，\_clipboard.swf在新出来的flash10中无效，因为flash10中规定了只有在swf上进行了实际的操作（比如鼠标点击）才能启动剪切板。而_clipboard.swf方法的swf是隐藏的，通过JavaScript来操作flash的剪切板，显然没有对swf进行实际的用户操作。  
针对这个，最近国外出现了一种新的方法，而且专门做了一个JavaScript库 Zero Clipboard ，它包含一个flash影片和一个JavaScript接口，这个flash是透明的（不是隐藏），用户不会察觉到它的存在。这个flash覆盖在一个 DOM元素上，比如button，div之类，当点击这个DOM时，你实际点击的是这个flash，这个作用在flash上的动作能够开启flash的剪切板。这实际上就是一种clickjacking。  
DEMO页面 : http://bowser.macminicolo.net/~jhuckaby/zeroclipboard/  
Zero Clipboard项目主页：　http://code.google.com/p/zeroclipboard/