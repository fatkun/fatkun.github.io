---
title: 在博客上显示QQ签名
author: fatkun
type: post
date: 2009-12-29T15:19:58+00:00
url: /2009/12/show-qq-signed-on-blog.html
views:
  - 20
duoshuo_thread_id:
  - 6300408707217883905
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:1581:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;script</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">&quot;text/javascript&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>var taotao_qq=12345678; var taotao_num=10;var taotao_type=0;<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/script<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;script</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">&quot;text/javascript&quot;</span> <span style="color: #000066;">charset</span>=<span style="color: #ff0000;">&quot;utf-8&quot;</span> <span style="color: #000066;">src</span>=<span style="color: #ff0000;">&quot;http://www.taotao.com/js/dkapi.js&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span><span style="color: #000000; font-weight: bold;">&lt;/script<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">&lt;script type=&quot;text/javascript&quot;&gt;var taotao_qq=12345678; var taotao_num=10;var taotao_type=0;&lt;/script&gt;
    &lt;script type=&quot;text/javascript&quot; charset=&quot;utf-8&quot; src=&quot;http://www.taotao.com/js/dkapi.js&quot;&gt;&lt;/script&gt;</p></div>
    ";i:2;s:1170:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;">doApi({&quot;posts&quot;:[{&quot;cn&quot;:&quot;人参要泡在杯具里才入味。有点感冒<span style="color: #ddbb00;">&amp;amp;</span>喉咙痛~没发热~~37.1° &quot;,&quot;id&quot;:&quot;14294845341&quot;,&quot;sr&quot;:3,&quot;time&quot;:&quot;3,1&quot;}],&quot;ret&quot;:0,&quot;total&quot;:203,&quot;type&quot;:0,&quot;ui&quot;:{&quot;lrank&quot;:0,&quot;name&quot;:&quot;QQ昵称&quot;,&quot;qq&quot;:你的QQ号,&quot;rank&quot;:0,&quot;rec&quot;:&quot;&quot;,&quot;usn&quot;:9948760}})</pre></td></tr></table><p class="theCode" style="display:none;">doApi({&quot;posts&quot;:[{&quot;cn&quot;:&quot;人参要泡在杯具里才入味。有点感冒&amp;amp;喉咙痛~没发热~~37.1° &quot;,&quot;id&quot;:&quot;14294845341&quot;,&quot;sr&quot;:3,&quot;time&quot;:&quot;3,1&quot;}],&quot;ret&quot;:0,&quot;total&quot;:203,&quot;type&quot;:0,&quot;ui&quot;:{&quot;lrank&quot;:0,&quot;name&quot;:&quot;QQ昵称&quot;,&quot;qq&quot;:你的QQ号,&quot;rank&quot;:0,&quot;rec&quot;:&quot;&quot;,&quot;usn&quot;:9948760}})</p></div>
    ";i:3;s:1221:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="js" style="font-family:monospace;">&lt;div id=&quot;taotao&quot;&gt;&lt;/div&gt;
    &nbsp;
    &lt;script type=&quot;text/javascript&quot;&gt;
    function doApi(obj) {
    	var taotao = document.getElementById(&quot;taotao&quot;);
        if (obj.ret != 0) {
            taotao.innerHTML = &quot;看,有灰机...QQ签名加载失败鸟&quot;;
            return;
        }
    	taotao.innerHTML = obj.posts[0].cn;
    }
    &lt;/script&gt;
    &lt;script type=&quot;text/javascript&quot; src=&quot;http://www.taotao.com/cgi-bin/msgj?qq=你的QQ号&amp;num=1&quot;&gt;&lt;/script&gt;</pre></td></tr></table><p class="theCode" style="display:none;">&lt;div id=&quot;taotao&quot;&gt;&lt;/div&gt;
    
    &lt;script type=&quot;text/javascript&quot;&gt;
    function doApi(obj) {
    	var taotao = document.getElementById(&quot;taotao&quot;);
        if (obj.ret != 0) {
            taotao.innerHTML = &quot;看,有灰机...QQ签名加载失败鸟&quot;;
            return;
        }
    	taotao.innerHTML = obj.posts[0].cn;
    }
    &lt;/script&gt;
    &lt;script type=&quot;text/javascript&quot; src=&quot;http://www.taotao.com/cgi-bin/msgj?qq=你的QQ号&amp;num=1&quot;&gt;&lt;/script&gt;</p></div>
    ";}
categories:
  - 网页前端
tags:
  - QQ
  - qq签名
  - 博客
  - 显示qq签名
  - 滔滔

---
先看看效果~~也可以在上面看到~~那就是QQ签名了。  
![][1]  
QQ签名哪里来呢·嘿嘿，我们可以利用taotao.com来取到我们的QQ签名，当然，需要你设置把签名保存在滔滔里，不然只能获取到滔滔的信息了。  
<!--more-->

  
大猫曾写过 [在Blog上显示QQ签名 &#8211; (庙)是一天建成的][2] ，输入下面的地址可以得到滔滔第一条信息，不过这个地址失效了。
> <pre id="line1" style="font-family: monospace; line-height: 14px; padding: 0px; margin: 0px;">http://taotao.qq.com/v1/qz_first/firstjson?uin=你的QQ号</pre>
没关系~~我们从滔滔给出的JS插件来找就可以。
## 下面是分析，如果看不懂直接跳到下面一段

<pre lang="xml"></pre>
当然你可以直接用上面的代码显示在你的博客上~但是我只需要我自己的签名信息就可以了。  
从http://www.taotao.com/js/dkapi.js可以看到下面这个地址，复制到浏览器看一下~
> http://www.taotao.com/cgi-bin/msgj?qq=这里换成你的QQ号&num=1
打开的结果是一段JS
<pre escaped="true" lang="xml">doApi({"posts":[{"cn":"人参要泡在杯具里才入味。有点感冒&amp;喉咙痛~没发热~~37.1° ","id":"14294845341","sr":3,"time":"3,1"}],"ret":0,"total":203,"type":0,"ui":{"lrank":0,"name":"QQ昵称","qq":你的QQ号,"rank":0,"rec":"","usn":9948760}})</pre>
以前我看到的好像只返回一段JSON的，现在前面加上了个调用函数，没关系，我们来实现就可以了。
## 上面是分析方法，如果看不懂直接跳到这里实现

具体代码：
<pre lang="js"><div id="taotao">  </div>



</pre>
在wordpress的做法是可以在header.php内你想显示的地方加一个<div id=&#8221;taotao&#8221;></div>，然后上面的代码可以放在任何地方。不过注意代码顺序不要乱了,doApi方法要在taotao.js的前面，这样才可以调用嘛~
很简单~

 [1]: http://farm5.static.flickr.com/4038/4225675170_4d9dcd1c34.jpg
 [2]: http://ooxx.me/qq-sig.orz