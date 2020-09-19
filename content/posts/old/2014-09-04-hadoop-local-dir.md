---
title: hadoop本地目录相关代码分析
author: fatkun
type: post
date: 2014-09-04T10:23:12+00:00
url: /2014/09/hadoop-local-dir.html
duoshuo_thread_id:
  - 6300410318652703489
wp-syntax-cache-content:
  - |
    a:4:{i:1;s:1644:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">yarn.<span style="color: #006633;">nodemanager</span>.<span style="color: #006633;">disk</span><span style="color: #339933;">-</span>health<span style="color: #339933;">-</span>checker.<span style="color: #006633;">enable</span>     是否开启磁盘健康检查，默认是开启
    yarn.<span style="color: #006633;">nodemanager</span>.<span style="color: #006633;">disk</span><span style="color: #339933;">-</span>health<span style="color: #339933;">-</span>checker.<span style="color: #006633;">interval</span><span style="color: #339933;">-</span>ms 检查间隔时间，默认是<span style="color: #cc66cc;">2</span>分钟
    yarn.<span style="color: #006633;">nodemanager</span>.<span style="color: #006633;">disk</span><span style="color: #339933;">-</span>health<span style="color: #339933;">-</span>checker.<span style="color: #006633;">min</span><span style="color: #339933;">-</span>healthy<span style="color: #339933;">-</span>disks  最少健康磁盘的个数，默认值是<span style="color: #cc66cc;">0.25</span>，如果少于这个值，则把这个节点变成unhealthy</pre></td></tr></table><p class="theCode" style="display:none;">yarn.nodemanager.disk-health-checker.enable     是否开启磁盘健康检查，默认是开启
    yarn.nodemanager.disk-health-checker.interval-ms 检查间隔时间，默认是2分钟
    yarn.nodemanager.disk-health-checker.min-healthy-disks  最少健康磁盘的个数，默认值是0.25，如果少于这个值，则把这个节点变成unhealthy</p></div>
    ";i:2;s:466:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">yarn.<span style="color: #006633;">resourcemanager</span>.<span style="color: #006633;">am</span>.<span style="color: #006633;">max</span><span style="color: #339933;">-</span>retries  AM最大重试次数</pre></td></tr></table><p class="theCode" style="display:none;">yarn.resourcemanager.am.max-retries  AM最大重试次数</p></div>
    ";i:3;s:709:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">mapreduce.<span style="color: #006633;">map</span>.<span style="color: #006633;">maxattempts</span>          map最大重试次数，默认是<span style="color: #cc66cc;">4</span>
    mapreduce.<span style="color: #006633;">reduce</span>.<span style="color: #006633;">maxattempts</span>      reduce最大重试次数，默认是<span style="color: #cc66cc;">4</span></pre></td></tr></table><p class="theCode" style="display:none;">mapreduce.map.maxattempts          map最大重试次数，默认是4
    mapreduce.reduce.maxattempts      reduce最大重试次数，默认是4</p></div>
    ";i:4;s:1771:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">mapreduce.<span style="color: #006633;">job</span>.<span style="color: #006633;">maxtaskfailures</span>.<span style="color: #006633;">per</span>.<span style="color: #006633;">tracker</span>  失败多少次后，加入黑名单，默认是<span style="color: #cc66cc;">3</span>
    yarn.<span style="color: #006633;">app</span>.<span style="color: #006633;">mapreduce</span>.<span style="color: #006633;">am</span>.<span style="color: #006633;">job</span>.<span style="color: #006633;">node</span><span style="color: #339933;">-</span>blacklisting.<span style="color: #006633;">ignore</span><span style="color: #339933;">-</span>threshold<span style="color: #339933;">-</span>node<span style="color: #339933;">-</span>percent  加入黑名单的比例超过这个值时，关闭黑名单，默认是<span style="color: #cc66cc;">33</span>
    yarn.<span style="color: #006633;">app</span>.<span style="color: #006633;">mapreduce</span>.<span style="color: #006633;">am</span>.<span style="color: #006633;">job</span>.<span style="color: #006633;">node</span><span style="color: #339933;">-</span>blacklisting.<span style="color: #006633;">enable</span>  是否使用黑名单，默认<span style="color: #000066; font-weight: bold;">true</span></pre></td></tr></table><p class="theCode" style="display:none;">mapreduce.job.maxtaskfailures.per.tracker  失败多少次后，加入黑名单，默认是3
    yarn.app.mapreduce.am.job.node-blacklisting.ignore-threshold-node-percent  加入黑名单的比例超过这个值时，关闭黑名单，默认是33
    yarn.app.mapreduce.am.job.node-blacklisting.enable  是否使用黑名单，默认true</p></div>
    ";}
categories:
  - hadoop
tags:
  - AppMaster
  - hadoop
  - 本地目录
  - 重试机制

---
最近hadoop本地磁盘总是坏，伴随着有些hadoop job失败，阅读了一些相关的代码。
## 本地磁盘健康检查

NodeManager默认会每两分钟检查本地磁盘（local-dirs），找出那些目录可以使用。注意这里如果判定这个磁盘不可用，则在重启NodeManager之前，就算磁盘好了，也不会把它变成可用。代码在LocalDirsHandlerService，DirectoryCollection。
当好磁盘数少于一定量时，会把这台机器变成unhealthy，将不会再给这台机器分配任务。
参数 ：
<pre lang="java" escaped="true">yarn.nodemanager.disk-health-checker.enable     是否开启磁盘健康检查，默认是开启
yarn.nodemanager.disk-health-checker.interval-ms 检查间隔时间，默认是2分钟
yarn.nodemanager.disk-health-checker.min-healthy-disks  最少健康磁盘的个数，默认值是0.25，如果少于这个值，则把这个节点变成unhealthy</pre>
## 本地磁盘使用

NodeManager会从hdfs下载job.jar等东西，这叫资源本地化。代码在ResourceLocalizationService和DefaultContainerExecutor里。
token文件会使用第一个好的local-dirs，其他的文件会顺序的使用local-dirs，文件可能分散在各个盘上。
##  AppMaster重试

AppMaster重试是由RM触发，代码在RMAppImpl的AttemptFailedTransition事件里。默认重试次数是1次（也就是不重试）
参数：
<pre lang="java" escaped="true">yarn.resourcemanager.am.max-retries  AM最大重试次数</pre>
## TaskAttempt重试

我们的map和reduce任务都是一个个TaskAttempt，TaskAttempt由AppMaster来管理，启动和重启的操作都是由AppMaster来处理。代码在TaskImpl的AttemptFailedTransition里
参数：
<pre lang="java" escaped="true">mapreduce.map.maxattempts          map最大重试次数，默认是4
mapreduce.reduce.maxattempts      reduce最大重试次数，默认是4</pre>
## AppMaster资源分配

AppMaster会定时申请、释放container资源，代码在RMContainerRequestor.containerFailedOnHost
当taskAttempt在一个节点的失败数目超过一定上限（通过参数 mapreduce.job.maxtaskfailures.per.tracker 配置，默认是3），该节点会被加入临时的黑名单，为了防止大量的机器加入黑名单，还有个参数 yarn.app.mapreduce.am.job.node-blacklisting.ignore-threshold-node-percent 设置最多被加入黑名单的比例，默认值是33，当超过33%的机器被加入黑名单，则黑名单将会失效。
加入黑名单后，会让RM回收这台机器的container，申请其他机器的container
参数：
<pre lang="java" escaped="true">mapreduce.job.maxtaskfailures.per.tracker  失败多少次后，加入黑名单，默认是3
yarn.app.mapreduce.am.job.node-blacklisting.ignore-threshold-node-percent  加入黑名单的比例超过这个值时，关闭黑名单，默认是33
yarn.app.mapreduce.am.job.node-blacklisting.enable  是否使用黑名单，默认true
</pre>
## 最终处理

在AM失败重启前，先sleep两分钟，等待磁盘健康检查完成。TaskAttempt有黑名单的方式，由于本地磁盘损坏造成的失败可能会比较少触发。