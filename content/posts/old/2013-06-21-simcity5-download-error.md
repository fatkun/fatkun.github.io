---
title: 《模拟城市5》破解版提示下载失败解决方法
author: fatkun
type: post
date: 2013-06-20T17:22:04+00:00
url: /2013/06/simcity5-download-error.html
duoshuo_thread_id:
  - 6300410024376156930
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:272:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="html" style="font-family:monospace;">EnableMMAP off
    EnableSendfile off</pre></td></tr></table><p class="theCode" style="display:none;">EnableMMAP off
    EnableSendfile off</p></div>
    ";}
categories:
  - 未分类
tags:
  - download error
  - simcity5

---
前面的步骤都没有问题，提示Everything sounds good !! 但是点击图标安装游戏的时候，过一会儿就提示下载失败了。。
![][1] 
尼玛，搞了一晚上，自己解决了。。修改D:\simcity5\apache\httpd.conf 文件（注意我的目录可能和你不一样D:\simcity5）
在首行加入以下两句
<pre escaped="true" lang="html">EnableMMAP off
EnableSendfile off</pre>
保存，然后stop server再start server。
本文同时发在3dmgame论坛。。

 [1]: http://att.3dmgame.com/att/forum/201306/21/011625ktfvjnbjzvdmlmbr.png