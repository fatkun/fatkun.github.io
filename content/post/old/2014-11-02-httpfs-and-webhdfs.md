---
title: hdfs httpfs与webhdfs的简单使用
author: fatkun
type: post
date: 2014-11-02T08:46:33+00:00
url: /2014/11/httpfs-and-webhdfs.html
duoshuo_thread_id:
  - 6300410880953680642
categories:
  - hadoop
tags:
  - hadoop
  - hdfs
  - httpfs
  - webhdfs

---
## HttpFS和WebHDFS

通过http协议操作hdfs有两个组件，httpfs和webhdfs，我一开始还以为这两个是同一个东西，其实不是。webhdfs是namenode、datanode自带的，httpfs是完全独立的一个组件。
webhdfs上传文件等操作需要通过某个datanode进行，而不是直接通过namenode上传，客户端有可能访问多个机器。而httpfs，所有的操作都通过httpfs进行。
webhdfs和httpfs的使用方法基本是一样的，只有很小很小的差别。
&nbsp;
## HttpFS一些常用的操作

查看home目录  
curl &#8220;http://osg11-vm06:8014/webhdfs/v1?op=GETHOMEDIRECTORY&user.name=kpi&#8221;
创建目录  
curl -i -X PUT &#8220;http://osg11-vm06:8014/webhdfs/v1/tmp/chenyk?op=MKDIRS&user.name=kpi&#8221;
curl -i -X PUT &#8220;http://osg11-vm06:8014/webhdfs/v1/tmp/chenyk/a/b/c?op=MKDIRS&user.name=kpi&#8221;
删除目录，recursive参数删除非空目录  
curl -i -X DELETE &#8220;http://osg11-vm06:8014/webhdfs/v1/tmp/chenyk/a?op=DELETE&recursive=true&user.name=kpi&#8221;
创建文件(httpfs执行这一步没意义，上传也是通过httpfs上传)  
curl -i -X PUT &#8220;http://osg11-vm06:8014/webhdfs/v1/tmp/chenyk/test?op=CREATE&user.name=kpi&#8221;
创建文件和上传  
这里需要加入header，否则提示出错，可能是个bug https://issues.cloudera.org/browse/HUE-679
curl -i -X PUT -T /tmp/test.txt &#8220;http://osg11-vm06:8014/webhdfs/v1/tmp/chenyk/test?op=CREATE&data=true&user.name=kpi&#8221; -H &#8220;Content-Type:application/octet-stream&#8221;
追加文件  
curl -i -X POST -T /tmp/test.txt &#8220;http://osg11-vm06:8014/webhdfs/v1/tmp/chenyk/test?op=APPEND&data=true&user.name=kpi&#8221; -H &#8220;Content-Type:application/octet-stream&#8221;
打开文件并读取  
curl -i -L &#8220;http://osg11-vm06:8014/webhdfs/v1/tmp/chenyk/test?op=OPEN&user.name=kpi&#8221;
&nbsp;
## 参考

<http://hadoop.apache.org/docs/r1.0.4/webhdfs.html>