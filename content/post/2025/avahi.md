---
title: "avahi服务发现"
date: 2025-05-26T10:55:33+08:00
tags: [nas]
categories: [nas]
author: "fatkun"
draft: false
---
## 背景
之前使用OMV，由于安装到U盘，U盘损坏，尝试使用飞牛os。但是在使用VRTV的时候，发现只能使用SMB，SMB在快进的时候，总是停顿几秒，很不爽，只有用FTP才能不停顿。
但是OMV是怎么让VRTV发现的，尝试OMV就算改了端口也一样能被发现，一定是有什么东西在广播。问了AI之后，发现是使用了avahi，可以在飞牛OS上安装。


## 安装
以下命令需要在root账号执行

```bash
apt install avahi-daemon avahi-utils
```


新增配置文件 /etc/avahi/services/smb.service
```xml
<!DOCTYPE service-group SYSTEM "avahi-service.dtd">

<service-group>
  <name replace-wildcards="yes">%h(SMB)</name>
  <service>
    <type>_device-info._tcp</type>
    <txt-record>model=Xserve</txt-record>
  </service>
  <service>
    <type>_smb._tcp</type>
    <port>445</port>
  </service>
</service-group>
```


重启和开机启动
```bash
systemctl restart avahi
systemctl enable avahi
```


停止原来的nmbd
```bash
systemctl stop nmbd
systemctl disable nmbd
```

avahi-tools 软件包包括许多方便的实用程序，可用于检查系统上的 mDNS 服务的工作情况。比如：
```bash
# 查看局域网内所有已注册的 mDNS 服务
$ avahi-browse -a -r
```

## 绑定.local域名
在 /etc/avahi/hosts 目录添加域名
```
10.0.0.210 xxx.local
```

修改完后重启
```
sudo systemctl restart avahi

# 查看日志
sudo systemctl status avahi
sudo journalctl -u avahi
```
如果IP重复，日志里面会报错误，貌似一个IP只能配置一个域名。
mdns在windows可以解析，但是在安卓我解析不了。

## 匿名FTP
为了使用匿名用户登录FTP，我安装了proftpd，匿名用户会使用ftp账户的目录。

## 参考
[如何使用 Avahi 在局域网轻松发现你的系统服务](https://www.hi-linux.com/posts/45401.html)