---
title: 在eclipse远程调试mapreduce（hadoop2）
author: fatkun
type: post
date: 2014-02-22T08:13:20+00:00
url: /2014/02/debug-mapreduce-with-eclipse.html
duoshuo_thread_id:
  - 6300410061155992321
wp-syntax-cache-content:
  - |
    a:8:{i:1;s:6000:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>mapreduce.jobtracker.staging.root.dir<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>/tmp<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
       <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>yarn.app.mapreduce.am.staging-dir<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>/tmp<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>mapreduce.framework.name<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>local<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>mapreduce.jobtracker.address<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>local<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>mapred.job.tracker<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>local<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">&lt;property&gt;
        &lt;name&gt;mapreduce.jobtracker.staging.root.dir&lt;/name&gt;
        &lt;value&gt;/tmp&lt;/value&gt;
      &lt;/property&gt;
       &lt;property&gt;
        &lt;name&gt;yarn.app.mapreduce.am.staging-dir&lt;/name&gt;
        &lt;value&gt;/tmp&lt;/value&gt;
      &lt;/property&gt;
      &lt;property&gt;
        &lt;name&gt;mapreduce.framework.name&lt;/name&gt;
        &lt;value&gt;local&lt;/value&gt;
      &lt;/property&gt;
      &lt;property&gt;
        &lt;name&gt;mapreduce.jobtracker.address&lt;/name&gt;
        &lt;value&gt;local&lt;/value&gt;
      &lt;/property&gt;
    &lt;property&gt;
    &lt;name&gt;mapred.job.tracker&lt;/name&gt;
    &lt;value&gt;local&lt;/value&gt;
    &lt;/property&gt;</p></div>
    ";i:2;s:453:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;">export HADOOP_CLIENT_OPTS=&quot;$HADOOP_CLIENT_OPTS -agentlib:jdwp=transport=dt_socket,server=y,suspend=y,address=52902&quot;</pre></td></tr></table><p class="theCode" style="display:none;">export HADOOP_CLIENT_OPTS=&quot;$HADOOP_CLIENT_OPTS -agentlib:jdwp=transport=dt_socket,server=y,suspend=y,address=52902&quot;</p></div>
    ";i:3;s:427:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">hadoop <span style="color: #660033;">--config</span> .<span style="color: #000000; font-weight: bold;">/</span>conf <span style="color: #c20cb9; font-weight: bold;">jar</span> xx.jar xxx</pre></td></tr></table><p class="theCode" style="display:none;">hadoop --config ./conf jar xx.jar xxx</p></div>
    ";i:4;s:484:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #007800;">YARN_NODEMANAGER_OPTS</span>=<span style="color: #ff0000;">&quot;-Xdebug -Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=8092&quot;</span></pre></td></tr></table><p class="theCode" style="display:none;">YARN_NODEMANAGER_OPTS=&quot;-Xdebug -Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=8092&quot;</p></div>
    ";i:5;s:562:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #7a0874; font-weight: bold;">export</span> <span style="color: #007800;">YARN_RESOURCEMANAGER_OPTS</span>=<span style="color: #ff0000;">&quot;-Xdebug -Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=8091&quot;</span></pre></td></tr></table><p class="theCode" style="display:none;">export YARN_RESOURCEMANAGER_OPTS=&quot;-Xdebug -Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=8091&quot;</p></div>
    ";i:6;s:1520:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;">  <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>yarn.app.mapreduce.am.command-opts<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span> -Xmx512m -agentlib:jdwp=transport=dt_socket,server=y,suspend=y,address=8314<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">  &lt;property&gt;
        &lt;name&gt;yarn.app.mapreduce.am.command-opts&lt;/name&gt;
        &lt;value&gt; -Xmx512m -agentlib:jdwp=transport=dt_socket,server=y,suspend=y,address=8314&lt;/value&gt;
      &lt;/property&gt;</p></div>
    ";i:7;s:265:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">hive <span style="color: #660033;">--debug</span></pre></td></tr></table><p class="theCode" style="display:none;">hive --debug</p></div>
    ";i:8;s:984:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">SET mapred.<span style="color: #006633;">job</span>.<span style="color: #006633;">tracker</span><span style="color: #339933;">=</span>local<span style="color: #339933;">;</span>
    SET hive.<span style="color: #006633;">exec</span>.<span style="color: #006633;">mode</span>.<span style="color: #006633;">local</span>.<span style="color: #006633;">auto</span><span style="color: #339933;">=</span><span style="color: #000066; font-weight: bold;">true</span><span style="color: #339933;">;</span>
    SET fs.<span style="color: #006633;">defaultFS</span><span style="color: #339933;">=</span>file<span style="color: #339933;">:</span><span style="color: #666666; font-style: italic;">///;</span></pre></td></tr></table><p class="theCode" style="display:none;">SET mapred.job.tracker=local;
    SET hive.exec.mode.local.auto=true;
    SET fs.defaultFS=file:///;</p></div>
    ";}
categories:
  - hadoop
tags:
  - debug
  - hadoop
  - 远程调试

---
## 背景

线上的服务器都是linux，直接在线上debug不需要准备太多测试数据。
## 实现

远程调试实际上实在服务端开启一个监听端口，通过eclipse连接进行debug。调试mapreduce程序需要修改配置，让mapreduce就在本机运行。从hadoop拷贝一份配置出来，修改mapper-site.xml配置（基于hadoop2配置说明）
<pre lang="xml" escaped="true">&lt;property&gt;
    &lt;name&gt;mapreduce.jobtracker.staging.root.dir&lt;/name&gt;
    &lt;value&gt;/tmp&lt;/value&gt;
  &lt;/property&gt;
   &lt;property&gt;
    &lt;name&gt;yarn.app.mapreduce.am.staging-dir&lt;/name&gt;
    &lt;value&gt;/tmp&lt;/value&gt;
  &lt;/property&gt;
  &lt;property&gt;
    &lt;name&gt;mapreduce.framework.name&lt;/name&gt;
    &lt;value&gt;local&lt;/value&gt;
  &lt;/property&gt;
  &lt;property&gt;
    &lt;name&gt;mapreduce.jobtracker.address&lt;/name&gt;
    &lt;value&gt;local&lt;/value&gt;
  &lt;/property&gt;
&lt;property&gt;
&lt;name&gt;mapred.job.tracker&lt;/name&gt;
&lt;value&gt;local&lt;/value&gt;
&lt;/property&gt;</pre>
注意检查这些标签是不是都有了。。可以放到最后覆盖原来的值
在hadoop-env.sh加上，这里的address=52902是监听的端口，suspend=y表示等待我们连接才继续执行下去
<pre lang="xml" escaped="true">export HADOOP_CLIENT_OPTS="$HADOOP_CLIENT_OPTS -agentlib:jdwp=transport=dt_socket,server=y,suspend=y,address=52902"</pre>
执行hadoop程序，指定配置文件目录为我们改过的配置目录
<pre lang="bash" escaped="true">hadoop --config ./conf jar xx.jar xxx</pre>
最后，在eclipse的debug configuration新增一个remote java application，填入IP和端口，点击debug即可。
## 调试NodeManager

在yarn-env.sh加入
<pre escaped="true" lang="bash">YARN_NODEMANAGER_OPTS="-Xdebug -Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=8092"</pre>
## 调试ResouceManager

在yarn-env.sh加入
<pre escaped="true" lang="bash">export YARN_RESOURCEMANAGER_OPTS="-Xdebug -Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=8091"</pre>
## 调试appMaster

设置只有一台nodemanager，在mapred-site.xml 加入
<pre lang="xml" escaped="true">&lt;property&gt;
    &lt;name&gt;yarn.app.mapreduce.am.command-opts&lt;/name&gt;
    &lt;value&gt; -Xmx512m -agentlib:jdwp=transport=dt_socket,server=y,suspend=y,address=8314&lt;/value&gt;
  &lt;/property&gt;</pre>
如果不可以，试多几次。。不知道为什么。检查一下进程有没有启动。 ps aux|grep MRAppMaster
## 不足

不能调试一个jar包有两个job，执行到第二个job时会报错，可能原因是HADOOP\_CLIENT\_OPTS被加载了两次，并且第二个job启动时需要更换端口，否则会冲突。  
不是很清楚hadoop LocalJobRunner是怎样调用的，并且暂时没调试第二个job就不深究了。
## 远程调试hive

执行命令，会启动监听端口8000
<pre lang="bash" escaped="true">hive --debug</pre>
如果报错，<span style="color: #555555;">ERROR: Cannot load this JVM TI agent twice, check your java command line for duplicate jdwp options.。打开${Hadoop_HOME}/bin/hadoop，注释掉HADOOP_OPTS=”$HADOOP_OPTS $HADOOP_CLIENT_OPTS”</span>
在hive输入以下命令，在单机执行
<pre lang="java" escaped="true">SET mapred.job.tracker=local;
SET hive.exec.mode.local.auto=true;
SET fs.defaultFS=file:///;</pre>
&nbsp;
打印日志
<pre class="lang-java prettyprint prettyprinted"><code>&lt;span class="pln">hive &lt;/span>&lt;span class="pun">--&lt;/span>&lt;span class="pln">hiveconf hive&lt;/span>&lt;span class="pun">.&lt;/span>&lt;span class="pln">root&lt;/span>&lt;span class="pun">.&lt;/span>&lt;span class="pln">logger&lt;/span>&lt;span class="pun">=&lt;/span>&lt;span class="pln">DEBUG&lt;/span>&lt;span class="pun">,&lt;/span>&lt;span class="pln">console&lt;/span></code></pre>
via: http://fatkun.com/2012/10/debug-hive-mapreduce-with-eclipse.html
## 参考

<a title="hadoop2.2.0 源码远程调试" href="http://blog.sina.com.cn/s/blog_5ccc692d0101pikf.html" target="_blank">hadoop2.2.0 源码远程调试</a> 这里有图  
http://www.aboutyun.com/thread-6504-1-1.html