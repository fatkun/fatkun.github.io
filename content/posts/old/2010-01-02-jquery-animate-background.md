---
title: JQUERY实现背景图渐显（淡入淡出）
author: fatkun
type: post
date: 2010-01-01T16:31:29+00:00
url: /2010/01/jquery-animate-background.html
views:
  - 206
duoshuo_thread_id:
  - 6300408712376877825
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:465:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="line_numbers"><pre>1
    </pre></td><td class="code"><pre class="html" style="font-family:monospace;">&lt;a id=&quot;logo&quot; href=&quot;http://fatkun.com&quot;&gt;&lt;span&gt;fatkun.com&lt;/span&gt;&lt;/a&gt;</pre></td></tr></table><p class="theCode" style="display:none;">&lt;a id=&quot;logo&quot; href=&quot;http://fatkun.com&quot;&gt;&lt;span&gt;fatkun.com&lt;/span&gt;&lt;/a&gt;</p></div>
    ";i:2;s:4476:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="css" style="font-family:monospace;">	<span style="color: #cc00cc;">#logo</span><span style="color: #00AA00;">&#123;</span>
    		<span style="color: #000000; font-weight: bold;">margin</span><span style="color: #00AA00;">:</span><span style="color: #cc66cc;">0</span> <span style="color: #993333;">auto</span><span style="color: #00AA00;">;</span>
    		<span style="color: #000000; font-weight: bold;">position</span><span style="color: #00AA00;">:</span><span style="color: #993333;">relative</span><span style="color: #00AA00;">;</span><span style="color: #808080; font-style: italic;">/*相对定位,为了下面hover的绝对定位*/</span>
    		<span style="color: #000000; font-weight: bold;">background</span><span style="color: #00AA00;">:</span><span style="color: #9932cc;">url</span><span style="color: #00AA00;">&#40;</span><span style="color: #ff0000; font-style: italic;">fatkun.png</span><span style="color: #00AA00;">&#41;</span> <span style="color: #993333;">left</span> <span style="color: #993333;">top</span> <span style="color: #993333;">no-repeat</span><span style="color: #00AA00;">;</span><span style="color: #808080; font-style: italic;">/*设置背景图*/</span>
    		<span style="color: #000000; font-weight: bold;">width</span><span style="color: #00AA00;">:</span><span style="color: #933;">150px</span><span style="color: #00AA00;">;</span>
    		<span style="color: #000000; font-weight: bold;">height</span><span style="color: #00AA00;">:</span><span style="color: #933;">40px</span><span style="color: #00AA00;">;</span><span style="color: #808080; font-style: italic;">/*注意这里高度*/</span>
    		<span style="color: #000000; font-weight: bold;">display</span><span style="color: #00AA00;">:</span><span style="color: #993333;">block</span><span style="color: #00AA00;">;</span>
    		<span style="color: #000000; font-weight: bold;">text-indent</span><span style="color: #00AA00;">:</span><span style="color: #933;">-9999px</span><span style="color: #00AA00;">;</span>
    	<span style="color: #00AA00;">&#125;</span>
    	<span style="color: #cc00cc;">#logo</span> .hover<span style="color: #00AA00;">&#123;</span><span style="color: #808080; font-style: italic;">/*为JQ准备*/</span>
    		<span style="color: #000000; font-weight: bold;">background</span><span style="color: #00AA00;">:</span><span style="color: #9932cc;">url</span><span style="color: #00AA00;">&#40;</span><span style="color: #ff0000; font-style: italic;">fatkun.png</span><span style="color: #00AA00;">&#41;</span> <span style="color: #993333;">left</span> <span style="color: #993333;">bottom</span> <span style="color: #993333;">no-repeat</span><span style="color: #00AA00;">;</span><span style="color: #808080; font-style: italic;">/*background-position和上面不同*/</span>
    		<span style="color: #000000; font-weight: bold;">position</span><span style="color: #00AA00;">:</span><span style="color: #993333;">absolute</span><span style="color: #00AA00;">;</span><span style="color: #808080; font-style: italic;">/*为了使两张图片重叠在一起*/</span>
    		<span style="color: #000000; font-weight: bold;">top</span><span style="color: #00AA00;">:</span><span style="color: #cc66cc;">0</span><span style="color: #00AA00;">;</span>
    		<span style="color: #000000; font-weight: bold;">left</span><span style="color: #00AA00;">:</span><span style="color: #cc66cc;">0</span><span style="color: #00AA00;">;</span>
    		<span style="color: #000000; font-weight: bold;">height</span><span style="color: #00AA00;">:</span><span style="color: #933;">40px</span><span style="color: #00AA00;">;</span>
    		<span style="color: #000000; font-weight: bold;">width</span><span style="color: #00AA00;">:</span><span style="color: #933;">150px</span><span style="color: #00AA00;">;</span>
    	<span style="color: #00AA00;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">	#logo{
    		margin:0 auto;
    		position:relative;/*相对定位,为了下面hover的绝对定位*/
    		background:url(fatkun.png) left top no-repeat;/*设置背景图*/
    		width:150px;
    		height:40px;/*注意这里高度*/
    		display:block;
    		text-indent:-9999px;
    	}
    	#logo .hover{/*为JQ准备*/
    		background:url(fatkun.png) left bottom no-repeat;/*background-position和上面不同*/
    		position:absolute;/*为了使两张图片重叠在一起*/
    		top:0;
    		left:0;
    		height:40px;
    		width:150px;
    	}</p></div>
    ";i:3;s:1438:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="js" style="font-family:monospace;">   &lt;script type=&quot;text/javascript&quot; src=&quot;http://ajax.googleapis.com/ajax/libs/jquery/1/jquery.min.js&quot;&gt;&lt;/script&gt;
        &lt;script type=&quot;text/javascript&quot;&gt;
    		$(&quot;#logo&quot;).append(&quot;&lt;span class='hover'&gt;&lt;/span&gt;&quot;);//添加一个标签用来和灰图重叠起来
    		$(&quot;.hover&quot;).css('opacity', 0);//先不显示
        	$(&quot;.hover&quot;).parent().hover(
    		function(){
    			$(&quot;.hover&quot;).stop().animate({opacity: '1'},1000);
    		},
    		function(){
    			$(&quot;.hover&quot;).stop().animate({opacity: '0'},1000);
    		});
        &lt;/script&gt;</pre></td></tr></table><p class="theCode" style="display:none;">   &lt;script type=&quot;text/javascript&quot; src=&quot;http://ajax.googleapis.com/ajax/libs/jquery/1/jquery.min.js&quot;&gt;&lt;/script&gt;
        &lt;script type=&quot;text/javascript&quot;&gt;
    		$(&quot;#logo&quot;).append(&quot;&lt;span class='hover'&gt;&lt;/span&gt;&quot;);//添加一个标签用来和灰图重叠起来
    		$(&quot;.hover&quot;).css('opacity', 0);//先不显示
        	$(&quot;.hover&quot;).parent().hover(
    		function(){
    			$(&quot;.hover&quot;).stop().animate({opacity: '1'},1000);
    		},
    		function(){
    			$(&quot;.hover&quot;).stop().animate({opacity: '0'},1000);
    		});
        &lt;/script&gt;</p></div>
    ";}
categories:
  - jquery
tags:
  - jquery
  - jquery动画
  - 渐变

---
普通的CSS Hover最多就换一下背景图，不是很好看~我们利用jquery给它加上一些淡入的效果~
在<a href="http://leotheme.cn/javascript/jquery-dragoninteractive-navi.html" target="_blank">这里</a>看到这个例子，我想我还是自己练习一下吧·~效果可以看<http://dragoninteractive.com/>网站~，挺帅的~  
![][1] <!--more-->

## 实现原理

通过一个两张不同的图片，两个不同的层重叠在一起，顶层暂时透明，当鼠标移上去时，顶层由透明变成不透明，鼠标离开反之。
## 准备工作

用PS做一张图~如下图，注意记下高度是多少。我这张图的高度是两个40px的图
<img class="alignnone" src="http://farm5.static.flickr.com/4034/4233112590_85f70380b1.jpg" alt="" width="150" height="80" /> 
下面写代码  
 **html结构：**
<pre lang="html" line="1"><a id="logo" href="http://fatkun.com"><span>fatkun.com</span></a></pre>
**css代码：**
<pre lang="css">#logo{
		margin:0 auto;
		position:relative;/*相对定位,为了下面hover的绝对定位*/
		background:url(fatkun.png) left top no-repeat;/*设置背景图*/
		width:150px;
		height:40px;/*注意这里高度*/
		display:block;
		text-indent:-9999px;
	}
	#logo .hover{/*为JQ准备*/
		background:url(fatkun.png) left bottom no-repeat;/*background-position和上面不同*/
		position:absolute;/*为了使两张图片重叠在一起*/
		top:0;
		left:0;
		height:40px;
		width:150px;
	}</pre>
**最后最重要的JQuery代码出现了**
<pre lang="js"></pre>
我做的例子在这里：<http://fatkun.com/demo/jquery-animate-background/>
到学期末了~~考试就要来了~更新减缓·~2010，祝各位朋友新年快乐。

 [1]: http://farm3.static.flickr.com/2741/4232344401_a6bb0be121.jpg