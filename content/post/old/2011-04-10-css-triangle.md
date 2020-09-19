---
title: CSS实现的三角形
author: fatkun
type: post
date: 2011-04-10T07:23:49+00:00
url: /2011/04/css-triangle.html
duoshuo_thread_id:
  - 6300408803598795522
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:725:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="css" style="font-family:monospace;">&lt;div style<span style="color: #00AA00;">=</span><span style="color: #ff0000;">&quot;width:0; height:0; border:40px solid transparent;border-top-color:green;border-left-color:red;border-right-color:blue;border-bottom-color:yellow;&quot;</span><span style="color: #00AA00;">&gt;</span>&lt;/div<span style="color: #00AA00;">&gt;</span></pre></td></tr></table><p class="theCode" style="display:none;">&lt;div style=&quot;width:0; height:0; border:40px solid transparent;border-top-color:green;border-left-color:red;border-right-color:blue;border-bottom-color:yellow;&quot;&gt;&lt;/div&gt;</p></div>
    ";i:2;s:5678:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="css" style="font-family:monospace;">&lt;style type<span style="color: #00AA00;">=</span><span style="color: #ff0000;">&quot;text/css&quot;</span><span style="color: #00AA00;">&gt;</span>
    <span style="color: #6666ff;">.triangle_contianer</span><span style="color: #00AA00;">&#123;</span> <span style="color: #000000; font-weight: bold;">position</span><span style="color: #00AA00;">:</span><span style="color: #993333;">relative</span><span style="color: #00AA00;">;</span> <span style="color: #000000; font-weight: bold;">background</span><span style="color: #00AA00;">:</span><span style="color: #cc00cc;">#FFE4CA</span><span style="color: #00AA00;">;</span> <span style="color: #000000; font-weight: bold;">color</span><span style="color: #00AA00;">:</span><span style="color: #cc00cc;">#000</span><span style="color: #00AA00;">;</span> <span style="color: #000000; font-weight: bold;">border</span><span style="color: #00AA00;">:</span><span style="color: #933;">4px</span> <span style="color: #993333;">solid</span> <span style="color: #cc00cc;">#F90</span><span style="color: #00AA00;">;</span> <span style="color: #000000; font-weight: bold;">padding</span><span style="color: #00AA00;">:</span><span style="color: #933;">5px</span><span style="color: #00AA00;">;</span><span style="color: #00AA00;">&#125;</span>
    <span style="color: #6666ff;">.triangle_border</span><span style="color: #00AA00;">&#123;</span> <span style="color: #000000; font-weight: bold;">width</span><span style="color: #00AA00;">:</span><span style="color: #cc66cc;">0</span><span style="color: #00AA00;">;</span> <span style="color: #000000; font-weight: bold;">position</span><span style="color: #00AA00;">:</span><span style="color: #993333;">absolute</span><span style="color: #00AA00;">;</span> <span style="color: #000000; font-weight: bold;">left</span><span style="color: #00AA00;">:</span><span style="color: #933;">50%</span><span style="color: #00AA00;">;</span><span style="color: #000000; font-weight: bold;">bottom</span><span style="color: #00AA00;">:</span><span style="color: #933;">-24px</span><span style="color: #00AA00;">;</span> <span style="color: #000000; font-weight: bold;">margin-left</span><span style="color: #00AA00;">:</span><span style="color: #933;">-12px</span><span style="color: #00AA00;">;</span> <span style="color: #000000; font-weight: bold;">border</span><span style="color: #00AA00;">:</span><span style="color: #933;">12px</span> <span style="color: #993333;">solid</span> <span style="color: #dc143c;">transparent</span><span style="color: #00AA00;">;</span><span style="color: #000000; font-weight: bold;">border-top-color</span><span style="color: #00AA00;">:</span><span style="color: #cc00cc;">#F90</span><span style="color: #00AA00;">;</span><span style="color: #00AA00;">&#125;</span>
    <span style="color: #6666ff;">.triangle</span><span style="color: #00AA00;">&#123;</span> <span style="color: #000000; font-weight: bold;">position</span><span style="color: #00AA00;">:</span><span style="color: #993333;">absolute</span><span style="color: #00AA00;">;</span> <span style="color: #000000; font-weight: bold;">left</span><span style="color: #00AA00;">:</span><span style="color: #933;">50%</span><span style="color: #00AA00;">;</span><span style="color: #000000; font-weight: bold;">bottom</span><span style="color: #00AA00;">:</span><span style="color: #933;">-12px</span><span style="color: #00AA00;">;</span> <span style="color: #000000; font-weight: bold;">margin-left</span><span style="color: #00AA00;">:</span><span style="color: #933;">-6px</span><span style="color: #00AA00;">;</span> <span style="color: #000000; font-weight: bold;">border</span><span style="color: #00AA00;">:</span><span style="color: #933;">6px</span> <span style="color: #993333;">solid</span> <span style="color: #dc143c;">transparent</span><span style="color: #00AA00;">;</span><span style="color: #000000; font-weight: bold;">border-top-color</span><span style="color: #00AA00;">:</span><span style="color: #cc00cc;">#FFE4CA</span><span style="color: #00AA00;">;</span><span style="color: #00AA00;">&#125;</span>
    &lt;/style<span style="color: #00AA00;">&gt;</span>
    &lt;span class<span style="color: #00AA00;">=</span><span style="color: #ff0000;">&quot;triangle_contianer&quot;</span><span style="color: #00AA00;">&gt;</span>
    Fatkun<span style="color: #00AA00;">,</span>这是提示的内容啊&lt;span class<span style="color: #00AA00;">=</span><span style="color: #ff0000;">&quot;triangle_border&quot;</span><span style="color: #00AA00;">&gt;</span>&lt;/span<span style="color: #00AA00;">&gt;</span>&lt;span class<span style="color: #00AA00;">=</span><span style="color: #ff0000;">&quot;triangle&quot;</span><span style="color: #00AA00;">&gt;</span>&lt;/span<span style="color: #00AA00;">&gt;</span>
    &lt;/span<span style="color: #00AA00;">&gt;</span></pre></td></tr></table><p class="theCode" style="display:none;">&lt;style type=&quot;text/css&quot;&gt;
    .triangle_contianer{ position:relative; background:#FFE4CA; color:#000; border:4px solid #F90; padding:5px;}
    .triangle_border{ width:0; position:absolute; left:50%;bottom:-24px; margin-left:-12px; border:12px solid transparent;border-top-color:#F90;}
    .triangle{ position:absolute; left:50%;bottom:-12px; margin-left:-6px; border:6px solid transparent;border-top-color:#FFE4CA;}
    &lt;/style&gt;
    &lt;span class=&quot;triangle_contianer&quot;&gt;
    Fatkun,这是提示的内容啊&lt;span class=&quot;triangle_border&quot;&gt;&lt;/span&gt;&lt;span class=&quot;triangle&quot;&gt;&lt;/span&gt;
    &lt;/span&gt;</p></div>
    ";}
categories:
  - 网页前端
tags:
  - css
  - 三角形

---
[<img class="alignnone size-full wp-image-878" title="triangle" src="http://fatkun.com/wp-content/uploads/2011/04/triangle.png" alt="" width="209" height="146" />][1]
看着喜欢，就试着自己做一个了。
## 原理

主要是利用border来实现。
看上图的的正方形的代码
<pre escaped="true" lang="css">&lt;div style="width:0; height:0; border:40px solid transparent;border-top-color:green;border-left-color:red;border-right-color:blue;border-bottom-color:yellow;"&gt;&lt;/div&gt;</pre>
分别给四边的border设了四种颜色。也许你看到这里就知道了，取一部分不就是三角形了嘛。没错，把其他三边设为透明即可。
<pre escaped="true" lang="css">&lt;style type="text/css"&gt;
.triangle_contianer{ position:relative; background:#FFE4CA; color:#000; border:4px solid #F90; padding:5px;}
.triangle_border{ width:0; position:absolute; left:50%;bottom:-24px; margin-left:-12px; border:12px solid transparent;border-top-color:#F90;}
.triangle{ position:absolute; left:50%;bottom:-12px; margin-left:-6px; border:6px solid transparent;border-top-color:#FFE4CA;}
&lt;/style&gt;
&lt;span class="triangle_contianer"&gt;
Fatkun,这是提示的内容啊&lt;span class="triangle_border"&gt;&lt;/span&gt;&lt;span class="triangle"&gt;&lt;/span&gt;
&lt;/span&gt;</pre>
其实这里用了一个span假装作为了三角形边框(triangle_border)，其实也是一个三角形border。
另外里面的边框宽度改变的话，还要相应的改变margin-left等一些值。

 [1]: http://fatkun.com/wp-content/uploads/2011/04/triangle.png