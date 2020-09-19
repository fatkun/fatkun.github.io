---
title: 在reduce InMemoryMapOutput OOM
author: fatkun
type: post
date: 2017-03-15T07:54:22+00:00
url: /2017/03/reduce-inmemorymapoutput-oom.html
duoshuo_thread_id:
  - 6397630859825906433
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:3191:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="other" style="font-family:monospace;">2017-03-14 15:41:52,724 WARN [main] org.apache.hadoop.mapred.YarnChild: Exception running child : org.apache.hadoop.mapreduce.task.reduce.Shuffle$ShuffleError: error in shuffle in fetcher#1
    	at org.apache.hadoop.mapreduce.task.reduce.Shuffle.run(Shuffle.java:134)
    	at org.apache.hadoop.mapred.ReduceTask.run(ReduceTask.java:376)
    	at org.apache.hadoop.mapred.YarnChild$2.run(YarnChild.java:164)
    	at java.security.AccessController.doPrivileged(Native Method)
    	at javax.security.auth.Subject.doAs(Subject.java:415)
    	at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1693)
    	at org.apache.hadoop.mapred.YarnChild.main(YarnChild.java:158)
    Caused by: java.lang.OutOfMemoryError: Java heap space
    	at org.apache.hadoop.io.BoundedByteArrayOutputStream.&lt;init&gt;(BoundedByteArrayOutputStream.java:56)
    	at org.apache.hadoop.io.BoundedByteArrayOutputStream.&lt;init&gt;(BoundedByteArrayOutputStream.java:46)
    	at org.apache.hadoop.mapreduce.task.reduce.InMemoryMapOutput.&lt;init&gt;(InMemoryMapOutput.java:63)
    	at org.apache.hadoop.mapreduce.task.reduce.MergeManagerImpl.unconditionalReserve(MergeManagerImpl.java:305)
    	at org.apache.hadoop.mapreduce.task.reduce.MergeManagerImpl.reserve(MergeManagerImpl.java:295)
    	at org.apache.hadoop.mapreduce.task.reduce.Fetcher.copyMapOutput(Fetcher.java:514)
    	at org.apache.hadoop.mapreduce.task.reduce.Fetcher.copyFromHost(Fetcher.java:336)
    	at org.apache.hadoop.mapreduce.task.reduce.Fetcher.run(Fetcher.java:193)</pre></td></tr></table><p class="theCode" style="display:none;">2017-03-14 15:41:52,724 WARN [main] org.apache.hadoop.mapred.YarnChild: Exception running child : org.apache.hadoop.mapreduce.task.reduce.Shuffle$ShuffleError: error in shuffle in fetcher#1
    	at org.apache.hadoop.mapreduce.task.reduce.Shuffle.run(Shuffle.java:134)
    	at org.apache.hadoop.mapred.ReduceTask.run(ReduceTask.java:376)
    	at org.apache.hadoop.mapred.YarnChild$2.run(YarnChild.java:164)
    	at java.security.AccessController.doPrivileged(Native Method)
    	at javax.security.auth.Subject.doAs(Subject.java:415)
    	at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1693)
    	at org.apache.hadoop.mapred.YarnChild.main(YarnChild.java:158)
    Caused by: java.lang.OutOfMemoryError: Java heap space
    	at org.apache.hadoop.io.BoundedByteArrayOutputStream.&lt;init&gt;(BoundedByteArrayOutputStream.java:56)
    	at org.apache.hadoop.io.BoundedByteArrayOutputStream.&lt;init&gt;(BoundedByteArrayOutputStream.java:46)
    	at org.apache.hadoop.mapreduce.task.reduce.InMemoryMapOutput.&lt;init&gt;(InMemoryMapOutput.java:63)
    	at org.apache.hadoop.mapreduce.task.reduce.MergeManagerImpl.unconditionalReserve(MergeManagerImpl.java:305)
    	at org.apache.hadoop.mapreduce.task.reduce.MergeManagerImpl.reserve(MergeManagerImpl.java:295)
    	at org.apache.hadoop.mapreduce.task.reduce.Fetcher.copyMapOutput(Fetcher.java:514)
    	at org.apache.hadoop.mapreduce.task.reduce.Fetcher.copyFromHost(Fetcher.java:336)
    	at org.apache.hadoop.mapreduce.task.reduce.Fetcher.run(Fetcher.java:193)</p></div>
    ";}
categories:
  - hadoop

---
<pre escaped="true" lang="other">2017-03-14 15:41:52,724 WARN [main] org.apache.hadoop.mapred.YarnChild: Exception running child : org.apache.hadoop.mapreduce.task.reduce.Shuffle$ShuffleError: error in shuffle in fetcher#1
	at org.apache.hadoop.mapreduce.task.reduce.Shuffle.run(Shuffle.java:134)
	at org.apache.hadoop.mapred.ReduceTask.run(ReduceTask.java:376)
	at org.apache.hadoop.mapred.YarnChild$2.run(YarnChild.java:164)
	at java.security.AccessController.doPrivileged(Native Method)
	at javax.security.auth.Subject.doAs(Subject.java:415)
	at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1693)
	at org.apache.hadoop.mapred.YarnChild.main(YarnChild.java:158)
Caused by: java.lang.OutOfMemoryError: Java heap space
	at org.apache.hadoop.io.BoundedByteArrayOutputStream.&lt;init&gt;(BoundedByteArrayOutputStream.java:56)
	at org.apache.hadoop.io.BoundedByteArrayOutputStream.&lt;init&gt;(BoundedByteArrayOutputStream.java:46)
	at org.apache.hadoop.mapreduce.task.reduce.InMemoryMapOutput.&lt;init&gt;(InMemoryMapOutput.java:63)
	at org.apache.hadoop.mapreduce.task.reduce.MergeManagerImpl.unconditionalReserve(MergeManagerImpl.java:305)
	at org.apache.hadoop.mapreduce.task.reduce.MergeManagerImpl.reserve(MergeManagerImpl.java:295)
	at org.apache.hadoop.mapreduce.task.reduce.Fetcher.copyMapOutput(Fetcher.java:514)
	at org.apache.hadoop.mapreduce.task.reduce.Fetcher.copyFromHost(Fetcher.java:336)
	at org.apache.hadoop.mapreduce.task.reduce.Fetcher.run(Fetcher.java:193)</pre>
调整这个参数 ( mapreduce.reduce.shuffle.input.percent )，默认值为0.7，改为0.5 
相关的参数 mapreduce.reduce.shuffle.memory.limit.percent 一个单一的shuffle的最大内存使用限制