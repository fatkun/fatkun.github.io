---
title: hdfs exceeds the limit of concurrent xcievers
author: fatkun
type: post
date: 2015-11-23T11:53:49+00:00
url: /2015/11/hdfs-exceeds-the-limit-of-concurrent-xcievers.html
duoshuo_thread_id:
  - 6300410896258695938
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:4980:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #ff0000;">&quot;DataXceiver for client unix:/var/run/hdfs-sockets/dn [Waiting for operation #1]&quot;</span> daemon <span style="color: #007800;">prio</span>=<span style="color: #000000;">10</span> <span style="color: #007800;">tid</span>=0x00007ffc42de9000 <span style="color: #007800;">nid</span>=0x68f8 waiting on condition <span style="color: #7a0874; font-weight: bold;">&#91;</span>0x00007ffacbd1d000<span style="color: #7a0874; font-weight: bold;">&#93;</span>
       java.lang.Thread.State: WAITING <span style="color: #7a0874; font-weight: bold;">&#40;</span>parking<span style="color: #7a0874; font-weight: bold;">&#41;</span>
    	at sun.misc.Unsafe.park<span style="color: #7a0874; font-weight: bold;">&#40;</span>Native Method<span style="color: #7a0874; font-weight: bold;">&#41;</span>
    	- parking to <span style="color: #7a0874; font-weight: bold;">wait</span> <span style="color: #000000; font-weight: bold;">for</span>  <span style="color: #000000; font-weight: bold;">&lt;</span>0x00000007a5d3d568<span style="color: #000000; font-weight: bold;">&gt;</span> <span style="color: #7a0874; font-weight: bold;">&#40;</span>a java.util.concurrent.locks.AbstractQueuedSynchronizer<span style="color: #007800;">$ConditionObject</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
    	at java.util.concurrent.locks.LockSupport.park<span style="color: #7a0874; font-weight: bold;">&#40;</span>LockSupport.java:<span style="color: #000000;">186</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
    	at java.util.concurrent.locks.AbstractQueuedSynchronizer<span style="color: #007800;">$ConditionObject</span>.await<span style="color: #7a0874; font-weight: bold;">&#40;</span>AbstractQueuedSynchronizer.java:<span style="color: #000000;">2043</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
    	at org.apache.hadoop.net.unix.DomainSocketWatcher.add<span style="color: #7a0874; font-weight: bold;">&#40;</span>DomainSocketWatcher.java:<span style="color: #000000;">316</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
    	at org.apache.hadoop.hdfs.server.datanode.ShortCircuitRegistry.createNewMemorySegment<span style="color: #7a0874; font-weight: bold;">&#40;</span>ShortCircuitRegistry.java:<span style="color: #000000;">322</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
    	at org.apache.hadoop.hdfs.server.datanode.DataXceiver.requestShortCircuitShm<span style="color: #7a0874; font-weight: bold;">&#40;</span>DataXceiver.java:<span style="color: #000000;">418</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
    	at org.apache.hadoop.hdfs.protocol.datatransfer.Receiver.opRequestShortCircuitShm<span style="color: #7a0874; font-weight: bold;">&#40;</span>Receiver.java:<span style="color: #000000;">214</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
    	at org.apache.hadoop.hdfs.protocol.datatransfer.Receiver.processOp<span style="color: #7a0874; font-weight: bold;">&#40;</span>Receiver.java:<span style="color: #000000;">95</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
    	at org.apache.hadoop.hdfs.server.datanode.DataXceiver.run<span style="color: #7a0874; font-weight: bold;">&#40;</span>DataXceiver.java:<span style="color: #000000;">241</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
    	at java.lang.Thread.run<span style="color: #7a0874; font-weight: bold;">&#40;</span>Thread.java:<span style="color: #000000;">745</span><span style="color: #7a0874; font-weight: bold;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">&quot;DataXceiver for client unix:/var/run/hdfs-sockets/dn [Waiting for operation #1]&quot; daemon prio=10 tid=0x00007ffc42de9000 nid=0x68f8 waiting on condition [0x00007ffacbd1d000]
       java.lang.Thread.State: WAITING (parking)
    	at sun.misc.Unsafe.park(Native Method)
    	- parking to wait for  &lt;0x00000007a5d3d568&gt; (a java.util.concurrent.locks.AbstractQueuedSynchronizer$ConditionObject)
    	at java.util.concurrent.locks.LockSupport.park(LockSupport.java:186)
    	at java.util.concurrent.locks.AbstractQueuedSynchronizer$ConditionObject.await(AbstractQueuedSynchronizer.java:2043)
    	at org.apache.hadoop.net.unix.DomainSocketWatcher.add(DomainSocketWatcher.java:316)
    	at org.apache.hadoop.hdfs.server.datanode.ShortCircuitRegistry.createNewMemorySegment(ShortCircuitRegistry.java:322)
    	at org.apache.hadoop.hdfs.server.datanode.DataXceiver.requestShortCircuitShm(DataXceiver.java:418)
    	at org.apache.hadoop.hdfs.protocol.datatransfer.Receiver.opRequestShortCircuitShm(Receiver.java:214)
    	at org.apache.hadoop.hdfs.protocol.datatransfer.Receiver.processOp(Receiver.java:95)
    	at org.apache.hadoop.hdfs.server.datanode.DataXceiver.run(DataXceiver.java:241)
    	at java.lang.Thread.run(Thread.java:745)</p></div>
    ";}
categories:
  - hadoop
tags:
  - hadoop
  - hdfs

---
版本: hadoop cdh5.4
datanode jstack，很多这样的线程
<pre lang="bash" escaped="true">"DataXceiver for client unix:/var/run/hdfs-sockets/dn [Waiting for operation #1]" daemon prio=10 tid=0x00007ffc42de9000 nid=0x68f8 waiting on condition [0x00007ffacbd1d000]
   java.lang.Thread.State: WAITING (parking)
	at sun.misc.Unsafe.park(Native Method)
	- parking to wait for  &lt;0x00000007a5d3d568&gt; (a java.util.concurrent.locks.AbstractQueuedSynchronizer$ConditionObject)
	at java.util.concurrent.locks.LockSupport.park(LockSupport.java:186)
	at java.util.concurrent.locks.AbstractQueuedSynchronizer$ConditionObject.await(AbstractQueuedSynchronizer.java:2043)
	at org.apache.hadoop.net.unix.DomainSocketWatcher.add(DomainSocketWatcher.java:316)
	at org.apache.hadoop.hdfs.server.datanode.ShortCircuitRegistry.createNewMemorySegment(ShortCircuitRegistry.java:322)
	at org.apache.hadoop.hdfs.server.datanode.DataXceiver.requestShortCircuitShm(DataXceiver.java:418)
	at org.apache.hadoop.hdfs.protocol.datatransfer.Receiver.opRequestShortCircuitShm(Receiver.java:214)
	at org.apache.hadoop.hdfs.protocol.datatransfer.Receiver.processOp(Receiver.java:95)
	at org.apache.hadoop.hdfs.server.datanode.DataXceiver.run(DataXceiver.java:241)
	at java.lang.Thread.run(Thread.java:745)</pre>
&nbsp;
## 相关issue

[HADOOP-11333] &#8211; Fix deadlock in DomainSocketWatcher when the notification pipe is full  
[HADOOP-10404] &#8211; Some accesses to DomainSocketWatcher#closed are not protected by lock
https://issues.apache.org/jira/browse/HADOOP-11604  
https://issues.apache.org/jira/browse/HADOOP-11802  
https://issues.apache.org/jira/browse/HDFS-8429
&nbsp;