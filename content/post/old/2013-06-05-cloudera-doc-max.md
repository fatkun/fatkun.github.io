---
title: '[蛋疼向]cloudera文档最大化'
author: fatkun
type: post
date: 2013-06-04T17:09:42+00:00
url: /2013/06/cloudera-doc-max.html
duoshuo_thread_id:
  - 6300410024036401922
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:904:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="js" style="font-family:monospace;">javascript:$(&quot;#center article&quot;).css(&quot;top&quot;, 0);$(&quot;#site-head&quot;).hide();$(&quot;#topnav&quot;).hide();$(&quot;#searchform&quot;).css(&quot;top&quot;, &quot;auto&quot;).css(&quot;bottom&quot;, 0).css(&quot;left&quot;, &quot;10px&quot;).css(&quot;right&quot;, &quot;auto&quot;);$(&quot;#leftbar&quot;).css(&quot;top&quot;, 0);</pre></td></tr></table><p class="theCode" style="display:none;">javascript:$(&quot;#center article&quot;).css(&quot;top&quot;, 0);$(&quot;#site-head&quot;).hide();$(&quot;#topnav&quot;).hide();$(&quot;#searchform&quot;).css(&quot;top&quot;, &quot;auto&quot;).css(&quot;bottom&quot;, 0).css(&quot;left&quot;, &quot;10px&quot;).css(&quot;right&quot;, &quot;auto&quot;);$(&quot;#leftbar&quot;).css(&quot;top&quot;, 0);</p></div>
    ";}
categories:
  - 未分类

---
cloudera的文档可视面积太小了。。。头部占了很大高度。。
<a href="http://www.cloudera.com/content/cloudera-content/cloudera-docs/CDH4/4.2.0/CDH4-Release-Notes/CDH4-Release-Notes.html" target="_blank">点我到文档地址</a>
## 解决方法

使用css改变一下样式。。
在浏览器加入一个书签
代码如下：
<pre lang="js" escaped="true">javascript:$("#center article").css("top", 0);$("#site-head").hide();$("#topnav").hide();$("#searchform").css("top", "auto").css("bottom", 0).css("left", "10px").css("right", "auto");$("#leftbar").css("top", 0);</pre>