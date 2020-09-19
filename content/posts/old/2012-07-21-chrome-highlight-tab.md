---
title: chrome扩展让指定标签作为当前浏览标签
author: fatkun
type: post
date: 2012-07-21T15:34:15+00:00
url: /2012/07/chrome-highlight-tab.html
duoshuo_thread_id:
  - 6300408865913570050
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:1222:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="html" style="font-family:monospace;">chrome.tabs.highlight(object highlightInfo, function callback)
    高亮突出指定标签页。
    参数
    highlightInfo ( object )
    windowId ( optional integer ) [从r136510开始该属性可选]
    包含标签页的窗口。
    tabs ( array of integer or integer )
    要高亮突出的一个或多个标签页索引。
    callback ( function )
    回调函数
    callback参数应该指定一个如下形式的函数：
    function(Window window) {...};
    window ( Window )
    高亮突出的标签页所在窗口的详情。</pre></td></tr></table><p class="theCode" style="display:none;">chrome.tabs.highlight(object highlightInfo, function callback)
    高亮突出指定标签页。
    参数
    highlightInfo ( object )
    windowId ( optional integer ) [从r136510开始该属性可选]
    包含标签页的窗口。
    tabs ( array of integer or integer )
    要高亮突出的一个或多个标签页索引。
    callback ( function )
    回调函数
    callback参数应该指定一个如下形式的函数：
    function(Window window) {...};
    window ( Window )
    高亮突出的标签页所在窗口的详情。</p></div>
    ";}
categories:
  - 网页前端
tags:
  - chrome
  - Chrome Extensions

---
Tab有一个active表示这个标签是否是激活的，但想要把某个tab变成激活怎么办呢？  
可以使用chrome.tabs.highlight，可以传入多个index，或者一个，第一个会变成激活状态。
<pre escaped="true" lang="html">chrome.tabs.highlight(object highlightInfo, function callback)
高亮突出指定标签页。
参数
highlightInfo ( object )
windowId ( optional integer ) [从r136510开始该属性可选]
包含标签页的窗口。
tabs ( array of integer or integer )
要高亮突出的一个或多个标签页索引。
callback ( function )
回调函数
callback参数应该指定一个如下形式的函数：
function(Window window) {...};
window ( Window )
高亮突出的标签页所在窗口的详情。</pre>
中文api来源：https://sites.google.com/site/crxdoczh/devguide/browserinteraction/tabs