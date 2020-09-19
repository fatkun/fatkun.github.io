---
title: HTML Canvas 鼠标画图
author: fatkun
type: post
date: 2011-02-20T07:32:27+00:00
url: /2011/02/html5-canvas-paint.html
duoshuo_thread_id:
  - 6300408802667660034
wp-syntax-cache-content:
  - |
    a:10:{i:1;s:426:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="html" style="font-family:monospace;">&lt;canvas id=&quot;canvasInAPerfectWorld&quot; width=&quot;490&quot; height=&quot;220&quot;&gt;&lt;/canvas&gt;</pre></td></tr></table><p class="theCode" style="display:none;">&lt;canvas id=&quot;canvasInAPerfectWorld&quot; width=&quot;490&quot; height=&quot;220&quot;&gt;&lt;/canvas&gt;</p></div>
    ";i:2;s:300:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="html" style="font-family:monospace;">&lt;div id=&quot;canvasDiv&quot;&gt;&lt;/div&gt;</pre></td></tr></table><p class="theCode" style="display:none;">&lt;div id=&quot;canvasDiv&quot;&gt;&lt;/div&gt;</p></div>
    ";i:3;s:374:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="js" style="font-family:monospace;">context = document.getElementById('canvasInAPerfectWorld').getContext(&quot;2d&quot;);</pre></td></tr></table><p class="theCode" style="display:none;">context = document.getElementById('canvasInAPerfectWorld').getContext(&quot;2d&quot;);</p></div>
    ";i:4;s:1012:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="js" style="font-family:monospace;">var canvasDiv = document.getElementById('canvasDiv');
    canvas = document.createElement('canvas');
    canvas.setAttribute('width', canvasWidth);
    canvas.setAttribute('height', canvasHeight);
    canvas.setAttribute('id', 'canvas');
    canvasDiv.appendChild(canvas);
    if(typeof G_vmlCanvasManager != 'undefined') {
    	canvas = G_vmlCanvasManager.initElement(canvas);
    }
    context = canvas.getContext(&quot;2d&quot;);</pre></td></tr></table><p class="theCode" style="display:none;">var canvasDiv = document.getElementById('canvasDiv');
    canvas = document.createElement('canvas');
    canvas.setAttribute('width', canvasWidth);
    canvas.setAttribute('height', canvasHeight);
    canvas.setAttribute('id', 'canvas');
    canvasDiv.appendChild(canvas);
    if(typeof G_vmlCanvasManager != 'undefined') {
    	canvas = G_vmlCanvasManager.initElement(canvas);
    }
    context = canvas.getContext(&quot;2d&quot;);</p></div>
    ";i:5;s:653:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="js" style="font-family:monospace;">$('#canvas').mousedown(function(e){
      var mouseX = e.pageX - this.offsetLeft;
      var mouseY = e.pageY - this.offsetTop;
    &nbsp;
      paint = true;
      addClick(e.pageX - this.offsetLeft, e.pageY - this.offsetTop);
      redraw();
    });</pre></td></tr></table><p class="theCode" style="display:none;">$('#canvas').mousedown(function(e){
      var mouseX = e.pageX - this.offsetLeft;
      var mouseY = e.pageY - this.offsetTop;
    
      paint = true;
      addClick(e.pageX - this.offsetLeft, e.pageY - this.offsetTop);
      redraw();
    });</p></div>
    ";i:6;s:550:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="js" style="font-family:monospace;">$('#canvas').mousemove(function(e){
      if(paint){//是不是按下了鼠标
        addClick(e.pageX - this.offsetLeft, e.pageY - this.offsetTop, true);
        redraw();
      }
    });</pre></td></tr></table><p class="theCode" style="display:none;">$('#canvas').mousemove(function(e){
      if(paint){//是不是按下了鼠标
        addClick(e.pageX - this.offsetLeft, e.pageY - this.offsetTop, true);
        redraw();
      }
    });</p></div>
    ";i:7;s:314:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="js" style="font-family:monospace;">$('#canvas').mouseup(function(e){
      paint = false;
    });</pre></td></tr></table><p class="theCode" style="display:none;">$('#canvas').mouseup(function(e){
      paint = false;
    });</p></div>
    ";i:8;s:320:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="js" style="font-family:monospace;">$('#canvas').mouseleave(function(e){
      paint = false;
    });</pre></td></tr></table><p class="theCode" style="display:none;">$('#canvas').mouseleave(function(e){
      paint = false;
    });</p></div>
    ";i:9;s:615:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="js" style="font-family:monospace;">var clickX = new Array();
    var clickY = new Array();
    var clickDrag = new Array();
    var paint;
    &nbsp;
    function addClick(x, y, dragging)
    {
      clickX.push(x);
      clickY.push(y);
      clickDrag.push(dragging);
    }</pre></td></tr></table><p class="theCode" style="display:none;">var clickX = new Array();
    var clickY = new Array();
    var clickDrag = new Array();
    var paint;
    
    function addClick(x, y, dragging)
    {
      clickX.push(x);
      clickY.push(y);
      clickDrag.push(dragging);
    }</p></div>
    ";i:10;s:1370:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="js" style="font-family:monospace;">function redraw(){
      canvas.width = canvas.width; // Clears the canvas
    &nbsp;
      context.strokeStyle = &quot;#df4b26&quot;;
      context.lineJoin = &quot;round&quot;;
      context.lineWidth = 5;
    &nbsp;
      for(var i=0; i &lt; clickX.length; i++)
      {
        context.beginPath();
        if(clickDrag[i] &amp;&amp; i){//当是拖动而且i!=0时，从上一个点开始画线。
          context.moveTo(clickX[i-1], clickY[i-1]);
         }else{
           context.moveTo(clickX[i]-1, clickY[i]);
         }
         context.lineTo(clickX[i], clickY[i]);
         context.closePath();
         context.stroke();
      }
    }</pre></td></tr></table><p class="theCode" style="display:none;">function redraw(){
      canvas.width = canvas.width; // Clears the canvas
    
      context.strokeStyle = &quot;#df4b26&quot;;
      context.lineJoin = &quot;round&quot;;
      context.lineWidth = 5;
    
      for(var i=0; i &lt; clickX.length; i++)
      {
        context.beginPath();
        if(clickDrag[i] &amp;&amp; i){//当是拖动而且i!=0时，从上一个点开始画线。
          context.moveTo(clickX[i-1], clickY[i-1]);
         }else{
           context.moveTo(clickX[i]-1, clickY[i]);
         }
         context.lineTo(clickX[i], clickY[i]);
         context.closePath();
         context.stroke();
      }
    }</p></div>
    ";}
categories:
  - 网页前端
tags:
  - canvas
  - html5
  - 手写
  - 画图

---
原文来自:<http://www.williammalone.com/articles/create-html5-canvas-javascript-drawing-app>(已被墙)
译文: <http://fatkun.com/2011/02/html5-canvas-paint.html>
我也不打算全部翻译了&#8230;大部分也看的懂,就算看不懂,代码也能看懂&#8230;.o(╯□╰)o原谅我非常懒&#8230;很久没写博客了.  
![][1] <!--more-->

&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-以下是一个简单的例子&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-
## html容器

首先，准备个容器,也就是画板了。
<pre escaped="true" lang="html">&lt;canvas id="canvasInAPerfectWorld" width="490" height="220"&gt;&lt;/canvas&gt;</pre>
但是，由于IE部分版本还是不支持HTML5，那我们可以借用exCanvas兼容IE..
<pre escaped="true" lang="html">&lt;div id="canvasDiv"&gt;&lt;/div&gt;</pre>
## 初始化js代码

如果你不管IE使用第一种方法
<pre escaped="true" lang="js">context = document.getElementById('canvasInAPerfectWorld').getContext("2d");</pre>
为了兼容IE，不得不使用下面这个方法，创建一个canvas，然后使用excanvas初始化。当然，为了IE兼容，你需要针对IE加上[exCanvas.js][2]
<pre escaped="true" lang="js">var canvasDiv = document.getElementById('canvasDiv');
canvas = document.createElement('canvas');
canvas.setAttribute('width', canvasWidth);
canvas.setAttribute('height', canvasHeight);
canvas.setAttribute('id', 'canvas');
canvasDiv.appendChild(canvas);
if(typeof G_vmlCanvasManager != 'undefined') {
	canvas = G_vmlCanvasManager.initElement(canvas);
}
context = canvas.getContext("2d");</pre>
## 开始一个简单的画板

在开始之前，说说怎么做先。它包含了四个鼠标事件和两个方法。addClick是为了记录鼠标的移动点，redraw是把记录的数据画出来。 (提一下，由于原作者使用了jquery，所以你也要把jquery引用进来。)
### 鼠标按下事件(Mouse Down Event)

当鼠标按下时，把paint设为true，表示正在画，鼠标没松开。把鼠标点记录下来。
<pre escaped="true" lang="js">$('#canvas').mousedown(function(e){
  var mouseX = e.pageX - this.offsetLeft;
  var mouseY = e.pageY - this.offsetTop;

  paint = true;
  addClick(e.pageX - this.offsetLeft, e.pageY - this.offsetTop);
  redraw();
});</pre>
### 鼠标移动事件(Mouse Move Event)

当按下鼠标的时候，鼠标移动就把点记录下来并画出来。
<pre escaped="true" lang="js">$('#canvas').mousemove(function(e){
  if(paint){//是不是按下了鼠标
    addClick(e.pageX - this.offsetLeft, e.pageY - this.offsetTop, true);
    redraw();
  }
});</pre>
### 鼠标松开事件(Mouse Up Event)

<pre escaped="true" lang="js">$('#canvas').mouseup(function(e){
  paint = false;
});</pre>
### 鼠标移开事件(Mouse Leave Event)

<pre escaped="true" lang="js">$('#canvas').mouseleave(function(e){
  paint = false;
});</pre>
### addClick方法

记录鼠标坐标点
<pre escaped="true" lang="js">var clickX = new Array();
var clickY = new Array();
var clickDrag = new Array();
var paint;

function addClick(x, y, dragging)
{
  clickX.push(x);
  clickY.push(y);
  clickDrag.push(dragging);
}</pre>
### redraw方法

目前这个redraw方法是每次都清空画板，然后重新把所有的点都画过，虽然效率不高，但是这样看起来还是挺简单的。
<pre escaped="true" lang="js">function redraw(){
  canvas.width = canvas.width; // Clears the canvas

  context.strokeStyle = "#df4b26";
  context.lineJoin = "round";
  context.lineWidth = 5;

  for(var i=0; i &lt; clickX.length; i++)
  {
    context.beginPath();
    if(clickDrag[i] && i){//当是拖动而且i!=0时，从上一个点开始画线。
      context.moveTo(clickX[i-1], clickY[i-1]);
     }else{
       context.moveTo(clickX[i]-1, clickY[i]);
     }
     context.lineTo(clickX[i], clickY[i]);
     context.closePath();
     context.stroke();
  }
}</pre>
## 最终效果

[点我看效果，赶紧点我][3]
## 最后

这上面的只是个简单的例子啦。。。原作者还在上面代码的基础上加了颜色，大小，橡皮擦等功能呢~~想看的翻墙去看作者博客吧。。这年头不会翻墙还真不好意思见人。

 [1]: http://wah88w.blu.livefilestore.com/y1pIqIdhuRNQzBo5xMVKTT97SV5E_bTIEr-ocWYMiE0iCXldxf0rIUXOiclvrtlhCChQc2zC9xFUClmwEgJS6t6NKiM_hE3flJ5/canvas.png?psid=1
 [2]: http://code.google.com/p/explorercanvas/
 [3]: http://fatkun.googlecode.com/hg/javascript/canvas.html