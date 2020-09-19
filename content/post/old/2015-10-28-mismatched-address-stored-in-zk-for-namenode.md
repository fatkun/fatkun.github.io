---
title: Mismatched address stored in ZK for NameNode
author: fatkun
type: post
date: 2015-10-28T08:28:52+00:00
url: /2015/10/mismatched-address-stored-in-zk-for-namenode.html
duoshuo_thread_id:
  - 6300410896166421249
categories:
  - hadoop
tags:
  - hadoop
  - hdfs

---
我在namenode配置dfs.namenode.servicerpc-address端口后，Failover Controller 报错
java.lang.RuntimeException: Mismatched address stored in ZK for NameNode at kpixxx/xx.xx.xx.xx:88
## 解决方法

  1. 停止Failover Controller
  2. 通过zookeeper删除 /hadoop-ha
  3. 通过cloudera manager 初始化zookeeper的HA
  4. 重新启动Failover Controller
&nbsp;