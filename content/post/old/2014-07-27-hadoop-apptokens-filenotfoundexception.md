---
title: hadoop重启Namenode时，appTokens报FileNotFoundException
author: fatkun
type: post
date: 2014-07-27T13:56:09+00:00
url: /2014/07/hadoop-apptokens-filenotfoundexception.html
duoshuo_thread_id:
  - 6300410318438793985
wp-syntax-cache-content:
  - |
    a:6:{i:1;s:977:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="other" style="font-family:monospace;">Application application_1405852606905_0014 failed 3 times due to AM Container for appattempt_1405852606905_0014_000003 exited with exitCode: -1000 due to: RemoteTrace: java.io.FileNotFoundException: File does not exist: hdfs://mycluster:8020/user/kpi/.staging/job_1405852606905_0014/appTokens at org.apache.hadoop.hdfs.DistributedFileSystem.getFileStatus(DistributedFileSystem.java:809)</pre></td></tr></table><p class="theCode" style="display:none;">Application application_1405852606905_0014 failed 3 times due to AM Container for appattempt_1405852606905_0014_000003 exited with exitCode: -1000 due to: RemoteTrace: java.io.FileNotFoundException: File does not exist: hdfs://mycluster:8020/user/kpi/.staging/job_1405852606905_0014/appTokens at org.apache.hadoop.hdfs.DistributedFileSystem.getFileStatus(DistributedFileSystem.java:809)</p></div>
    ";i:2;s:1466:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #7a0874; font-weight: bold;">cd</span> <span style="color: #000000; font-weight: bold;">/</span>opt<span style="color: #000000; font-weight: bold;">/</span>cloudera<span style="color: #000000; font-weight: bold;">/</span>parcels<span style="color: #000000; font-weight: bold;">/</span>CDH<span style="color: #000000; font-weight: bold;">/</span>lib<span style="color: #000000; font-weight: bold;">/</span>hadoop-mapreduce;
    hadoop <span style="color: #c20cb9; font-weight: bold;">jar</span> hadoop-mapreduce-client-<span style="color: #000000; font-weight: bold;">*</span>-tests.jar <span style="color: #c20cb9; font-weight: bold;">sleep</span> -Dmapred.job.queue.name=<span style="color: #c20cb9; font-weight: bold;">sleep</span> <span style="color: #660033;">-m5</span> <span style="color: #660033;">-r5</span> <span style="color: #660033;">-mt</span> <span style="color: #000000;">60000</span> <span style="color: #660033;">-rt</span> <span style="color: #000000;">30000</span> <span style="color: #660033;">-recordt</span> <span style="color: #000000;">1000</span></pre></td></tr></table><p class="theCode" style="display:none;">cd /opt/cloudera/parcels/CDH/lib/hadoop-mapreduce;
    hadoop jar hadoop-mapreduce-client-*-tests.jar sleep -Dmapred.job.queue.name=sleep -m5 -r5 -mt 60000 -rt 30000 -recordt 1000</p></div>
    ";i:3;s:318:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="html" style="font-family:monospace;">cmd=delete  src=/user/kpi/.staging/job_1405852606905_0013</pre></td></tr></table><p class="theCode" style="display:none;">cmd=delete  src=/user/kpi/.staging/job_1405852606905_0013</p></div>
    ";i:4;s:1316:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">synchronized</span> <span style="color: #000066; font-weight: bold;">void</span> stop<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    ...
    <span style="color: #666666; font-style: italic;">//这里判断了是不是AM的最后一次尝试，如果是才清理</span>
            <span style="color: #000000; font-weight: bold;">if</span><span style="color: #009900;">&#40;</span>isLastAMRetry<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
              cleanupStagingDir<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span> 
    ...
      <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">    public synchronized void stop() {
    ...
    //这里判断了是不是AM的最后一次尝试，如果是才清理
            if(isLastAMRetry) {
              cleanupStagingDir();
            } 
    ...
      }</p></div>
    ";i:5;s:1824:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">  <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> shutDownJob<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    ...
          <span style="color: #666666; font-style: italic;">//We are finishing cleanly so this is the last retry</span>
          isLastAMRetry <span style="color: #339933;">=</span> <span style="color: #000066; font-weight: bold;">true</span><span style="color: #339933;">;</span>
          <span style="color: #666666; font-style: italic;">// Stop all services</span>
          <span style="color: #666666; font-style: italic;">// This will also send the final report to the ResourceManager</span>
          LOG.<span style="color: #006633;">info</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Calling stop for all the services&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          MRAppMaster.<span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">stop</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    ...
      <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">  public void shutDownJob() {
    ...
          //We are finishing cleanly so this is the last retry
          isLastAMRetry = true;
          // Stop all services
          // This will also send the final report to the ResourceManager
          LOG.info(&quot;Calling stop for all the services&quot;);
          MRAppMaster.this.stop();
    ...
      }</p></div>
    ";i:6;s:485:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="other" style="font-family:monospace;">org.apache.hadoop.yarn.exceptions.impl.pb.YarnRemoteExceptionPBImpl: Application doesn't exist in cache appattempt_1405852606905_0014_000001</pre></td></tr></table><p class="theCode" style="display:none;">org.apache.hadoop.yarn.exceptions.impl.pb.YarnRemoteExceptionPBImpl: Application doesn't exist in cache appattempt_1405852606905_0014_000001</p></div>
    ";}
categories:
  - hadoop
tags:
  - appTokens
  - exception
  - hadoop

---
## 现象

报错如下
<pre escaped="true" lang="other">Application application_1405852606905_0014 failed 3 times due to AM Container for appattempt_1405852606905_0014_000003 exited with exitCode: -1000 due to: RemoteTrace: java.io.FileNotFoundException: File does not exist: hdfs://mycluster:8020/user/kpi/.staging/job_1405852606905_0014/appTokens at org.apache.hadoop.hdfs.DistributedFileSystem.getFileStatus(DistributedFileSystem.java:809)</pre>
同时注意到是因为每次重启nodemanager才发生。  
首先用关键词“apptokens FileNotFoundException”在google和issue搜索没找到相关的问题。
## 猜测原因

可能找不到的原因：1.客户端没上传成功 2.上传成功了，但后面不知道给谁删了
## 重现

既然在网上找不到，尝试在测试环境重现这个问题，运行一个sleep job
<pre escaped="true" lang="bash">cd /opt/cloudera/parcels/CDH/lib/hadoop-mapreduce;
hadoop jar hadoop-mapreduce-client-*-tests.jar sleep -Dmapred.job.queue.name=sleep -m5 -r5 -mt 60000 -rt 30000 -recordt 1000</pre>
重启nodemanage后会发现报错。
## 分析日志

但发现找不到AM的日志，哪里去了？我们的hadoop环境都配置了“日志聚集”(yarn.log-aggregation-enable)，失败的任务就把日志删了(可能是bug)，尝试关掉后，从crontainer日志找到AM日志。  
同时还可以看ResourceManager，NameNode，HDFS审计日志（hdfs-audit.log）  
从AM日志可以看到第一次尝试好像是成功的，从HDFS审计日志发现了删除staging的目录
<pre escaped="true" lang="html">cmd=delete  src=/user/kpi/.staging/job_1405852606905_0013</pre>
到此可以确认目录是被删除了，导致后面的job失败，但谁删了这个目录？
## 继续搜索

代码很多，需要定位一下那里操作.staging这个目录，确定谁删了这个目录。在issue搜索“staging delete”，看有没有相关的操作代码。  
同时阅读代码发现了org.apache.hadoop.mapreduce.v2.app.MRAppMaster.cleanupStagingDir()方法，对照日志，可以确定是这个方法删除了staging目录。
<pre escaped="true" lang="java">public synchronized void stop() {
...
//这里判断了是不是AM的最后一次尝试，如果是才清理
        if(isLastAMRetry) {
          cleanupStagingDir();
        } 
...
  }</pre>
这个逻辑还算正常, 继续找isLastAMRetry是怎么来的
<pre escaped="true" lang="java">public void shutDownJob() {
...
      //We are finishing cleanly so this is the last retry
      isLastAMRetry = true;
      // Stop all services
      // This will also send the final report to the ResourceManager
      LOG.info("Calling stop for all the services");
      MRAppMaster.this.stop();
...
  }</pre>
发现调用了shutDownJob，会把isLastAMRetry设置为true，调用shutDownJob是因为接收到JobFinishEvent事件。  
我们多了一些信息，偷懒在issue继续搜索一下，看有没有人解决了。  
这次找到issue了，https://issues.apache.org/jira/browse/MAPREDUCE-5086
阅读patch，发现之前忽略了RM报的一个错误。
<pre escaped="true" lang="other">org.apache.hadoop.yarn.exceptions.impl.pb.YarnRemoteExceptionPBImpl: Application doesn't exist in cache appattempt_1405852606905_0014_000001</pre>
## 结果

重启nodemanager导致RM的appattempt cache数组删除，JobImpl返回了InternalError，AM认为出错了就没必要重试了，直接置isLastRetry=true。  
修改方式是加了一个状态，表明这是“RM重启”了（注意这里不是nodemanager重启，有一些关联），还可以继续重试。具体修改阅读patch https://issues.apache.org/jira/browse/MAPREDUCE-5086
最后，由于patch修改的版本和我们用的版本不一致，还得需要用我们使用的版本依照它的思路改一遍。