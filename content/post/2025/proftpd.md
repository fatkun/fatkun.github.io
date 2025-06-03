---
title: "在debian安装proftpd，配置匿名用户和虚拟路径"
date: 2025-05-26T10:55:33+08:00
tags: [nas]
categories: [nas]
author: "fatkun"
draft: false
---

## 安装
```bash
apt install proftpd
apt install proftpd-mod-vroot
```

```bash
useradd -md /var/ftp ftp
```

## 修改配置
配置目录在/etc/proftpd

修改 /etc/proftpd/proftpd.conf，去掉下面这句的#号。
```
DefaultRoot ~
Include /etc/proftpd/virtuals.conf

# 解决登录慢
UseReverseDNS off

```

在/etc/proftpd/virtuals.conf增加配置
VRootAlias的写法 `VRootAlias 原路径 虚拟路径`
```
# 加载模块
LoadModule mod_vroot.c
<IfModule mod_vroot.c>
VRootEngine on
VRootAlias /vol00/xxxx n8t
</IfModule>
```

## 权限问题

如果权限后面还有个+号，表示用了acl，需要使用getfacl查看

```bash
# 查看acl
getfacl vol1
# 移除所有的acl
setfacl -R -b vol1

chown -R admin:Users vol1
chmod -R 751 vol1
```