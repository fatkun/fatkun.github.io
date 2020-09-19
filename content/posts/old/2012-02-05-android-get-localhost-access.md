---
title: Android真机调试访问本地服务器（localhost）的解决方案
author: fatkun
type: post
date: 2012-02-05T15:21:33+00:00
url: /2012/02/android-get-localhost-access.html
duoshuo_thread_id:
  - 6300408827783152385
categories:
  - Android
tags:
  - Android
  - localhost
  - 真机调试

---
Android系统把它自己作为了localhost!当连接localhost都是他自己啊。。
囧，在这里晕了好久才发现。。
网上介绍的都是模拟器连接本地服务器的，我试着把链接改为http://10.0.2.2/依然不可以。。  
我是真机调试，不是模拟器，那怎么办呢？
## 解决方法

我的环境是用手机通过WIFI上网，和本地电脑在同一个局域网内。找出本地电脑的ip即可，手机可以直接访问这个IP。
如果不是在局域网内，只能把网页放到可以给外部访问的地方了（例如服务器）