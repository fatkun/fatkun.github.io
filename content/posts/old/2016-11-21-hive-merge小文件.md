---
title: hive merge小文件
author: fatkun
type: post
date: 2016-11-21T10:47:17+00:00
url: /2016/11/hive-merge小文件.html
duoshuo_thread_id:
  - 6355374519040869122
categories:
  - hive
tags:
  - hive

---
2.输出合并  
set hive.merge.mapfiles = true #在Map-only的任务结束时合并小文件（默认开启）
set hive.merge.mapredfiles = true #在Map-Reduce的任务结束时合并小文件  
set hive.merge.size.per.task = 256\*1000\*1000 #合并文件的大小  
set hive.merge.smallfiles.avgsize=16000000 #当输出文件的平均大小小于该值时，启动一个独立的map-reduce任务进行文件merge
见：<http://blog.csdn.net/yfkiss/article/details/8590486>