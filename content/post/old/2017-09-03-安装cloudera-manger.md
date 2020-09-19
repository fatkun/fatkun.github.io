---
title: 安装cloudera manger（中科大反向代理）
author: fatkun
type: post
date: 2017-09-03T07:02:09+00:00
url: /2017/09/安装cloudera-manger.html
categories:
  - hadoop
tags:
  - cloudera
  - cloudera manger
  - mirror
  - 镜像

---
从文档[Cloudera Manager Version and Download Information][1] 找到下载地址，按系统版本下载
国外的下载地址很慢，使用中科大做的反向代理访问，下面是centos6的cm地址
wget -r -np -k &#8216;https://cloudera.proxy.ustclug.org/cm5/redhat/6/x86_64/cm/5.12.1/&#8217;

 [1]: https://www.cloudera.com/documentation/enterprise/release-notes/topics/cm_vd.html#cmvd_topic_1