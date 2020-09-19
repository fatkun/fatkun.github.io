---
title: apache php 不缓存配置
author: fatkun
type: post
date: 2015-01-25T04:08:04+00:00
url: /2015/01/apache-php-no-cache.html
duoshuo_thread_id:
  - 6300410881830290177
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:1065:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;">ExpiresDefault &quot;access plus 2 day&quot;
    ExpiresByType text/php &quot;access plus 5 seconds&quot;
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;FilesMatch</span> <span style="color: #ff0000;">&quot;.(php)$&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
    Header set Cache-Control &quot;private, must-revalidate&quot;
    Header set Pragma &quot;no-cache&quot;
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/FilesMatch<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">ExpiresDefault &quot;access plus 2 day&quot;
    ExpiresByType text/php &quot;access plus 5 seconds&quot;
    &lt;FilesMatch &quot;.(php)$&quot;&gt;
    Header set Cache-Control &quot;private, must-revalidate&quot;
    Header set Pragma &quot;no-cache&quot;
    &lt;/FilesMatch&gt;</p></div>
    ";}
categories:
  - 未分类

---
&nbsp;
ExpiresDefault可以设置所有文件的缓存时间
针对php设置 header, &#8220;private, must-revalidate&#8221; 设成这个还能够后退，没搞清楚原理，但每次刷新不会使用旧的缓存。
<pre escaped="true" lang="xml">ExpiresDefault "access plus 2 day"
ExpiresByType text/php "access plus 5 seconds"
&lt;FilesMatch ".(php)$"&gt;
Header set Cache-Control "private, must-revalidate"
Header set Pragma "no-cache"
&lt;/FilesMatch&gt;</pre>
&nbsp;
## 参考

http://httpd.apache.org/docs/2.2/mod/mod_expires.html  
http://www.jb51.net/article/15009.htm