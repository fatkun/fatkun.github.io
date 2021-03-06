---
title: HDFS文件的健康检查
author: fatkun
type: post
date: 2017-07-16T13:35:45+00:00
url: /2017/07/hdfs-health-check.html
categories:
  - hadoop
tags:
  - hdfs

---
文章来源：[HDFS DataNode Scanners and Disk Checker Explained][1]
以下只简单翻译部分文字，详情看英文原文。
## 简单的概念

一个文件包含多个block，一个block有一个或多个副本。
block存储在每台机器的磁盘上，并且包含个blk_xxx.meta信息，meta中包含crc校验信息等。
## 这篇文章为了解答以下问题

datanode什么时候检查blocks？
datanode怎么保证内存（in-memory）中的metadata和本地磁盘保持一致？
如果发生block读失败，是因为磁盘错误吗？有可能是其他间歇性的错误（例如网络中断）？
## Block Scanner & Volume Scanner

每个datanode有一个block scanner，一个block scanner包含有多个volume scanner，每个volume scanner扫描一个磁盘。这里是多线程的。volume scanner需要读取全部磁盘的数据，验证每一个block，我们称这个为常规扫描（_regular scans_）。因为要真实读取数据，这是一个重IO的操作，这里会有个限速器。
除了常规扫描外，volume scanner还维护了一份suspicious blocks（怀疑有问题的blocks列表），它是在出现读写错误的时候（不管是来自于client或者datanode），并且不是网络错误，加进这个列表里面。volume scanner会优先检查这些文件，并且为了避免重复检查，这里也有些优化。
这里还有个block cursor来保存扫描进度，重启datanode也可以接着上次干活。
有两个参数
dfs.block.scanner.volume.bytes.per.second  每秒最多扫描的字节数
dfs.datanode.scan.period.hours 每次扫描间隔多长时间，如果扫描提前完成了，就等。如果超过时间都没完成，就一直做完。
## Directory Scanners

用来检查datanode内存的元数据和磁盘实际存储的是不是一致，主要检查文件在不在，meta信息在不在，文件大小和内存中的是不是一样。
这块没有仔细看，后面再认真看下。
如果发现文件大小不一样，会认为是corrupted block，汇报给namenode。
## Disk Checker

主要检查目录在不在，能不能建子目录，location路径是不是目录，目录有没有read、write、execute权限。
## 坏块（corrupted block）处理

corrupted block会汇报给namenode，namenode调用namesystem.reportBadBlocks处理，会把block标记为corrupt，如果副本数满足一定条件，会把那个副本删掉。
存活的副本数低于要求的副本数时，会触发副本复制。
## 再来看看我们集群

发现我们用的cdh5.4.0版本，dfs.datanode.scan.period.hours的默认值是0，Block Scanner被关闭了。
下面是打开的补丁，另外对于磁盘检查这块后面的版本也有很多补丁。
https://issues.apache.org/jira/browse/HDFS-8681 BlockScanner is incorrectly disabled by default
&nbsp;

 [1]: https://blog.cloudera.com/blog/2016/12/hdfs-datanode-scanners-and-disk-checker-explained/