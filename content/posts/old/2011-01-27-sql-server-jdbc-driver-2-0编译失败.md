---
title: SQL Server JDBC Driver 2.0编译失败
author: fatkun
type: post
date: 2011-01-27T04:46:59+00:00
url: /2011/01/sql-server-jdbc-driver-2-0编译失败.html
duoshuo_thread_id:
  - 6300408796833383170
categories:
  - J2EE
tags:
  - jdk
  - 版本错误

---
&nbsp;
<p align="left">  Exception in thread "main" java.lang.UnsupportedClassVersionError: Bad version number in .class file</p>
<p align="left">  这个错误是因为JDK的版本不对，请检查你的JDK版本。然后检查你的包是不是都用低版本JDK编译的。</p>
<p align="left">  如果你在使用JDK1.5的话，一定要使用sqljdbc.jar包，sqljdbc4.jar是在JDK1.6的环境下才能使用的。</p>
<p align="left">  &nbsp;</p>