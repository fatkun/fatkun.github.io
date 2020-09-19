---
title: hadoop磁盘写入选择策略
author: fatkun
type: post
date: 2016-07-14T10:27:36+00:00
url: /2016/07/hadoop-volume-choosing-policy.html
duoshuo_thread_id:
  - 6307125639627408129
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:1552:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>  
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>dfs.datanode.fsdataset.volume.choosing.policy<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>  
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>org.apache.hadoop.hdfs.server.datanode.fsdataset.AvailableSpaceVolumeChoosingPolicy<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>  
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">&lt;property&gt;  
      &lt;name&gt;dfs.datanode.fsdataset.volume.choosing.policy&lt;/name&gt;  
      &lt;value&gt;org.apache.hadoop.hdfs.server.datanode.fsdataset.AvailableSpaceVolumeChoosingPolicy&lt;/value&gt;  
    &lt;/property&gt;</p></div>
    ";}
categories:
  - hadoop
tags:
  - hadoop
  - hdfs

---
hadoop写入时，默认磁盘选择是轮询的方式。可以改用按空间大小来分配，避免某个磁盘特别满。
参数 ：dfs.datanode.fsdataset.volume.choosing.policy
<pre escaped="true" lang="xml">&lt;property&gt;  
  &lt;name&gt;dfs.datanode.fsdataset.volume.choosing.policy&lt;/name&gt;  
  &lt;value&gt;org.apache.hadoop.hdfs.server.datanode.fsdataset.AvailableSpaceVolumeChoosingPolicy&lt;/value&gt;  
&lt;/property&gt;</pre>
详细见：  
[hadoop2.0的datanode多目录数据副本存放策略][1]

 [1]: http://blog.csdn.net/bigdatahappy/article/details/39992075