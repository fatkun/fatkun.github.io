---
title: "N5095 Jellyfin硬解"
date: 2023-06-24T00:28:01+08:00
draft: false
---

按照一般教程开启jellyfin硬件加速总是报错：该客户端与媒体不兼容，服务器未发送兼容的媒体格式

由于N5095是11代的CPU，需要有些特殊配置。

首先内核要比较新，我是使用OMV，内核是6.1的



1. 在系统上添加所需的i915内核参数以启用加载GUC和HuC固件

```
sudo mkdir -p /etc/modprobe.d
sudo sh -c "echo 'options i915 enable_guc=3' >> /etc/modprobe.d/i915.conf"
```

2. 更新initramfs和grub

   Debian和Ubuntu

```
sudo update-initramfs -u && sudo update-grub
```

3. 重新启动系统并使用以下命令检查GuC和HuC状态，确保输出中没有FAIL或ERROR。

```
sudo reboot
sudo dmesg | grep i915
sudo cat /sys/kernel/debug/dri/0/gt/uc/guc_info
sudo cat /sys/kernel/debug/dri/0/gt/uc/huc_info
```

4. 安装jellyfin

```
---
version: "2.1"
services:
  jellyfin:
    image: nyanmisaka/jellyfin:latest
    container_name: jellyfin
    environment:
      - PUID=1000
      - PGID=100
      - TZ=Etc/UTC
      #- JELLYFIN_PublishedServerUrl=192.168.0.5 #optional
    volumes:
      - /mnt/docker/jellyfin2:/config
      - /mnt/hgst_8t:/data/hgst_8t
      - /mnt/2t:/data/2t
      - /mnt/st_4t:/data/st_4t
    devices:
      - "/dev/dri:/dev/dri"
    ports:
      - 8096:8096
      - 8920:8920 #optional
      - 7359:7359/udp #optional
      - 1900:1900/udp #optional
    restart: unless-stopped
```

在jellyfin里面，控制台-》播放

- 硬件加速选择QSV
- 勾选 启用低电压模式的 Intel H.264 硬件编码器
- 勾选 启用低电压模式的 Intel HEVC 硬件编码器



# 参考文档

[N5095, N5100, N5105, N6005, J6412等intel 11代Jasper Lake和Elkhart Lake平台cpu使用jellyfin开启硬件加速](https://www.symphonysun.com/2023/04/08/n5095-n5100-n5105-n6005-j6412%E7%AD%89intel-11%E4%BB%A3jasper-lake%E5%92%8Celkhart-lake%E5%B9%B3%E5%8F%B0cpu%E4%BD%BF%E7%94%A8jellyfin%E5%BC%80%E5%90%AF%E7%A1%AC%E4%BB%B6%E5%8A%A0%E9%80%9F/)

[N5095使用经验分享 Step By Step ](https://post.smzdm.com/p/avxe2p87/)
