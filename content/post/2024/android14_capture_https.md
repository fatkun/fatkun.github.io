---
title: "Android14 https 抓包"
date: 2024-06-22T00:41:10+08:00
tags: [android, 抓包]
categories: [android]
author: "fatkun"
draft: false
typora-root-url: ./..\..\..\static
---

# 目标

使用Android14的设备进行网络抓包。

# 前提

我的设备是小米6平板，已root。

# 操作

使用[Reqable](https://reqable.com/)来抓包，这个软件和知名应用HttpCanary是同一个作者，试用了一下还挺方便。

由于要抓取的是https，所以要安装CA证书，我是抓取手机的APP，Reqable有指引怎么在Android手机安装证书，我用的是Magisk的方式。

同时在手机上也下载一个客户端，我是使用协同的方式。电脑点击左上角的手机图标![image-20240622004817428](/img/android14_capture_https/image-20240622004817428.png)，手机扫码后，使用协同的方式。这个时候已经可以抓取部分https的请求了，但是部分提示客户端SSL握手失败。

![image-20240622005428599](/img/android14_capture_https/image-20240622005428599.png)

客户端SSL握手失败的问题，这时要借助LSPosed的模块JustTrustMe，用于跳过证书校验，为了支持Android14，有人[自己编译了一个版本](https://github.com/SekiBetu/JustTrustMe/releases/tag/v.3)。安装后，并且选择你抓包的应用。
