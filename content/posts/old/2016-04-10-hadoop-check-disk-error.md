---
title: hadoop检查目录健康状态
author: fatkun
type: post
date: 2016-04-10T08:38:39+00:00
url: /2016/04/hadoop-check-disk-error.html
duoshuo_thread_id:
  - 6300421658486244098
categories:
  - hadoop

---
DiskChecker负责检查目录是否有建目录和判断权限。
## datanode

BlockPoolSlice.checkDirs()  
DataNode.checkDiskError()
## nodeManager

LocalDirsHandlerService.checkDirs()