---
title: 记录cloudera manager安装hadoop的步骤
author: fatkun
type: post
date: 2013-10-19T17:24:36+00:00
url: /2013/10/cloudera-manager-install-hadoop.html
duoshuo_thread_id:
  - 6300410041287574274
categories:
  - hadoop

---
## 安装cloudera-manager

在<http://go.cloudera.com/cloudera-standard-download.html>下载cloudera-manager-installer.bin
下载完要给它设置执行权限 chmod +x ./cloudera-manager-installer.bin
要用root权限运行, sudo ./cloudera-manager-installer.bin
一步步执行后，会下载安装jdk和cm，需要等一会儿，要下载200mb左右。(手工下载路径，http://archive.cloudera.com/cm4/cm/4/，但下载这个不知道怎么用，还是给程序下载吧。)
安装完后，提示打开 http://localhost:7180
## 部署hadoop

ubuntu中的root用户没有密码，可以sudo passwd root设置密码
ubuntu默认没有openssh-server，使用sudo apt-get install openssh-server安装吧，需要测试ssh localhost是否有效
host好像不允许一个IP对应多个主机名称，编辑/etc/hosts把localhost的那个去掉，保留主机的那个。
到\`http://archive.cloudera.com/cdh4/parcels/\`下载你想要安装的CDH版本（我的是ubuntu12.04，下载CDH-4.3.0-1.cdh4.3.0.p0.22-precise.parcel文件），并且下载manifest.json文件，里面有hash值，把hash值找出来，保存为CDH-4.3.0-1.cdh4.3.0.p0.22-precise.parcel.sha文件（根据版本改名字），echo &#8220;1959e87dc6bfcfe9cc7eacd1ff7727bfd737f42d&#8221;  > /opt/cloudera/parcel-repo/CDH-4.3.0-1.cdh4.3.0.p0.22-precise.parcel.sha
把下载好的包放在/opt/cloudera/parcel-repo目录下,然后cm应该不会重新下载了。。
另外如果用mysql还要自己安装mysql-server和jdbc包。
&nbsp;
&nbsp;