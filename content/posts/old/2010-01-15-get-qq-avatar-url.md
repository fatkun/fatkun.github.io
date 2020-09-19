---
title: 获取QQ头像地址
author: fatkun
type: post
date: 2010-01-14T16:19:59+00:00
url: /2010/01/get-qq-avatar-url.html
views:
  - 264
duoshuo_thread_id:
  - 6300408713186378497
categories:
  - 胡言乱语
tags:
  - qq头像
  - qq头像网址
  - 显示qq头像

---
由于QQ通过判断cookies是否登陆，所以**获取QQ头像已经失效**了。期待新的解决方法。(新方法：<a href="http://fatkun.com/2010/07/get-qq-avatar-with-cookie/" target="_blank">使用cookie获取QQ头像（JSP版）</a>)  
最近期末了~要考试，所以博客基本没怎么更新了~放假回家后可能都没什么机会上网咯~所以可能博客会停止更新一段时间~
今晚突然想得到某人的QQ头像，找找是否有一样的头像（纯蛋疼得无聊~）。 这个网站可以通过上传图片搜索相同的图片 <http://www.tineye.com/>，传说Google以后会支持这个功能~
<img style="border: 0px initial initial;" src="http://farm5.static.flickr.com/4048/4273718797_61f507b4bd.jpg" alt="" width="500" height="239" /> <!--more-->

说到Google，就不得不说Google可能要退出中国市场，可是真要说些什么，却什么都不敢说。杯具都是瓷器造的，Ma de in china! F*ck G..F.W! 好吧，说完了，于事无补。身在天朝只好笑而不语。
说正题，主要说说我的搜索方法的思路~
## 如何找到QQ头像地址？

  1. 首先想到的是通过**搜索引擎**搜索是否有现成的。不过第一次使用的关键词是“QQ头像地址”，结果找到的都失效了（如Myqq以及Vipqq的）
  2. 查看myqq以及Vipqq的代码。失望啊，它头像获取的地址是<http://my.qq.com/qq_face.php>，可惜，没有参数给我们调用，估计是通过Cookies传值的或者其他
  3. 想想还有没有同类的网站显示QQ头像的。对，WebQQ，里面有QQ头像地址，果然，就给我找到了。
  4. 找到之后，觉得我第一次的搜索关键字好像不太好，换一个“获取QQ头像”，丫的，搜索出来了。
## QQ头像地址在此

QQ10000号的qq头像：![qq][1]  
任意QQ头像地址：
http://face4.qun.qq.com/cgi/svr/face/getface?uin=<span style="color: #ff0000;"><strong>529403452 </strong></span><a href="http://face4.qun.qq.com/cgi/svr/face/getface?uin=529403452" target="_blank">点此看看效果</a>
QQ会员动态头像（仅会员的头像可查看）：
http://58.60.9.59/HISFACE/getfacefile?from=qqclub&usertype=1&dstuin=**<span style="color: #ff0000;">529403452</span>**
注：把上面<span style="color: #ff0000;"><strong>红色加粗</strong></span>的QQ号换为其他人的QQ号就行了，任何人的都可以。
注2：上面的QQ号非本人QQ号，在网上搜索到的，如有侵权，请联系我修改。
## 用Jquery显示头像（纯蛋疼）

<img id="avatar" alt="" /> 
输入你的qq号试试：  
<input id="qqnum" onkeyup="getQQAvatar()" type="text" />

 [1]: http://face4.qun.qq.com/cgi/svr/face/getface?uin=10000