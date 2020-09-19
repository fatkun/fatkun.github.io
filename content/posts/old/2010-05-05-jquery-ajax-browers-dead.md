---
title: 使用JQuery的ajax方法造成浏览器假死
author: fatkun
type: post
date: 2010-05-04T16:07:31+00:00
url: /2010/05/jquery-ajax-browers-dead.html
views:
  - 21
duoshuo_thread_id:
  - 6300408725328888577
categories:
  - 网页前端

---
## 问题

最近做项目时使用JQuery的load等方法时会造成浏览器假死，在本地测试到不是很明显，上传到服务器后，浏览器居然能卡个10多秒。。（假死）  
因为我用jquery加载了整个页面，而不是少量的数据，听说用jquery加载大量的数据是会假死的，可能需要创建一个DOM树比较消耗时间吧。
## 解决方法

发现把jquery加载页面中引入的JS放在**主页面**上，假死情况就不会发生了。假死时间大大缩短。主页面的脚本如果不是马上要用到，可以放到底部让它慢慢下载，这样就不会影响到页面的显示。
另外还遇到了IE6的一个图像缓存的BUG~My god！·