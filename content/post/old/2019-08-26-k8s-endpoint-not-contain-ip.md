---
title: K8s Endpoint无IP定位错误方法
author: fatkun
type: post
date: 2019-08-26T02:57:21+00:00
url: /2019/08/k8s-endpoint-not-contain-ip.html
categories:
  - docker
tags:
  - endpoint
  - k8s
  - service

---
确认selector是否正确
确认pod里面配置的containerPort以及service里面的配置的port能对应上
确认pod是否ready了，不能只看get pod看到的1/1，还要看一下-o yaml的输出结果