---
title: 使用eclipse调试hive mapreduce
author: fatkun
type: post
date: 2012-10-21T12:12:35+00:00
url: /2012/10/debug-hive-mapreduce-with-eclipse.html
duoshuo_thread_id:
  - 6300408866450440962
wp-syntax-cache-content:
  - |
    a:4:{i:1;s:1319:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>mapred.job.tracker<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>local<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">&lt;property&gt;
    &lt;name&gt;mapred.job.tracker&lt;/name&gt;
    &lt;value&gt;local&lt;/value&gt;
    &lt;/property&gt;</p></div>
    ";i:2;s:1666:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #666666; font-style: italic;">//MapRedTask.java </span>
      <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">int</span> execute<span style="color: #009900;">&#40;</span>DriverContext driverContext<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
           <span style="color: #666666; font-style: italic;">//....</span>
          <span style="color: #666666; font-style: italic;">// Run ExecDriver in another JVM</span>
          executor <span style="color: #339933;">=</span> <span style="color: #003399;">Runtime</span>.<span style="color: #006633;">getRuntime</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">exec</span><span style="color: #009900;">&#40;</span>cmdLine, env, <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">File</span><span style="color: #009900;">&#40;</span>workDir<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
         <span style="color: #666666; font-style: italic;">//....</span>
      <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">//MapRedTask.java 
      public int execute(DriverContext driverContext) {
           //....
          // Run ExecDriver in another JVM
          executor = Runtime.getRuntime().exec(cmdLine, env, new File(workDir));
         //....
      }</p></div>
    ";i:3;s:1921:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">/</span>home<span style="color: #000000; font-weight: bold;">/</span>fatkun<span style="color: #000000; font-weight: bold;">/</span>hadoop<span style="color: #000000; font-weight: bold;">/</span>bin<span style="color: #000000; font-weight: bold;">/</span>hadoop <span style="color: #c20cb9; font-weight: bold;">jar</span> <span style="color: #000000; font-weight: bold;">/</span>home<span style="color: #000000; font-weight: bold;">/</span>fatkun<span style="color: #000000; font-weight: bold;">/</span>local<span style="color: #000000; font-weight: bold;">/</span>hive-0.7.1-cdh3u4<span style="color: #000000; font-weight: bold;">/</span>lib<span style="color: #000000; font-weight: bold;">/</span>hive-exec-0.7.1-cdh3u4.jar org.apache.hadoop.hive.ql.exec.ExecDriver  <span style="color: #660033;">-plan</span> file:<span style="color: #000000; font-weight: bold;">/</span>tmp<span style="color: #000000; font-weight: bold;">/</span>fatkun<span style="color: #000000; font-weight: bold;">/</span>hive_2012-<span style="color: #000000;">10</span>-<span style="color: #000000;">21</span>_19-<span style="color: #000000;">55</span>-<span style="color: #000000;">58</span>_644_8079645408059698793<span style="color: #000000; font-weight: bold;">/</span>-local-<span style="color: #000000;">10002</span><span style="color: #000000; font-weight: bold;">/</span>plan.xml  <span style="color: #660033;">-jobconf</span> ...</pre></td></tr></table><p class="theCode" style="display:none;">/home/fatkun/hadoop/bin/hadoop jar /home/fatkun/local/hive-0.7.1-cdh3u4/lib/hive-exec-0.7.1-cdh3u4.jar org.apache.hadoop.hive.ql.exec.ExecDriver  -plan file:/tmp/fatkun/hive_2012-10-21_19-55-58_644_8079645408059698793/-local-10002/plan.xml  -jobconf ...</p></div>
    ";i:4;s:1639:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #666666; font-style: italic;"># 找到jar这一行</span>
    <span style="color: #000000; font-weight: bold;">elif</span> <span style="color: #7a0874; font-weight: bold;">&#91;</span> <span style="color: #ff0000;">&quot;<span style="color: #007800;">$COMMAND</span>&quot;</span> = <span style="color: #ff0000;">&quot;jar&quot;</span> <span style="color: #7a0874; font-weight: bold;">&#93;</span> ; <span style="color: #000000; font-weight: bold;">then</span>
      <span style="color: #007800;">CLASS</span>=org.apache.hadoop.util.RunJar
      <span style="color: #666666; font-style: italic;"># 加上下面这一行代码用于调试，6666是端口</span>
      <span style="color: #007800;">HADOOP_OPTS</span>=<span style="color: #ff0000;">&quot;<span style="color: #007800;">$HADOOP_OPTS</span> -Xdebug -Xrunjdwp:transport=dt_socket,address=6666,server=y,suspend=y&quot;</span>
      <span style="color: #007800;">HADOOP_OPTS</span>=<span style="color: #ff0000;">&quot;<span style="color: #007800;">$HADOOP_OPTS</span> <span style="color: #007800;">$HADOOP_CLIENT_OPTS</span>&quot;</span></pre></td></tr></table><p class="theCode" style="display:none;"># 找到jar这一行
    elif [ &quot;$COMMAND&quot; = &quot;jar&quot; ] ; then
      CLASS=org.apache.hadoop.util.RunJar
      # 加上下面这一行代码用于调试，6666是端口
      HADOOP_OPTS=&quot;$HADOOP_OPTS -Xdebug -Xrunjdwp:transport=dt_socket,address=6666,server=y,suspend=y&quot;
      HADOOP_OPTS=&quot;$HADOOP_OPTS $HADOOP_CLIENT_OPTS&quot;</p></div>
    ";}
categories:
  - hive
tags:
  - debug
  - hive

---
我们知道Hive经过一些转换后，提交job到hadoop，一般我们只能debug到submitJob这里，而不知道后面那些mapper到底是怎样执行的。如果想要跟踪一下像SelectOperator是怎么处理的怎样做呢？
## 解决方法

### 使用local模式运行

确保配置hive-site.xml中mapred.job.tracker设为local
<pre lang="xml" escaped="true">&lt;property&gt;
&lt;name&gt;mapred.job.tracker&lt;/name&gt;
&lt;value&gt;local&lt;/value&gt;
&lt;/property&gt;</pre>
在hadoop的mapred-site.xml也有mapred.job.tracker配置，我这里也设为了local（不确定是否可以不设置）  
如果设为local，系统会调用命令的方式运行
<pre lang="java" escaped="true">//MapRedTask.java 
  public int execute(DriverContext driverContext) {
       //....
      // Run ExecDriver in another JVM
      executor = Runtime.getRuntime().exec(cmdLine, env, new File(workDir));
     //....
  }</pre>
上面的代码会最终调用这样的命令
<pre lang="bash" escaped="true">/home/fatkun/hadoop/bin/hadoop jar /home/fatkun/local/hive-0.7.1-cdh3u4/lib/hive-exec-0.7.1-cdh3u4.jar org.apache.hadoop.hive.ql.exec.ExecDriver  -plan file:/tmp/fatkun/hive_2012-10-21_19-55-58_644_8079645408059698793/-local-10002/plan.xml  -jobconf ...</pre>
如果这里提示找不到null/bin/hadoop，是环境变量HADOOP\_HOME读取不到的原因，在eclipse的debug environment加上一个HADOOP\_HOME配置。(<a href="http://blog.csdn.net/liwei_1988/article/details/7311691" target="_blank">这里有图</a>)
### 远程 debug hadoop

其实貌似不像远程debug，都是在本地进行的，我们知道上面是通过hadoop jar运行的。拷贝%HADOOP_HOME%/bin/hadoop一个备份出来，然后修改这个文件。
<pre lang="bash" escaped="true"># 找到jar这一行
elif [ "$COMMAND" = "jar" ] ; then
  CLASS=org.apache.hadoop.util.RunJar
  # 加上下面这一行代码用于调试，6666是端口
  HADOOP_OPTS="$HADOOP_OPTS -Xdebug -Xrunjdwp:transport=dt_socket,address=6666,server=y,suspend=y"
  HADOOP_OPTS="$HADOOP_OPTS $HADOOP_CLIENT_OPTS"</pre>
这样，每次调用hadoop jar这个命令时，就会等着eclipse调试了。  
eclipse在Debug configuration配置一个Remote Java Application，端口填6666就可以开始调试了。  
<a href="http://www.lifeba.org/arch/hadoop_debug.html" target="_blank">hadoop调试的更多信息点击这里<br /> </a>这样就可以在ExecMapper.java下断点调试了。
### 远程 debug hadoop 2

  1. 以debug模式启动Cli，${HIVE\_HOME}/bin/hive &#8211;debug。进程会监听在8000端口等待调试连接。如果想更改监听端口，可以修改配置文件:${HIVE\_HOME}bin/ext/debug.sh 。</p> 
  2. 在Eclipse中, 选择Debug configurations->Remote Java Application，填好Host和Port，确定。
  3. 如果Hadoop是0.23以上版本，debug模式启动Cli会报错：ERROR: Cannot load this JVM TI agent twice, check your java command line for duplicate jdwp options.。打开${Hadoop\_HOME}/bin/hadoop，注释掉HADOOP\_OPTS=&#8221;$HADOOP\_OPTS $HADOOP\_CLIENT_OPTS&#8221;即可。
注1：https://issues.apache.org/jira/browse/HIVE-2500
<http://long-xie.iteye.com/blog/1779072>
&nbsp;
在yarn中单步调试时使用local job
    SET mapred.job.tracker=local;
    SET hive.exec.mode.local.auto=true;
    SET fs.defaultFS=file:///; 