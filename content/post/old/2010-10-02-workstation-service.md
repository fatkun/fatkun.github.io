---
title: XP下系统服务workstation启动很慢解决方法
author: fatkun
type: post
date: 2010-10-02T02:51:18+00:00
url: /2010/10/workstation-service.html
duoshuo_thread_id:
  - 6300408770463793921
categories:
  - 电脑知识
tags:
  - vmware
  - workstation
  - xp
  - 启动慢
  - 服务
  - 系统

---
## 症状

系统进入桌面之后，要等上1-2分钟才能完全操作，在这期间，发现很多自动运行的服务依然没有启动。设置workstation服务为手动或者禁止则开机正常。
## 解决方法

  1. 设置workstation服务为手动或禁止运行。（不过有个后遗症是关机时会提示“正在关闭网络连接”）
  2. 检查网卡自动获取IP是不是很慢，把网卡的IP设置为固定IP（我的电脑是因为这个原因，通过宽带拨号，本地连接可以设置为任何一个ip：如192.168.1.33，没影响的）
## 其他解决方法

  1.  由于安装各种插件(雅虎助手等)导致网络服务出问题或EXPLORER负载过大,同时还会引起WORKSTATION服务启动慢,有时候要20分钟左右才能启动机器.建议使用360安全卫士处理下流氓软件.这样情况会有好转
  2. 在本地连接的网络组件里,多余的组件会给WORKSTATION很大负荷,XP专业版的情况下基本只有4个是必需的,那就是MICROSOFT网络客户端,MICROSOFT网络文件和打印机的共享,QOS数据包计划程序和TIP/IP,其他的一律删掉.
  3. 因为安装VMware变慢，可以把VMware的三个服务(VMware Authorization Service,VMware NAT Service,VMware DHCP Service)设为手动，有需要再开启
## 额外知识

Workstation(即lanmanworkstation)服务，如果启动慢，将导致：  
在该服务启动后启动的各类服务组的服务延迟启动，包括  
RemoteValidation（包含NetLogon服务）  
NetDDEGroup（包含NetDDE服务）  
Parallel arbitrator（包含Parport并口服务）  
Extended Base（各类硬件管理服务如USB、串口等，音视频解码等）  
PCI Configuration（包含PCIDump服务）  
MS Transactions（包含MSDTC服务）  
　　而这些启动延迟，将导致网络登录延迟、网络管理功能延迟加载、音频启动延迟（开机声音延迟播出）、USB设备延迟加载等问题，直接导致系统的可用性。