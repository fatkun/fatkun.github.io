---
title: minikube在宿主机请求集群IP
author: fatkun
type: post
date: 2019-02-18T03:34:47+00:00
url: /2019/02/minikube在宿主机请求集群ip.html
categories:
  - docker
tags:
  - k8s
  - minikube

---
添加路由进行请求
sudo ip route add 172.17.0.0/16 via $(minikube ip)
## 来源

https://stackoverflow.com/questions/42268814/routing-an-internal-kubernetes-ip-address-to-the-host-system