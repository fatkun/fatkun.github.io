---
title: cloudera manager添加hive时报错找不到jdbc driver
author: fatkun
type: post
date: 2015-05-07T03:19:57+00:00
url: /2015/05/cloudera-manage-jdbc-driver-cannot-be-found.html
duoshuo_thread_id:
  - 6300410895658910465
categories:
  - hadoop
tags:
  - cloudera manager
  - cm
  - hadoop

---
cm 4.7
## 报错

JDBC driver cannot be found. Unable to find the JDBC database jar on host
## 解决方法

把包放入这个目录，注意文件名要保持一致  /usr/share/java/mysql-<wbr />connector-java.jar
## 来源

<https://groups.google.com/a/cloudera.org/forum/#!topic/cdh-user/OpXSfmzsnuo>