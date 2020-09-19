---
title: ADB server didn’t ACK解决方法
author: fatkun
type: post
date: 2013-08-10T10:06:19+00:00
url: /2013/08/adb-server-didnt-ack解决方法.html
duoshuo_thread_id:
  - 6300410040826200834
categories:
  - Android
tags:
  - adb

---
原文：[【杂症】一个豌豆荚引发的血案——关于ADB server didn&#8217;t ACK的问题][1]  
原文有图，本文只作为备忘。
## 现象

ADB server didn&#8217;t ACK  
\* failed to start daemon \*
## 解决方法

找出那个程序占用了5037端口，然后把对应的进程kill掉。最后一位是PID。  
netstat -a -o 5037
我遇到的是tadb.exe，这个是腾讯手机管家的进程。  
如果你用了豌豆荚，也有个wangdoujia_hepler.exe之类的进程也要kill掉。

 [1]: http://www.cnblogs.com/longqi293/archive/2012/06/19/Android-Troubleshooting-ACK.html