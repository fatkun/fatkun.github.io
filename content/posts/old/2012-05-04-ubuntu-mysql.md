---
title: '[转]解决ubuntu下mysql不能远程连接数据库的问题'
author: fatkun
type: post
date: 2012-05-03T18:00:09+00:00
url: /2012/05/ubuntu-mysql.html
duoshuo_thread_id:
  - 6300408858699367169
categories:
  - Linux
tags:
  - mysql
  - mysql权限
  - Ubuntu
  - 权限

---
来源：<http://www.php100.com/html/webkaifa/database/Mysql/2010/1115/6818.html>  
Ubuntu10.04上自带的MySQL，执行了  
root@ubuntu:~#sudo apt-get install mysql  
安装完mysql-server
启动mysql  
root@ubuntu:~#/etc/init.d/mysql start
本地可以连接进入数据库。  
root@ubuntu:~#mysql -uroot -p
设置了远程访问权限：  
mysql> grant all PRIVILEGES on \*.\* to admin@’%’ identified by ‘123456′;  
Query OK, 0 rows affected (0.04 sec)
mysql> use information_schema  
mysql> select * from user_privileges;  
查询到有下面的结果：&#8217;admin’@&#8217;%&#8217;，说明mysql已经授权远程连接。
在windows下访问Ubuntu的数据库，连接不上，但是Ubuntu上安装的apache可以访问。  
用iptalbes添加端口3306后也无法访问。  
root@ubuntu:~# iptables -A INPUT -p tcp –dport 3306 -j ACCEPT
Ubuntu上查看Mysql网络连接：  
root@ubuntu:~# netstat -an |grep 3306  
tcp 0 0 127.0.0.1:3306 0.0.0.0:* LISTEN  
本地端口也在监听
root@ubuntu:~# ufw status  
Firewall not loaded  
本地防火墙未打开
后来在网上找到一个解决办法：  
查看/etc/mysql/my.cnf找到bind-address才发现配置的是 127.0.0.1(bind-address=127.0.0.1)，直接改为bind-address=192.168.0.xxx(本机ip)，然 后再查看3306端口打开了，ok，可以正常连接了