---
title: hive-builtins文件找不到
author: fatkun
type: post
date: 2013-06-11T16:57:19+00:00
url: /2013/06/filenotfoundexception-hive-builtins.html
duoshuo_thread_id:
  - 6300410024309031681
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:16089:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">java.<span style="color: #006633;">io</span>.<span style="color: #003399;">FileNotFoundException</span><span style="color: #339933;">:</span> <span style="color: #003399;">File</span> does not exist<span style="color: #339933;">:</span> hdfs<span style="color: #339933;">:</span><span style="color: #666666; font-style: italic;">//localhost:8020/home/fatkun/hive-0.10.0-cdh4.3.0/lib/hive-builtins-0.10.0-cdh4.3.0.jar</span>
    	at org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">hadoop</span>.<span style="color: #006633;">hdfs</span>.<span style="color: #006633;">DistributedFileSystem</span>.<span style="color: #006633;">getFileStatus</span><span style="color: #009900;">&#40;</span>DistributedFileSystem.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">824</span><span style="color: #009900;">&#41;</span>
    	at org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">hadoop</span>.<span style="color: #006633;">mapreduce</span>.<span style="color: #006633;">filecache</span>.<span style="color: #006633;">ClientDistributedCacheManager</span>.<span style="color: #006633;">getFileStatus</span><span style="color: #009900;">&#40;</span>ClientDistributedCacheManager.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">288</span><span style="color: #009900;">&#41;</span>
    	at org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">hadoop</span>.<span style="color: #006633;">mapreduce</span>.<span style="color: #006633;">filecache</span>.<span style="color: #006633;">ClientDistributedCacheManager</span>.<span style="color: #006633;">getFileStatus</span><span style="color: #009900;">&#40;</span>ClientDistributedCacheManager.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">224</span><span style="color: #009900;">&#41;</span>
    	at org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">hadoop</span>.<span style="color: #006633;">mapreduce</span>.<span style="color: #006633;">filecache</span>.<span style="color: #006633;">ClientDistributedCacheManager</span>.<span style="color: #006633;">determineTimestamps</span><span style="color: #009900;">&#40;</span>ClientDistributedCacheManager.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">93</span><span style="color: #009900;">&#41;</span>
    	at org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">hadoop</span>.<span style="color: #006633;">mapreduce</span>.<span style="color: #006633;">filecache</span>.<span style="color: #006633;">ClientDistributedCacheManager</span>.<span style="color: #006633;">determineTimestampsAndCacheVisibilities</span><span style="color: #009900;">&#40;</span>ClientDistributedCacheManager.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">57</span><span style="color: #009900;">&#41;</span>
    	at org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">hadoop</span>.<span style="color: #006633;">mapreduce</span>.<span style="color: #006633;">JobSubmitter</span>.<span style="color: #006633;">copyAndConfigureFiles</span><span style="color: #009900;">&#40;</span>JobSubmitter.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">254</span><span style="color: #009900;">&#41;</span>
    	at org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">hadoop</span>.<span style="color: #006633;">mapreduce</span>.<span style="color: #006633;">JobSubmitter</span>.<span style="color: #006633;">copyAndConfigureFiles</span><span style="color: #009900;">&#40;</span>JobSubmitter.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">290</span><span style="color: #009900;">&#41;</span>
    	at org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">hadoop</span>.<span style="color: #006633;">mapreduce</span>.<span style="color: #006633;">JobSubmitter</span>.<span style="color: #006633;">submitJobInternal</span><span style="color: #009900;">&#40;</span>JobSubmitter.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">361</span><span style="color: #009900;">&#41;</span>
    	at org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">hadoop</span>.<span style="color: #006633;">mapreduce</span>.<span style="color: #006633;">Job</span>$11.<span style="color: #006633;">run</span><span style="color: #009900;">&#40;</span>Job.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">1269</span><span style="color: #009900;">&#41;</span>
    	at org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">hadoop</span>.<span style="color: #006633;">mapreduce</span>.<span style="color: #006633;">Job</span>$11.<span style="color: #006633;">run</span><span style="color: #009900;">&#40;</span>Job.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">1266</span><span style="color: #009900;">&#41;</span>
    	at java.<span style="color: #006633;">security</span>.<span style="color: #003399;">AccessController</span>.<span style="color: #006633;">doPrivileged</span><span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">Native</span> <span style="color: #003399;">Method</span><span style="color: #009900;">&#41;</span>
    	at javax.<span style="color: #006633;">security</span>.<span style="color: #006633;">auth</span>.<span style="color: #006633;">Subject</span>.<span style="color: #006633;">doAs</span><span style="color: #009900;">&#40;</span>Subject.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">396</span><span style="color: #009900;">&#41;</span>
    	at org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">hadoop</span>.<span style="color: #006633;">security</span>.<span style="color: #006633;">UserGroupInformation</span>.<span style="color: #006633;">doAs</span><span style="color: #009900;">&#40;</span>UserGroupInformation.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">1408</span><span style="color: #009900;">&#41;</span>
    	at org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">hadoop</span>.<span style="color: #006633;">mapreduce</span>.<span style="color: #006633;">Job</span>.<span style="color: #006633;">submit</span><span style="color: #009900;">&#40;</span>Job.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">1266</span><span style="color: #009900;">&#41;</span>
    	at org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">hadoop</span>.<span style="color: #006633;">mapred</span>.<span style="color: #006633;">JobClient</span>$1.<span style="color: #006633;">run</span><span style="color: #009900;">&#40;</span>JobClient.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">606</span><span style="color: #009900;">&#41;</span>
    	at org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">hadoop</span>.<span style="color: #006633;">mapred</span>.<span style="color: #006633;">JobClient</span>$1.<span style="color: #006633;">run</span><span style="color: #009900;">&#40;</span>JobClient.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">601</span><span style="color: #009900;">&#41;</span>
    	at java.<span style="color: #006633;">security</span>.<span style="color: #003399;">AccessController</span>.<span style="color: #006633;">doPrivileged</span><span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">Native</span> <span style="color: #003399;">Method</span><span style="color: #009900;">&#41;</span>
    	at javax.<span style="color: #006633;">security</span>.<span style="color: #006633;">auth</span>.<span style="color: #006633;">Subject</span>.<span style="color: #006633;">doAs</span><span style="color: #009900;">&#40;</span>Subject.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">396</span><span style="color: #009900;">&#41;</span>
    	at org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">hadoop</span>.<span style="color: #006633;">security</span>.<span style="color: #006633;">UserGroupInformation</span>.<span style="color: #006633;">doAs</span><span style="color: #009900;">&#40;</span>UserGroupInformation.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">1408</span><span style="color: #009900;">&#41;</span>
    	at org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">hadoop</span>.<span style="color: #006633;">mapred</span>.<span style="color: #006633;">JobClient</span>.<span style="color: #006633;">submitJobInternal</span><span style="color: #009900;">&#40;</span>JobClient.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">601</span><span style="color: #009900;">&#41;</span>
    	at org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">hadoop</span>.<span style="color: #006633;">mapred</span>.<span style="color: #006633;">JobClient</span>.<span style="color: #006633;">submitJob</span><span style="color: #009900;">&#40;</span>JobClient.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">586</span><span style="color: #009900;">&#41;</span>
    	at org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">hadoop</span>.<span style="color: #006633;">hive</span>.<span style="color: #006633;">ql</span>.<span style="color: #006633;">exec</span>.<span style="color: #006633;">ExecDriver</span>.<span style="color: #006633;">execute</span><span style="color: #009900;">&#40;</span>ExecDriver.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">448</span><span style="color: #009900;">&#41;</span>
    	at org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">hadoop</span>.<span style="color: #006633;">hive</span>.<span style="color: #006633;">ql</span>.<span style="color: #006633;">exec</span>.<span style="color: #006633;">ExecDriver</span>.<span style="color: #006633;">main</span><span style="color: #009900;">&#40;</span>ExecDriver.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">690</span><span style="color: #009900;">&#41;</span>
    	at sun.<span style="color: #006633;">reflect</span>.<span style="color: #006633;">NativeMethodAccessorImpl</span>.<span style="color: #006633;">invoke0</span><span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">Native</span> <span style="color: #003399;">Method</span><span style="color: #009900;">&#41;</span>
    	at sun.<span style="color: #006633;">reflect</span>.<span style="color: #006633;">NativeMethodAccessorImpl</span>.<span style="color: #006633;">invoke</span><span style="color: #009900;">&#40;</span>NativeMethodAccessorImpl.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">39</span><span style="color: #009900;">&#41;</span>
    	at sun.<span style="color: #006633;">reflect</span>.<span style="color: #006633;">DelegatingMethodAccessorImpl</span>.<span style="color: #006633;">invoke</span><span style="color: #009900;">&#40;</span>DelegatingMethodAccessorImpl.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">25</span><span style="color: #009900;">&#41;</span>
    	at java.<span style="color: #006633;">lang</span>.<span style="color: #006633;">reflect</span>.<span style="color: #003399;">Method</span>.<span style="color: #006633;">invoke</span><span style="color: #009900;">&#40;</span><span style="color: #003399;">Method</span>.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">597</span><span style="color: #009900;">&#41;</span>
    	at org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">hadoop</span>.<span style="color: #006633;">util</span>.<span style="color: #006633;">RunJar</span>.<span style="color: #006633;">main</span><span style="color: #009900;">&#40;</span>RunJar.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">208</span><span style="color: #009900;">&#41;</span>
    Job Submission failed with exception <span style="color: #0000ff;">'java.io.FileNotFoundException(File does not exist: hdfs://localhost:8020/home/fatkun/hive-0.10.0-cdh4.3.0/lib/hive-builtins-0.10.0-cdh4.3.0.jar)'</span></pre></td></tr></table><p class="theCode" style="display:none;">java.io.FileNotFoundException: File does not exist: hdfs://localhost:8020/home/fatkun/hive-0.10.0-cdh4.3.0/lib/hive-builtins-0.10.0-cdh4.3.0.jar
    	at org.apache.hadoop.hdfs.DistributedFileSystem.getFileStatus(DistributedFileSystem.java:824)
    	at org.apache.hadoop.mapreduce.filecache.ClientDistributedCacheManager.getFileStatus(ClientDistributedCacheManager.java:288)
    	at org.apache.hadoop.mapreduce.filecache.ClientDistributedCacheManager.getFileStatus(ClientDistributedCacheManager.java:224)
    	at org.apache.hadoop.mapreduce.filecache.ClientDistributedCacheManager.determineTimestamps(ClientDistributedCacheManager.java:93)
    	at org.apache.hadoop.mapreduce.filecache.ClientDistributedCacheManager.determineTimestampsAndCacheVisibilities(ClientDistributedCacheManager.java:57)
    	at org.apache.hadoop.mapreduce.JobSubmitter.copyAndConfigureFiles(JobSubmitter.java:254)
    	at org.apache.hadoop.mapreduce.JobSubmitter.copyAndConfigureFiles(JobSubmitter.java:290)
    	at org.apache.hadoop.mapreduce.JobSubmitter.submitJobInternal(JobSubmitter.java:361)
    	at org.apache.hadoop.mapreduce.Job$11.run(Job.java:1269)
    	at org.apache.hadoop.mapreduce.Job$11.run(Job.java:1266)
    	at java.security.AccessController.doPrivileged(Native Method)
    	at javax.security.auth.Subject.doAs(Subject.java:396)
    	at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1408)
    	at org.apache.hadoop.mapreduce.Job.submit(Job.java:1266)
    	at org.apache.hadoop.mapred.JobClient$1.run(JobClient.java:606)
    	at org.apache.hadoop.mapred.JobClient$1.run(JobClient.java:601)
    	at java.security.AccessController.doPrivileged(Native Method)
    	at javax.security.auth.Subject.doAs(Subject.java:396)
    	at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1408)
    	at org.apache.hadoop.mapred.JobClient.submitJobInternal(JobClient.java:601)
    	at org.apache.hadoop.mapred.JobClient.submitJob(JobClient.java:586)
    	at org.apache.hadoop.hive.ql.exec.ExecDriver.execute(ExecDriver.java:448)
    	at org.apache.hadoop.hive.ql.exec.ExecDriver.main(ExecDriver.java:690)
    	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
    	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:39)
    	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:25)
    	at java.lang.reflect.Method.invoke(Method.java:597)
    	at org.apache.hadoop.util.RunJar.main(RunJar.java:208)
    Job Submission failed with exception 'java.io.FileNotFoundException(File does not exist: hdfs://localhost:8020/home/fatkun/hive-0.10.0-cdh4.3.0/lib/hive-builtins-0.10.0-cdh4.3.0.jar)'</p></div>
    ";i:2;s:4002:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"> <span style="color: #666666; font-style: italic;">//ql/src/java/org/apache/hadoop/hive/ql/session/SessionState.java</span>
    &nbsp;
       <span style="color: #666666; font-style: italic;">// Register the Hive builtins jar and all of its functions</span>
        <span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#123;</span>
          Class<span style="color: #339933;">&lt;?&gt;</span> pluginClass <span style="color: #339933;">=</span> <span style="color: #003399;">Utilities</span>.<span style="color: #006633;">getBuiltinUtilsClass</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #003399;">URL</span> jarLocation <span style="color: #339933;">=</span> pluginClass.<span style="color: #006633;">getProtectionDomain</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getCodeSource</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>
            .<span style="color: #006633;">getLocation</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          add_builtin_resource<span style="color: #009900;">&#40;</span>
            ResourceType.<span style="color: #006633;">JAR</span>, jarLocation.<span style="color: #006633;">toString</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          FunctionRegistry.<span style="color: #006633;">registerFunctionsFromPluginJar</span><span style="color: #009900;">&#40;</span>
            jarLocation, pluginClass.<span style="color: #006633;">getClassLoader</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          sessionFunctionRegistry.<span style="color: #006633;">putAll</span><span style="color: #009900;">&#40;</span>FunctionRegistry.<span style="color: #006633;">getStaticFunctionRegistry</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">Exception</span> ex<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #000000; font-weight: bold;">throw</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">RuntimeException</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Failed to load Hive builtin functions&quot;</span>, ex<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;"> //ql/src/java/org/apache/hadoop/hive/ql/session/SessionState.java
    
       // Register the Hive builtins jar and all of its functions
        try {
          Class&lt;?&gt; pluginClass = Utilities.getBuiltinUtilsClass();
          URL jarLocation = pluginClass.getProtectionDomain().getCodeSource()
            .getLocation();
          add_builtin_resource(
            ResourceType.JAR, jarLocation.toString());
          FunctionRegistry.registerFunctionsFromPluginJar(
            jarLocation, pluginClass.getClassLoader());
          sessionFunctionRegistry.putAll(FunctionRegistry.getStaticFunctionRegistry());
        } catch (Exception ex) {
          throw new RuntimeException(&quot;Failed to load Hive builtin functions&quot;, ex);
        }</p></div>
    ";i:3;s:1346:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;">  <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>fs.default.name<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>file:///<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">  &lt;property&gt;
        &lt;name&gt;fs.default.name&lt;/name&gt;
        &lt;value&gt;file:///&lt;/value&gt;
      &lt;/property&gt;</p></div>
    ";}
categories:
  - hive
tags:
  - FileNotFoundException
  - hive
  - hive-builtins

---
<pre escaped="true" lang="java">java.io.FileNotFoundException: File does not exist: hdfs://localhost:8020/home/fatkun/hive-0.10.0-cdh4.3.0/lib/hive-builtins-0.10.0-cdh4.3.0.jar
	at org.apache.hadoop.hdfs.DistributedFileSystem.getFileStatus(DistributedFileSystem.java:824)
	at org.apache.hadoop.mapreduce.filecache.ClientDistributedCacheManager.getFileStatus(ClientDistributedCacheManager.java:288)
	at org.apache.hadoop.mapreduce.filecache.ClientDistributedCacheManager.getFileStatus(ClientDistributedCacheManager.java:224)
	at org.apache.hadoop.mapreduce.filecache.ClientDistributedCacheManager.determineTimestamps(ClientDistributedCacheManager.java:93)
	at org.apache.hadoop.mapreduce.filecache.ClientDistributedCacheManager.determineTimestampsAndCacheVisibilities(ClientDistributedCacheManager.java:57)
	at org.apache.hadoop.mapreduce.JobSubmitter.copyAndConfigureFiles(JobSubmitter.java:254)
	at org.apache.hadoop.mapreduce.JobSubmitter.copyAndConfigureFiles(JobSubmitter.java:290)
	at org.apache.hadoop.mapreduce.JobSubmitter.submitJobInternal(JobSubmitter.java:361)
	at org.apache.hadoop.mapreduce.Job$11.run(Job.java:1269)
	at org.apache.hadoop.mapreduce.Job$11.run(Job.java:1266)
	at java.security.AccessController.doPrivileged(Native Method)
	at javax.security.auth.Subject.doAs(Subject.java:396)
	at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1408)
	at org.apache.hadoop.mapreduce.Job.submit(Job.java:1266)
	at org.apache.hadoop.mapred.JobClient$1.run(JobClient.java:606)
	at org.apache.hadoop.mapred.JobClient$1.run(JobClient.java:601)
	at java.security.AccessController.doPrivileged(Native Method)
	at javax.security.auth.Subject.doAs(Subject.java:396)
	at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1408)
	at org.apache.hadoop.mapred.JobClient.submitJobInternal(JobClient.java:601)
	at org.apache.hadoop.mapred.JobClient.submitJob(JobClient.java:586)
	at org.apache.hadoop.hive.ql.exec.ExecDriver.execute(ExecDriver.java:448)
	at org.apache.hadoop.hive.ql.exec.ExecDriver.main(ExecDriver.java:690)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:39)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:25)
	at java.lang.reflect.Method.invoke(Method.java:597)
	at org.apache.hadoop.util.RunJar.main(RunJar.java:208)
Job Submission failed with exception 'java.io.FileNotFoundException(File does not exist: hdfs://localhost:8020/home/fatkun/hive-0.10.0-cdh4.3.0/lib/hive-builtins-0.10.0-cdh4.3.0.jar)'</pre>
## 可能的原因

刚开始我用伪分布模式没有提示这个错误，我配置了mapred-site.xml为local模式，但core-site.xml使用hdfs，从hdfs找不到这个文件。
## 可能的代码

<pre escaped="true" lang="java">//ql/src/java/org/apache/hadoop/hive/ql/session/SessionState.java

   // Register the Hive builtins jar and all of its functions
    try {
      Class&lt;?&gt; pluginClass = Utilities.getBuiltinUtilsClass();
      URL jarLocation = pluginClass.getProtectionDomain().getCodeSource()
        .getLocation();
      add_builtin_resource(
        ResourceType.JAR, jarLocation.toString());
      FunctionRegistry.registerFunctionsFromPluginJar(
        jarLocation, pluginClass.getClassLoader());
      sessionFunctionRegistry.putAll(FunctionRegistry.getStaticFunctionRegistry());
    } catch (Exception ex) {
      throw new RuntimeException("Failed to load Hive builtin functions", ex);
    }
</pre>
## 解决方法

方法一：  
更改core.site.xml，把fs.default.name改成local
<pre escaped="true" lang="xml">&lt;property&gt;
    &lt;name&gt;fs.default.name&lt;/name&gt;
    &lt;value&gt;file:///&lt;/value&gt;
  &lt;/property&gt;
</pre>
方法二（没试过）：  
把hive-builtins包上传到提示的hdfs路径（我这里是/home/fatkun/hive-0.10.0-cdh4.3.0/lib/）  
$ hadoop fs -mkdir /home/fatkun/hive-0.10.0-cdh4.3.0/lib/  
$ hadoop fs -put $HIVE_HOME/lib/hive-builtins-*.jar /home/fatkun/hive-0.10.0-cdh4.3.0/lib/
## 参考

[FileNotFoundException for hive/lib/hive-builtins-0.9.0.jar in Hive][1]

 [1]: http://stackoverflow.com/questions/13527377/filenotfoundexception-for-hive-lib-hive-builtins-0-9-0-jar-in-hive