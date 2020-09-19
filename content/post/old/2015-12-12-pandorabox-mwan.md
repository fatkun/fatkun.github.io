---
title: PandoraBox路由多线多拨
author: fatkun
type: post
date: 2015-12-12T13:12:15+00:00
url: /2015/12/pandorabox-mwan.html
duoshuo_thread_id:
  - 6300410896317416193
categories:
  - 未分类
tags:
  - MWAN
  - 多线多拨
  - 路由

---
## 划分VLAN

在网络->交换机里面，添加一个VLAN，看一下第二个vlan是怎么配置的，WAN的接口是在哪一个，然后自己插入lan接口，照着加一个。
第三个vlan：端口1为不关联，CPU为关联，其他为关
第一个vlan：端口1改成关
在网络->接口里面，添加一个新接口wan2。配置物理网卡为vlan eth0.3，配置拨号信息。配置两个WAN的网络跃点为不同的值
教程：http://www.right.com.cn/forum/thread-147109-1-1.html
## 配置MWAN

添加两个interface wan和刚才加的wan2  
添加成员分别配置两个网卡  
修改策略，选择两个成员