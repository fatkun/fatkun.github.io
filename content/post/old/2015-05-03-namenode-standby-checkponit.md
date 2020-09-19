---
title: namenode standby checkponit时间过长导致的问题
author: fatkun
type: post
date: 2015-05-03T13:30:28+00:00
url: /2015/05/namenode-standby-checkponit.html
duoshuo_thread_id:
  - 6300410882077754114
categories:
  - hadoop
tags:
  - hadoop
  - hdfs

---
我们当前使用的版本是cdh-4.2.1，standby namenode默认每小时生成一个editlog文件，由于操作很多，这个保存时间超过了1分钟。这里面使用了一些读写锁，导致阻塞了其他的一些请求。
## HDFS HA的实现

要理解整个过程，先来看看是如何实现hdfs ha的，我自己不懂，只能看其他大神的文章了。
[Hadoop 2.0 NameNode HA和Federation实践][1]
[Hadoop目前的HA(High Availability)机制分析和源代码研究(1)][2]
[基于QJM/Qurom Journal Manager/Paxos的HDFS HA原理及代码分析][3]
还有一些fsimage、editlog的文章见: <http://yanbohappy.sinaapp.com/?tag=hdfs>
概括一下：
  * fsimage是历史的元数据，会定期把editlog合并进来，editlog是最近一段时间对namenode的操作，当前的文件状态等于fsimage+editlog
  * Datanode会同时向两个Namenode汇报块信息
  * 保证在一个时间内，客户端只会连接active Namenode，由active Namenode负责写editlog（写入QJM），standby Namenode从QJM中获取editlog，更新自己内存中的块信息。这样当standby 变成active时，只用合并最近一小段时间的editlog就可以提供服务了。
  * 客户端根据抛出的异常(StandbyException)来切换连接的namenode
  * 隔离(fence)，需要避免同时存在两个active Namenode，同时服务，同时往QJM写editlog
  * 为了避免namenode启动时合并fsimage和editlog时间过长，standby Namenode 负责定期合并editlog，生成新的fsimage，并且同步给active Namenode。(StandbyCheckpointer)
cdh4.2.1
回到原来的问题，在checkpoint时，FSNamesystem有一个ReentrantReadWriteLock fslock，它包含一个读写锁。
读锁时，允许其他线程读，但写操作会被阻塞。
写锁时，其他线程的读写都会被阻塞。
cdh4.2.1版本的代码在checkpoint时，会加上writelock，导致一些rpc操作需要readlock被阻塞。当时检查日志发现failover controller的心跳RPC请求被阻塞了，但没找到它用到这个锁。后来发现NameNodeRpcServer里public synchronized void monitorHealth()方法使用了synchronized，同时还有public synchronized HAServiceStatus getServiceStatus()等方法，在这个类中，同时只允许进入一个synchronized的方法内。在checkpoint期间，getServiceStatus使用了readLock，导致monitorHealth也被阻塞住。
## HDFS-5064

[Standby checkpoints should not block concurrent readers][4]
找到的第一个补丁是这个，主要修改是在checkpoint的过程中，不应该阻塞那些读操作（如getServiceStatus、monitorHealth）。专门给checkpoint增加了一个读锁fsLongReadLock，在writeLock方法先锁定fsLongReadLock
## HDFS-7097

但是这样修改后，依然会阻塞一些需要writeLock的操作，然后有了新的patch
<p id="summary-val">  <a href="https://issues.apache.org/jira/browse/HDFS-7097">Allow block reports to be processed during checkpointing on standby name node</a></p>
Since block reports are not modifying any state that is being saved to fsimage, I propose letting them through during checkpointing.
补丁作者说&#8221;块汇报&#8221;不改变任何保存在fsimage的状态，所以允许在checkpoint期间执行块报告。（<del><strong>没看懂为什么不影响</strong>，代码中好像是把当前的FSNameSystem持久化为文件，而block report也会操作FSNameSystem&#8230;有可能我理解错了</del>）
这次修改也是新加了一个锁，去掉了上一个补丁的fsLongReadLock，换为cpLock，但是没有在writeLock中先锁定cpLock。
&nbsp;
update: 2015-05-05
fsimage的存储结构可以看这篇文章，[NameNode启动过程详细剖析][5]
  * block mapping(block ID <=> DN location)没有存储在fsimage内，只是保留在内存。
  * block report汇报每个block在datanode的状况(block id <-> localtion)
  * fsimage里面存储的只是blockid
&nbsp;

 [1]: http://www.infoq.com/cn/articles/hadoop-2-0-namenode-ha-federation-practice-zh
 [2]: http://yanbohappy.sinaapp.com/?p=50
 [3]: http://yanbohappy.sinaapp.com/?p=205
 [4]: https://issues.apache.org/jira/browse/HDFS-5064
 [5]: http://blog.csdn.net/myproudcodelife/article/details/41999993