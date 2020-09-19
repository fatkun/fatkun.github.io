---
title: 使用docker部署hadoop hdfs
author: fatkun
type: post
date: 2017-12-24T10:15:12+00:00
url: /2017/12/deploy-hadoop-hdfs-use-docker.html
wp-syntax-cache-content:
  - |
    a:4:{i:1;s:260:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">docker network create hadoop</pre></td></tr></table><p class="theCode" style="display:none;">docker network create hadoop</p></div>
    ";i:2;s:2062:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="yml" style="font-family:monospace;">version: &quot;3&quot;
    services:
      namenode:
        image: uhopper/hadoop-namenode
        hostname: namenode1
        container_name: namenode1
        # 要和networks保持一致，这样能够自动发现其他机器（如datanode1.hadoop）
        domainname: hadoop
        ports:
          - &quot;50070:50070&quot;
        volumes:
          - ./nn:/hadoop/dfs/name
        environment:
          - HDFS_CONF_dfs_replication=1
          - CLUSTER_NAME=ns1
    &nbsp;
      datanode1:
        image: uhopper/hadoop-datanode
        hostname: datanode1
        container_name: datanode1
        domainname: hadoop
        volumes:
          - ./dn1:/hadoop/dfs/data
        environment:
          - HDFS_CONF_dfs_replication=1
          - CLUSTER_NAME=ns1
          - CORE_CONF_fs_defaultFS=hdfs://namenode1:8020
    &nbsp;
    &nbsp;
    networks:
      default:
        # 使用外部网络（如果不加这个，启动时会自动创建一个${目录名}_${name}的网络）
        external:
          name: hadoop</pre></td></tr></table><p class="theCode" style="display:none;">version: &quot;3&quot;
    services:
      namenode:
        image: uhopper/hadoop-namenode
        hostname: namenode1
        container_name: namenode1
        # 要和networks保持一致，这样能够自动发现其他机器（如datanode1.hadoop）
        domainname: hadoop
        ports:
          - &quot;50070:50070&quot;
        volumes:
          - ./nn:/hadoop/dfs/name
        environment:
          - HDFS_CONF_dfs_replication=1
          - CLUSTER_NAME=ns1
      
      datanode1:
        image: uhopper/hadoop-datanode
        hostname: datanode1
        container_name: datanode1
        domainname: hadoop
        volumes:
          - ./dn1:/hadoop/dfs/data
        environment:
          - HDFS_CONF_dfs_replication=1
          - CLUSTER_NAME=ns1
          - CORE_CONF_fs_defaultFS=hdfs://namenode1:8020
          
    
    networks:
      default:
        # 使用外部网络（如果不加这个，启动时会自动创建一个${目录名}_${name}的网络）
        external:
          name: hadoop</p></div>
    ";i:3;s:413:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">docker <span style="color: #7a0874; font-weight: bold;">exec</span> <span style="color: #660033;">-it</span> namenode1 <span style="color: #c20cb9; font-weight: bold;">bash</span></pre></td></tr></table><p class="theCode" style="display:none;">docker exec -it namenode1 bash</p></div>
    ";i:4;s:5348:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #cc66cc;">17</span><span style="color: #339933;">/</span><span style="color: #cc66cc;">12</span><span style="color: #339933;">/</span><span style="color: #cc66cc;">24</span> 08<span style="color: #339933;">:</span><span style="color: #cc66cc;">39</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">15</span> WARN hdfs.<span style="color: #006633;">DFSClient</span><span style="color: #339933;">:</span> DataStreamer <span style="color: #003399;">Exception</span>
    java.<span style="color: #006633;">nio</span>.<span style="color: #006633;">channels</span>.<span style="color: #006633;">UnresolvedAddressException</span>
            at sun.<span style="color: #006633;">nio</span>.<span style="color: #006633;">ch</span>.<span style="color: #006633;">Net</span>.<span style="color: #006633;">checkAddress</span><span style="color: #009900;">&#40;</span>Net.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">101</span><span style="color: #009900;">&#41;</span>
            at sun.<span style="color: #006633;">nio</span>.<span style="color: #006633;">ch</span>.<span style="color: #006633;">SocketChannelImpl</span>.<span style="color: #006633;">connect</span><span style="color: #009900;">&#40;</span>SocketChannelImpl.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">622</span><span style="color: #009900;">&#41;</span>
            at org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">hadoop</span>.<span style="color: #006633;">net</span>.<span style="color: #006633;">SocketIOWithTimeout</span>.<span style="color: #006633;">connect</span><span style="color: #009900;">&#40;</span>SocketIOWithTimeout.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">192</span><span style="color: #009900;">&#41;</span>
            at org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">hadoop</span>.<span style="color: #006633;">net</span>.<span style="color: #006633;">NetUtils</span>.<span style="color: #006633;">connect</span><span style="color: #009900;">&#40;</span>NetUtils.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">531</span><span style="color: #009900;">&#41;</span>
            at org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">hadoop</span>.<span style="color: #006633;">hdfs</span>.<span style="color: #006633;">DFSOutputStream</span>.<span style="color: #006633;">createSocketForPipeline</span><span style="color: #009900;">&#40;</span>DFSOutputStream.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">1537</span><span style="color: #009900;">&#41;</span>
            at org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">hadoop</span>.<span style="color: #006633;">hdfs</span>.<span style="color: #006633;">DFSOutputStream</span>$DataStreamer.<span style="color: #006633;">createBlockOutputStream</span><span style="color: #009900;">&#40;</span>DFSOutputStream.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">1313</span><span style="color: #009900;">&#41;</span>
            at org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">hadoop</span>.<span style="color: #006633;">hdfs</span>.<span style="color: #006633;">DFSOutputStream</span>$DataStreamer.<span style="color: #006633;">nextBlockOutputStream</span><span style="color: #009900;">&#40;</span>DFSOutputStream.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">1266</span><span style="color: #009900;">&#41;</span>
            at org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">hadoop</span>.<span style="color: #006633;">hdfs</span>.<span style="color: #006633;">DFSOutputStream</span>$DataStreamer.<span style="color: #006633;">run</span><span style="color: #009900;">&#40;</span>DFSOutputStream.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">449</span><span style="color: #009900;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">17/12/24 08:39:15 WARN hdfs.DFSClient: DataStreamer Exception
    java.nio.channels.UnresolvedAddressException
            at sun.nio.ch.Net.checkAddress(Net.java:101)
            at sun.nio.ch.SocketChannelImpl.connect(SocketChannelImpl.java:622)
            at org.apache.hadoop.net.SocketIOWithTimeout.connect(SocketIOWithTimeout.java:192)
            at org.apache.hadoop.net.NetUtils.connect(NetUtils.java:531)
            at org.apache.hadoop.hdfs.DFSOutputStream.createSocketForPipeline(DFSOutputStream.java:1537)
            at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.createBlockOutputStream(DFSOutputStream.java:1313)
            at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.nextBlockOutputStream(DFSOutputStream.java:1266)
            at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:449)</p></div>
    ";}
categories:
  - 未分类
tags:
  - docker
  - hadoop

---
先创建一个网络
<pre escaped="true" lang="bash">docker network create hadoop</pre>
把本机新建一个目录hadoop，以下xml保存为docker-compose.yml
<pre escaped="true" lang="yml">version: "3"
services:
  namenode:
    image: uhopper/hadoop-namenode
    hostname: namenode1
    container_name: namenode1
    # 要和networks保持一致，这样能够自动发现其他机器（如datanode1.hadoop）
    domainname: hadoop
    ports:
      - "50070:50070"
    volumes:
      - ./nn:/hadoop/dfs/name
    environment:
      - HDFS_CONF_dfs_replication=1
      - CLUSTER_NAME=ns1
  
  datanode1:
    image: uhopper/hadoop-datanode
    hostname: datanode1
    container_name: datanode1
    domainname: hadoop
    volumes:
      - ./dn1:/hadoop/dfs/data
    environment:
      - HDFS_CONF_dfs_replication=1
      - CLUSTER_NAME=ns1
      - CORE_CONF_fs_defaultFS=hdfs://namenode1:8020
      

networks:
  default:
    # 使用外部网络（如果不加这个，启动时会自动创建一个${目录名}_${name}的网络）
    external:
      name: hadoop
</pre>
使用docker-compose up -d 启动，可以访问 http://127.0.0.1:50070 查看namenode页面
另外可以进入container里面
<pre escaped="true" lang="bash">docker exec -it namenode1 bash</pre>
尝试执行一下hdfs dfs -put /etc/issue /
如果报错
<pre escaped="true" lang="java">17/12/24 08:39:15 WARN hdfs.DFSClient: DataStreamer Exception
java.nio.channels.UnresolvedAddressException
        at sun.nio.ch.Net.checkAddress(Net.java:101)
        at sun.nio.ch.SocketChannelImpl.connect(SocketChannelImpl.java:622)
        at org.apache.hadoop.net.SocketIOWithTimeout.connect(SocketIOWithTimeout.java:192)
        at org.apache.hadoop.net.NetUtils.connect(NetUtils.java:531)
        at org.apache.hadoop.hdfs.DFSOutputStream.createSocketForPipeline(DFSOutputStream.java:1537)
        at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.createBlockOutputStream(DFSOutputStream.java:1313)
        at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.nextBlockOutputStream(DFSOutputStream.java:1266)
        at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:449)</pre>
请检查网络配置是否正确，ping datanode1.hadoop 是否返回IP