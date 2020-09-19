---
title: CSS圆角框+Jquery圆角框
author: fatkun
type: post
date: 2009-12-11T12:30:32+00:00
excerpt: 刚在群上看到一个CSS/CSS+JS的圆角框，所以发上来了~平时做网页的时候很多时候都想要做成圆角的~~一般的做法...
url: /2009/12/css-corner-and-jquery-corner.html
views:
  - 16
duoshuo_thread_id:
  - 6300408700653798146
categories:
  - 网页前端
tags:
  - css
  - CSS圆角框
  - jquery

---
刚在群上看到一个CSS/CSS+JS的圆角框，所以发上来了~平时做网页的时候很多时候都想要做成圆角的~~一般的做法都是做一个圆角的图片~然后上中下三个div类似~但是这样做一般只对固定宽度的有效~不固定宽度的就有点烦了。  
现在用JS来实现吧。这个JS可以对图片进行圆角~<!--more-->

## CSS圆角框组件

**原创：**<a href="http://binyong.cnblogs.com/" target="_blank"><span style="COLOR: black; TEXT-DECORATION: none; text-underline: none"><span><strong>冰极峰</strong></span></span></a>
下载和Demo地址：[CSS圆角框组件 V1.0][1]{#ctl04_TitleUrl}
<img class="alignnone" title="css" src="http://farm3.static.flickr.com/2720/4175810337_5c3b73591e_o.jpg" alt="" width="511" height="707" /> 
作者也说了它的优缺点~
> 缺点：
> 对于这种用纯CSS来实现的圆角框，不得不说说它的缺陷。
> 1. 语义化不够好，因为其圆角全部由HTML结构标签堆砌而成，而这些标签在字面上讲没有任何的含义，全是为了样式的表现而存在的，所以造成HTML代码无端增多，不利于SEO优化。这也是大家所诟病的地方，也是广大前端工程师不喜欢它的最大原因。
> 2. 样式的定义比较复杂，可操作性繁琐，如果没有弄懂原理，会觉得特麻烦。
> 3. 边线框宽度只适用于较小的值，无法定义线框的大小，因为一超过1px的宽度值，就会产生比较直观的锯齿。
> 4. 圆角不能调节大小，如果要模拟更圆滑的效果，就需要添加更多的容器，造成结构更加复杂。
> 5. 不太适合对图形要求比较高的场合，因为它不够圆滑，如果将它放大会看到一些锯齿。
> 优点：
> 说了这么多缺点，也要来说说它的优点：
> 1. 兼容性好，这种圆角框通用于全部的浏览器，不存在兼容性问题。
> 2. 弹性自适应宽度高度的大小变化，特别适用于流体布局的页面中使用。
> 3. 可自定义边框和背景色，随心所欲地改变风格。
> 4. 不需要制作圆角图片，节约网络流量，并且也可以减少或降低设计人员的工作量，减少前端人员布局定位的兼容性工作。
> 扩展性：
> 如果将它的不足尽最大化地减弱，那么这将是一种不错的效果，我想这些工作就需要JS来参与了，而这样的话已超出本文标题的范围了。并且这种JS的圆角框已经有了比较成熟的作品了。
## Jquery.corner.js

我以前用过这个插件，感觉还是可以的（可是不知道我上次用的时候在IE6下，圆角框的border消失了。不知道是不是bug)。这个插件非常容易使用~~就算不熟悉Jquery也没关系~~有很多效果~
jquery.corner的DEMO可以在这里看：<http://malsup.com/jquery/corner/>
下载地址也在这：<http://malsup.com/jquery/corner/>  
预览图：  
![][2]

 [1]: http://www.cnblogs.com/binyong/archive/2009/12/11/1621484.html
 [2]: http://farm3.static.flickr.com/2633/4175810341_91f156b21b_o.jpg