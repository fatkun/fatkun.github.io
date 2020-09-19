---
title: hadoop cdh5.4 windows 开发环境
author: fatkun
type: post
date: 2015-11-15T03:45:27+00:00
url: /2015/11/hadoop-cdh5-4-windows-开发环境.html
duoshuo_thread_id:
  - 6300410896208364289
categories:
  - hadoop

---
  1. 下载hadoop编译好的包
  2. 安装cygwin
  3. 下载hadoop.dll和winutils.exe (我是自己编译的，在网上找了一个，不知道能否通用http://www.aboutyun.com/thread-8178-1-1.html)
  4. 配置环境变量HADOOP_HOME
  5. 配置环境变量PATH，增加%HADOOP_HOME%/bin
&nbsp;
报错处理
> <pre class="code-java">java.lang.UnsatisfiedLinkError: org.apache.hadoop.io.nativeio.NativeIO$Windows.access0(Ljava/lang/<span class="code-object">String</span>;I)Z</pre>
没有安装cygwin
> 找不到winutils.exe
上网下载或者自己编译，自己编译好麻烦。。。要安装windows sdk。如果你确实准备好了winutils.exe还是报错，看看是不是显示null\bin\winutils.exe，这样的话是你的环境变量HADOOP_HOME没生效。