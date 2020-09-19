---
title: android抓包
author: fatkun
type: post
date: 2012-06-02T18:29:14+00:00
url: /2012/06/android-tcpdump.html
duoshuo_thread_id:
  - 6300408858850362114
categories:
  - Android
tags:
  - Android
  - 抓包

---
首先要安装好adb驱动,手机通过usb连接.
通过adb shell进入shell,再su有root权限  
把/system分区变成可读写  
android4.0的命令是这个,具体可以参考[这篇文章][1],有点不同  
mount -o remount /dev/block/platform/s3c-sdhci.0/by-name/system /system 
下载[tcpdump][2] ,[备用地址][3]
上传文件并添加权限  
adb push tcpdump /system/xbin/  
adb shell  
cd /system/xbin/  
chmod +x tcpdump
然后执行一下  
tcpdump -p -vv -s 0 -w /sdcard/capture.pcap
执行要监控的程序
最后把日志取下来  
adb pull /sdcard/capture.pcap
使用WireShark打开日志文件进行分析。
## 参考文章

http://yezhiqiu-love-yeah-net.iteye.com/blog/1122237  
http://blog.csdn.net/Zengyangtech/article/details/6030390

 [1]: http://blog.csdn.net/Zengyangtech/article/details/6030390
 [2]: http://www.strazzere.com/android/tcpdump
 [3]: http://files.cnblogs.com/yunsean/tcpdump.rar