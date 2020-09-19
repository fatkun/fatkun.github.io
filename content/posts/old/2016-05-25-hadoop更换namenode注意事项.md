---
title: hadoop更换namenode注意事项
author: fatkun
type: post
date: 2016-05-25T09:56:00+00:00
url: /2016/05/hadoop更换namenode注意事项.html
duoshuo_thread_id:
  - 6300421658884702978
categories:
  - hadoop

---
  1. 所有机器hosts都要加上新namenode
  2. 新namenode要建立好以前的用户和组
  3. zookeeper中HA的信息可以删除，然后重建zookeeper HA
  4. 把namenode image备份，把image和edit log传到新机器
  5. 需要删除一个namenode和failover controler，然后重新建
  6. 重启所有业务（包含用到hdfs的所有程序）
  7. 重新部署所有配置