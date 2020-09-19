---
title: cdh4 spark配置LZO
author: fatkun
type: post
date: 2014-09-27T05:36:21+00:00
url: /2014/09/spark-with-lzo.html
duoshuo_thread_id:
  - 6300410880886571777
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:1119:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="html" style="font-family:monospace;">HADOOP_CONF_DIR=/etc/hadoop/conf
    &nbsp;
    SPARK_SUBMIT_CLASSPATH=$SPARK_SUBMIT_CLASSPATH:/etc/hive/conf:/opt/cloudera/parcels/HADOOP_LZO/lib/hadoop/lib/hadoop-lzo.jar
    #SPARK_SUBMIT_LIBRARY_PATH=$SPARK_SUBMIT_LIBRARY_PATH:/opt/cloudera/parcels/CDH/lib/hadoop/lib/native:/opt/cloudera/parcels/HADOOP_LZO/lib/hadoop/lib/native
    LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/opt/cloudera/parcels/CDH/lib/hadoop/lib/native:/opt/cloudera/parcels/HADOOP_LZO/lib/hadoop/lib/native</pre></td></tr></table><p class="theCode" style="display:none;">HADOOP_CONF_DIR=/etc/hadoop/conf
    
    SPARK_SUBMIT_CLASSPATH=$SPARK_SUBMIT_CLASSPATH:/etc/hive/conf:/opt/cloudera/parcels/HADOOP_LZO/lib/hadoop/lib/hadoop-lzo.jar
    #SPARK_SUBMIT_LIBRARY_PATH=$SPARK_SUBMIT_LIBRARY_PATH:/opt/cloudera/parcels/CDH/lib/hadoop/lib/native:/opt/cloudera/parcels/HADOOP_LZO/lib/hadoop/lib/native
    LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/opt/cloudera/parcels/CDH/lib/hadoop/lib/native:/opt/cloudera/parcels/HADOOP_LZO/lib/hadoop/lib/native</p></div>
    ";i:2;s:1448:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">spark.ui.port   <span style="color: #000000;">8810</span>
    spark.executor.extraLibraryPath <span style="color: #000000; font-weight: bold;">/</span>opt<span style="color: #000000; font-weight: bold;">/</span>cloudera<span style="color: #000000; font-weight: bold;">/</span>parcels<span style="color: #000000; font-weight: bold;">/</span>CDH<span style="color: #000000; font-weight: bold;">/</span>lib<span style="color: #000000; font-weight: bold;">/</span>hadoop<span style="color: #000000; font-weight: bold;">/</span>lib<span style="color: #000000; font-weight: bold;">/</span>native:<span style="color: #000000; font-weight: bold;">/</span>opt<span style="color: #000000; font-weight: bold;">/</span>cloudera<span style="color: #000000; font-weight: bold;">/</span>parcels<span style="color: #000000; font-weight: bold;">/</span>HADOOP_LZO<span style="color: #000000; font-weight: bold;">/</span>lib<span style="color: #000000; font-weight: bold;">/</span>hadoop<span style="color: #000000; font-weight: bold;">/</span>lib<span style="color: #000000; font-weight: bold;">/</span>native</pre></td></tr></table><p class="theCode" style="display:none;">spark.ui.port   8810
    spark.executor.extraLibraryPath /opt/cloudera/parcels/CDH/lib/hadoop/lib/native:/opt/cloudera/parcels/HADOOP_LZO/lib/hadoop/lib/native</p></div>
    ";}
categories:
  - hadoop
  - hive
tags:
  - lzo
  - spark

---
使用的hadoop是cdh4.2.1版本 spark1.1，需要配置hadoop-native和lzo native
在spark-env.sh加入
<pre lang="html" escaped="true">HADOOP_CONF_DIR=/etc/hadoop/conf

SPARK_SUBMIT_CLASSPATH=$SPARK_SUBMIT_CLASSPATH:/etc/hive/conf:/opt/cloudera/parcels/HADOOP_LZO/lib/hadoop/lib/hadoop-lzo.jar
#SPARK_SUBMIT_LIBRARY_PATH=$SPARK_SUBMIT_LIBRARY_PATH:/opt/cloudera/parcels/CDH/lib/hadoop/lib/native:/opt/cloudera/parcels/HADOOP_LZO/lib/hadoop/lib/native
LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/opt/cloudera/parcels/CDH/lib/hadoop/lib/native:/opt/cloudera/parcels/HADOOP_LZO/lib/hadoop/lib/native
</pre>
我加了SPARK\_SUBMIT\_LIBRARY\_PATH发现是加入了java.library.path，但是丢了默认的配置。改为加入LD\_LIBRARY_PATH里
spark-defaults.conf的配置
<pre escaped="true" lang="bash">spark.ui.port   8810
spark.executor.extraLibraryPath /opt/cloudera/parcels/CDH/lib/hadoop/lib/native:/opt/cloudera/parcels/HADOOP_LZO/lib/hadoop/lib/native</pre>
可能还需要加上 spark.executor.extraClassPath，但我当前还是单机测试，没配也能跑成功。。  
启动spark-sql试试，打开监控页面看看 http://xxxx:8810/environment/ 是否配置正确。
参考：  
http://hsiamin.com/posts/2014/05/03/enable-lzo-compression-on-hadoop-pig-and-spark/ （按这里的配置不成功，可能环境变量名称改了。）  
http://lotso.blog.51cto.com/3681673/1441737  
https://spark.apache.org/docs/latest/configuration.html