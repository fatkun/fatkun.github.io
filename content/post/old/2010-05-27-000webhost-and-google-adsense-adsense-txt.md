---
title: 利用.htaccess解决000webhost免费主机Google Adsense验证问题(adsense.txt)
author: fatkun
type: post
date: 2010-05-28T02:41:27+00:00
url: /2010/05/000webhost-and-google-adsense-adsense-txt.html
views:
  - 8
duoshuo_thread_id:
  - 6300408725496660737
categories:
  - 胡言乱语
tags:
  - htaccess

---
最近在申请Google Adsense，提示要验证域名的所有者，所以上网找到了这个方法。我使用的是wordpress，用super-cache时加了一些规则，注意要把下面的规则放到最前面。
**原创文章，转载请注明：** 转载自<a style="color: #5371c5; text-decoration: none; padding: 0px; margin: 0px;" href="http://www.imlongleg.com/archives/94.html">利用rewrite规则解决000webhost免费主机Google Adsense验证问题</a>
## 解决方法：

最近长脚在生气Google Adsense的广告申请，可是在申请过程中遇到了瓶颈。Google Adsense需要在网站根目录放置一个adsense.txt的文件，来证明这个网站的所有权。长脚在放了好几次，都无法正常的通过浏览器访问到这个txt文件，网上查找了一下，好像是000webhost主机做过设置还是怎么的，反正就是不行。
不过长脚还是找来一个偏门的解决办法,利用.htaccess中添加rewrite语句。具体请看下例：
**RewriteRule ^a\.txt$ a.html**
其中要上传的文件为a.html，访问的为a.txt
如果你的.htaccess文件中是空的，那就要写全下列语句了
**RewriteEngine on  
RewriteBase /  
RewriteRule ^a\.txt$ a.html**
有以上问题的朋友不妨试试看这个方法