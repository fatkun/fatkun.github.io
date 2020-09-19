---
title: CSS中的部分缩写
author: fatkun
type: post
date: 2010-09-22T03:21:23+00:00
url: /2010/09/css-shortcut.html
duoshuo_thread_id:
  - 6300408770367324929
wp-syntax-cache-content:
  - |
    a:7:{i:1;s:2500:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="css" style="font-family:monospace;"><span style="color: #808080; font-style: italic;">/*按“上右下左”顺时针的方向填写*/</span>
    <span style="color: #000000; font-weight: bold;">margin</span><span style="color: #00AA00;">:</span><span style="color: #933;">1px</span> <span style="color: #933;">1px</span> <span style="color: #933;">1px</span> <span style="color: #933;">1px</span><span style="color: #00AA00;">;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">margin</span><span style="color: #00AA00;">:</span><span style="color: #933;">1px</span><span style="color: #00AA00;">;</span><span style="color: #808080; font-style: italic;">/*四个方向的边距相同，等同于margin:1px 1px 1px 1px;*/</span>
    <span style="color: #000000; font-weight: bold;">margin</span><span style="color: #00AA00;">:</span><span style="color: #933;">1px</span> <span style="color: #933;">2px</span><span style="color: #00AA00;">;</span><span style="color: #808080; font-style: italic;">/*上下边距都为1px，左右边距均为2px，等同于margin:1px 2px 1px 2px*/</span>
    <span style="color: #000000; font-weight: bold;">margin</span><span style="color: #00AA00;">:</span><span style="color: #933;">1px</span> <span style="color: #933;">2px</span> <span style="color: #933;">3px</span><span style="color: #00AA00;">;</span><span style="color: #808080; font-style: italic;">/*右边距和左边距相同，等同于margin:1px 2px 3px 2px;*/</span>
    <span style="color: #000000; font-weight: bold;">margin</span><span style="color: #00AA00;">:</span><span style="color: #933;">1px</span> <span style="color: #933;">2px</span> <span style="color: #933;">1px</span> <span style="color: #933;">3px</span><span style="color: #00AA00;">;</span><span style="color: #808080; font-style: italic;">/*注意，这里虽然上下边距都为1px，但是这里不能缩写。*/</span></pre></td></tr></table><p class="theCode" style="display:none;">/*按“上右下左”顺时针的方向填写*/
    margin:1px 1px 1px 1px;
    
    margin:1px;/*四个方向的边距相同，等同于margin:1px 1px 1px 1px;*/
    margin:1px 2px;/*上下边距都为1px，左右边距均为2px，等同于margin:1px 2px 1px 2px*/
    margin:1px 2px 3px;/*右边距和左边距相同，等同于margin:1px 2px 3px 2px;*/
    margin:1px 2px 1px 3px;/*注意，这里虽然上下边距都为1px，但是这里不能缩写。*/</p></div>
    ";i:2;s:755:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="css" style="font-family:monospace;"><span style="color: #808080; font-style: italic;">/*宽度  样式  样色*/</span>
    <span style="color: #000000; font-weight: bold;">border</span><span style="color: #00AA00;">:</span><span style="color: #933;">5px</span> <span style="color: #993333;">solid</span> <span style="color: #cc00cc;">#369</span><span style="color: #00AA00;">;</span>
    <span style="color: #808080; font-style: italic;">/*border的缩写中border-style是必须的。*/</span></pre></td></tr></table><p class="theCode" style="display:none;">/*宽度  样式  样色*/
    border:5px solid #369;
    /*border的缩写中border-style是必须的。*/</p></div>
    ";i:3;s:2297:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="css" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">background-color</span><span style="color: #00AA00;">:</span> color || <span style="color: #cc00cc;">#hex</span> || RGB<span style="color: #00AA00;">&#40;</span>% || <span style="color: #cc66cc;">0</span>-<span style="color: #cc66cc;">255</span><span style="color: #00AA00;">&#41;</span> || RGBa<span style="color: #00AA00;">;</span>
    <span style="color: #000000; font-weight: bold;">background-image</span><span style="color: #00AA00;">:</span><span style="color: #9932cc;">url</span><span style="color: #00AA00;">&#40;</span><span style="color: #00AA00;">&#41;</span><span style="color: #00AA00;">;</span>
    <span style="color: #000000; font-weight: bold;">background-repeat</span><span style="color: #00AA00;">:</span> <span style="color: #993333;">repeat</span> || <span style="color: #993333;">repeat-x</span> || <span style="color: #993333;">repeat-y</span> || <span style="color: #993333;">no-repeat</span><span style="color: #00AA00;">;</span>
    <span style="color: #000000; font-weight: bold;">background-attachment</span><span style="color: #00AA00;">:</span> <span style="color: #993333;">scroll</span> || <span style="color: #993333;">fixed</span><span style="color: #00AA00;">;</span>
    <span style="color: #000000; font-weight: bold;">background-position</span><span style="color: #00AA00;">:</span> X Y || <span style="color: #00AA00;">&#40;</span><span style="color: #993333;">top</span>||<span style="color: #993333;">bottom</span>||<span style="color: #993333;">center</span><span style="color: #00AA00;">&#41;</span> <span style="color: #00AA00;">&#40;</span><span style="color: #993333;">left</span>||<span style="color: #993333;">right</span>||<span style="color: #993333;">center</span><span style="color: #00AA00;">&#41;</span><span style="color: #00AA00;">;</span></pre></td></tr></table><p class="theCode" style="display:none;">background-color: color || #hex || RGB(% || 0-255) || RGBa;
    background-image:url();
    background-repeat: repeat || repeat-x || repeat-y || no-repeat;
    background-attachment: scroll || fixed;
    background-position: X Y || (top||bottom||center) (left||right||center);</p></div>
    ";i:4;s:1543:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="css" style="font-family:monospace;"><span style="color: #808080; font-style: italic;">/*按照上面的顺序写即可，各个属性都可以省略*/</span>
    <span style="color: #000000; font-weight: bold;">background</span><span style="color: #00AA00;">:</span><span style="color: #cc00cc;">#ccc</span> <span style="color: #9932cc;">url</span><span style="color: #00AA00;">&#40;</span><span style="color: #ff0000;">&quot;xxx.png&quot;</span><span style="color: #00AA00;">&#41;</span> <span style="color: #993333;">repeat</span> <span style="color: #993333;">scroll</span> <span style="color: #993333;">top</span> <span style="color: #993333;">left</span> <span style="color: #00AA00;">;</span>
    <span style="color: #808080; font-style: italic;">/*默认值是*/</span>
    <span style="color: #000000; font-weight: bold;">background</span><span style="color: #00AA00;">:</span><span style="color: #dc143c;">transparent</span> <span style="color: #993333;">none</span> <span style="color: #993333;">repeat</span> <span style="color: #993333;">scroll</span> <span style="color: #993333;">top</span> <span style="color: #993333;">left</span> <span style="color: #00AA00;">;</span></pre></td></tr></table><p class="theCode" style="display:none;">/*按照上面的顺序写即可，各个属性都可以省略*/
    background:#ccc url(&quot;xxx.png&quot;) repeat scroll top left ;
    /*默认值是*/
    background:transparent none repeat scroll top left ;</p></div>
    ";i:5;s:2524:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="css" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">font-style</span><span style="color: #00AA00;">:</span> <span style="color: #993333;">normal</span> || <span style="color: #993333;">italic</span> || <span style="color: #993333;">oblique</span><span style="color: #00AA00;">;</span>
    <span style="color: #000000; font-weight: bold;">font-variant</span><span style="color: #00AA00;">:</span><span style="color: #993333;">normal</span> || <span style="color: #993333;">small-caps</span><span style="color: #00AA00;">;</span>
    <span style="color: #000000; font-weight: bold;">font-weight</span><span style="color: #00AA00;">:</span> <span style="color: #993333;">normal</span> || <span style="color: #993333;">bold</span> || <span style="color: #993333;">bolder</span> || || <span style="color: #993333;">lighter</span> || <span style="color: #00AA00;">&#40;</span><span style="color: #cc66cc;">100</span>-<span style="color: #cc66cc;">900</span><span style="color: #00AA00;">&#41;</span><span style="color: #00AA00;">;</span>
    <span style="color: #000000; font-weight: bold;">font-size</span><span style="color: #00AA00;">:</span> <span style="color: #00AA00;">&#40;</span>number<span style="color: #00AA00;">+</span>unit<span style="color: #00AA00;">&#41;</span> || <span style="color: #00AA00;">&#40;</span><span style="color: #993333;">xx-small</span> - <span style="color: #993333;">xx-large</span><span style="color: #00AA00;">&#41;</span><span style="color: #00AA00;">;</span>
    <span style="color: #000000; font-weight: bold;">line-height</span><span style="color: #00AA00;">:</span> <span style="color: #993333;">normal</span> || <span style="color: #00AA00;">&#40;</span>number<span style="color: #00AA00;">+</span>unit<span style="color: #00AA00;">&#41;</span><span style="color: #00AA00;">;</span>
    <span style="color: #000000; font-weight: bold;">font-family</span><span style="color: #00AA00;">:</span>name<span style="color: #00AA00;">,</span><span style="color: #ff0000;">&quot;more names&quot;</span><span style="color: #00AA00;">;</span></pre></td></tr></table><p class="theCode" style="display:none;">font-style: normal || italic || oblique;
    font-variant:normal || small-caps;
    font-weight: normal || bold || bolder || || lighter || (100-900);
    font-size: (number+unit) || (xx-small - xx-large);
    line-height: normal || (number+unit);
    font-family:name,&quot;more names&quot;;</p></div>
    ";i:6;s:1125:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="css" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">list-style</span><span style="color: #00AA00;">:</span><span style="color: #993333;">disc</span> <span style="color: #993333;">outside</span> <span style="color: #993333;">none</span>
    <span style="color: #808080; font-style: italic;">/*如果list-tyle中定义了图片，那么图片的优先级要比list-style-type高*/</span>
    <span style="color: #000000; font-weight: bold;">list-style</span><span style="color: #00AA00;">:</span><span style="color: #993333;">circle</span> <span style="color: #993333;">inside</span> <span style="color: #9932cc;">url</span><span style="color: #00AA00;">&#40;</span><span style="color: #ff0000; font-style: italic;">../img.gif</span><span style="color: #00AA00;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">list-style:disc outside none
    /*如果list-tyle中定义了图片，那么图片的优先级要比list-style-type高*/
    list-style:circle inside url(../img.gif)</p></div>
    ";i:7;s:881:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="css" style="font-family:monospace;"><span style="color: #808080; font-style: italic;">/*按 左上 右上 右下 左下 顺时针方向*/</span>
    <span style="color: #000000; font-weight: bold;">border-radius</span><span style="color: #00AA00;">:</span><span style="color: #933;">10px</span> <span style="color: #933;">20px</span> <span style="color: #933;">30px</span> <span style="color: #933;">40px</span><span style="color: #00AA00;">;</span>
    <span style="color: #808080; font-style: italic;">/*大致与边距的缩写相同，也可以省略某个值*/</span></pre></td></tr></table><p class="theCode" style="display:none;">/*按 左上 右上 右下 左下 顺时针方向*/
    border-radius:10px 20px 30px 40px;
    /*大致与边距的缩写相同，也可以省略某个值*/</p></div>
    ";}
categories:
  - 网页前端
tags:
  - css简写
  - css缩写

---
对于想学习好CSS的话，缩写的顺序必须是正确的（虽然有些不正确的浏览器能自动修正），既能看懂别人的缩写，也能省点敲键盘的时间~~
## 边距（margin与padding）

margin和padding的缩写方法相同
<pre escaped="true" lang="css">/*按“上右下左”顺时针的方向填写*/
margin:1px 1px 1px 1px;

margin:1px;/*四个方向的边距相同，等同于margin:1px 1px 1px 1px;*/
margin:1px 2px;/*上下边距都为1px，左右边距均为2px，等同于margin:1px 2px 1px 2px*/
margin:1px 2px 3px;/*右边距和左边距相同，等同于margin:1px 2px 3px 2px;*/
margin:1px 2px 1px 3px;/*注意，这里虽然上下边距都为1px，但是这里不能缩写。*/</pre>
## 边框(border与outline)

<pre escaped="true" lang="css">/*宽度  样式  样色*/
border:5px solid #369;
/*border的缩写中border-style是必须的。*/</pre>
## 背景(background)

background是最常用的简写之一，它包含以下属性：
<pre escaped="true" lang="css">background-color: color || #hex || RGB(% || 0-255) || RGBa;
background-image:url();
background-repeat: repeat || repeat-x || repeat-y || no-repeat;
background-attachment: scroll || fixed;
background-position: X Y || (top||bottom||center) (left||right||center);</pre>
<pre escaped="true" lang="css">/*按照上面的顺序写即可，各个属性都可以省略*/
background:#ccc url("xxx.png") repeat scroll top left ;
/*默认值是*/
background:transparent none repeat scroll top left ;</pre>
## 字体（font）

**很多人并不赞成使用font缩写**  
包含的属性有
<pre escaped="true" lang="css">font-style: normal || italic || oblique;
font-variant:normal || small-caps;
font-weight: normal || bold || bolder || || lighter || (100-900);
font-size: (number+unit) || (xx-small - xx-large);
line-height: normal || (number+unit);
font-family:name,"more names";</pre>
<img src="http://www.woaicss.com/attachments/month_1007/w201077162243.jpg" alt="" width="500" height="360" /> 
## 列表样式

<pre escaped="true" lang="css">list-style:disc outside none
/*如果list-tyle中定义了图片，那么图片的优先级要比list-style-type高*/
list-style:circle inside url(../img.gif)</pre>
## 圆角（border-radius）

<pre escaped="true" lang="css">/*按 左上 右上 右下 左下 顺时针方向*/
border-radius:10px 20px 30px 40px;
/*大致与边距的缩写相同，也可以省略某个值*/</pre>
文章来自<span style="font-weight: normal;"><a title="Permanent Link: CSS简写指南" rel="bookmark" href="http://www.qianduan.net/css-font-shorthand-attribute-handbook.html">CSS简写指南</a>，部分有删改，更多内容可以看原文</span>