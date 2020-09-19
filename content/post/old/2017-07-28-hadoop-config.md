---
title: hadoop参数
author: fatkun
type: post
date: 2017-07-28T03:06:10+00:00
url: /2017/07/hadoop-config.html
categories:
  - hadoop

---
## YARN

<table>  <tr>    <td style="width: 575px;">      参数    </td>
    <td style="width: 72px;">      默认值    </td>
    <td style="width: 10px;">      值    </td>
    <td style="width: 477px;">      备注    </td>  </tr>
  <tr>    <td style="width: 575px;">      yarn.nodemanager.container-metrics.enable    </td>
    <td style="width: 72px;">    </td>
    <td style="width: 10px;">      false    </td>
    <td style="width: 477px;">      关闭，避免nodemanager内存OOM，http://hackershell.cn/?p=993    </td>  </tr>
  <tr>    <td style="width: 575px;">      yarn.resourcemanager.recovery.enabled    </td>
    <td style="width: 72px;">    </td>
    <td style="width: 10px;">      true    </td>
    <td style="width: 477px;">      启用 ResourceManager Recovery    </td>  </tr>
  <tr>    <td style="width: 575px;">      yarn.scheduler.fair.continuous-scheduling-enabled    </td>
    <td style="width: 72px;">    </td>
    <td style="width: 10px;">      true    </td>
    <td style="width: 477px;">      启用 Fair Scheduler 持续调度    </td>  </tr>
  <tr>    <td style="width: 575px;">      mapreduce.reduce.shuffle.memory.limit.percent    </td>
    <td style="width: 72px;">    </td>
    <td style="width: 10px;">      0.5    </td>
    <td style="width: 477px;">    </td>  </tr>
  <tr>    <td style="width: 575px;">      yarn.nodemanager.disk-health-checker.max-disk-utilization-per-disk-percentage    </td>
    <td style="width: 72px;">    </td>
    <td style="width: 10px;">      0.95    </td>
    <td style="width: 477px;">    </td>  </tr>
  <tr>    <td style="width: 575px;">      mapreduce.task.userlog.limit.kb    </td>
    <td style="width: 72px;">    </td>
    <td style="width: 10px;">      102400    </td>
    <td style="width: 477px;">       限制container输出的日志不要太大，设置为100MB，注意要设置log.backups，不然会使用内存    </td>  </tr>
  <tr>    <td style="width: 575px;">      yarn.app.mapreduce.task.container.log.backups    </td>
    <td style="width: 72px;">    </td>
    <td style="width: 10px;">       1    </td>
    <td style="width: 477px;">       备份文件个数    </td>  </tr>
  <tr>    <td style="width: 575px;">       yarn.scheduler.fair.max.assign    </td>
    <td style="width: 72px;">       -1    </td>
    <td style="width: 10px;">      10    </td>
    <td style="width: 477px;">       在rm配置，一次分配中，每台机器最大分配任务数    </td>  </tr>
  <tr>    <td style="width: 575px;">    </td>
    <td style="width: 72px;">    </td>
    <td style="width: 10px;">    </td>
    <td style="width: 477px;">    </td>  </tr>
  <tr>    <td style="width: 575px;">    </td>
    <td style="width: 72px;">    </td>
    <td style="width: 10px;">    </td>
    <td style="width: 477px;">    </td>  </tr>
  <tr>    <td style="width: 575px;">    </td>
    <td style="width: 72px;">    </td>
    <td style="width: 10px;">    </td>
    <td style="width: 477px;">    </td>  </tr>
  <tr>    <td style="width: 575px;">    </td>
    <td style="width: 72px;">    </td>
    <td style="width: 10px;">    </td>
    <td style="width: 477px;">    </td>  </tr></table>
<div class="property-name" data-bind="visible: propertyName, text: propertyName"></div>
<h2 class="property-name" data-bind="visible: propertyName, text: propertyName">  HDFS</h2>
<table>  <tr>    <td style="width: 104px;">      参数    </td>
    <td style="width: 104px;">      默认值    </td>
    <td style="width: 58px;">      值    </td>
    <td style="width: 611px;">      配置位置    </td>
    <td style="width: 611px;">      备注    </td>  </tr>
  <tr>    <td style="width: 104px;">      fs.du.interval    </td>
    <td style="width: 104px;">    </td>
    <td style="width: 58px;">      1200000    </td>
    <td style="width: 611px;">    </td>
    <td style="width: 611px;">      磁盘du间隔，du对磁盘IO影响比较大    </td>  </tr>
  <tr>    <td style="width: 104px;">      dfs.blockreport.initialDelay    </td>
    <td style="width: 104px;">    </td>
    <td style="width: 58px;">      180    </td>
    <td style="width: 611px;">    </td>
    <td style="width: 611px;">      延迟blockreport，避免重启时集中汇报    </td>  </tr>
  <tr>    <td style="width: 104px;">      dfs.block.scanner.cursor.save.interval.ms    </td>
    <td style="width: 104px;">    </td>
    <td style="width: 58px;">       默认10分钟    </td>
    <td style="width: 611px;">    </td>
    <td style="width: 611px;">       10分钟保存一次scan cursor    </td>  </tr>
  <tr>    <td style="width: 104px;">      dfs.block.scanner.volume.bytes.per.second    </td>
    <td style="width: 104px;">    </td>
    <td style="width: 58px;">       4194304    </td>
    <td style="width: 611px;">    </td>
    <td style="width: 611px;">       默认值1MB，磁盘扫描的限速，要注意看看扫描一个磁盘会不会太慢，但设的太高也会影响IO    </td>  </tr>
  <tr>    <td style="width: 104px;">      dfs.datanode.scan.period.hours    </td>
    <td style="width: 104px;">    </td>
    <td style="width: 58px;">       3weeks    </td>
    <td style="width: 611px;">    </td>
    <td style="width: 611px;">      常规 磁盘扫描间隔    </td>  </tr>
  <tr>    <td style="width: 104px;">      dfs.namenode.checkpoint.txns    </td>
    <td style="width: 104px;">    </td>
    <td style="width: 58px;">       10000000    </td>
    <td style="width: 611px;">       namenode hdfs-site.xml    </td>
    <td style="width: 611px;">       设置大一些，避免频繁的checkpoint传输    </td>  </tr>
  <tr>    <td style="width: 104px;">      <del>hadoop.user.group.static.mapping.overrides</del>    </td>
    <td style="width: 104px;">      <del>dr.who=;</del>    </td>
    <td style="width: 58px;">      <del>dr.who=;yarn=yarn,hadoop,supergroup;</del></p> 
      
      <p>        <del>mapred:mapred,hadoop,supergroup</del></td> 
        
        <td style="width: 611px;">        </td>
        <td style="width: 611px;">          <del>覆盖组权限，需要配置在core-site.xml里面，需要重启namenode</del>        </td></tr> 
        
        <tr>          <td style="width: 104px;">            dfs.namenode.posix.acl.inheritance.enabled          </td>
          <td style="width: 104px;">             false          </td>
          <td style="width: 58px;">            true          </td>
          <td style="width: 611px;">          </td>
          <td style="width: 611px;">             在namenode hdfs-site.xml配置，在打上HDFS-6962补丁后，ACL mask权限能够继承          </td>        </tr>
        <tr>          <td style="width: 104px;">            dfs.datanode.balance.max.concurrent.moves          </td>
          <td style="width: 104px;">            5          </td>
          <td style="width: 58px;">            50          </td>
          <td style="width: 611px;">          </td>
          <td style="width: 611px;">            平衡的线程数，用于提高平衡效率（需要在DataNode和Balance的hdfs-site配置，需要重启DataNode）          </td>        </tr>
        <tr>          <td style="width: 104px;">            dfs.datanode.balance.bandwidthPerSec          </td>
          <td style="width: 104px;">            10MB          </td>
          <td style="width: 58px;">            30MB          </td>
          <td style="width: 611px;">          </td>
          <td style="width: 611px;">            平衡的速度          </td>        </tr>
        <tr>          <td style="width: 104px;">            ha.failover-controller.new-active.rpc-timeout.ms          </td>
          <td style="width: 104px;">            60000          </td>
          <td style="width: 58px;">            300000          </td>
          <td style="width: 611px;">            全局的core-site.xml里面配置（客户端和failover controller都会用到）          </td>
          <td style="width: 611px;">            failover controller在转换active等待的时间，在hdfs failover controller里面配置，如果时间不够会在failover controller里面看到超时错误日志。<a href="https://issues.apache.org/jira/browse/HDFS-11254">HDFS-11254</a> 在replay editlog的时候也会很慢。<br /> 注意要先重启备机的controller，否则重启active controller，namenode会切换。          </td>        </tr>
        <tr>          <td style="width: 104px;">            dfs.image.transfer.bandwidthPerSec          </td>
          <td style="width: 104px;">          </td>
          <td style="width: 58px;">            41943040          </td>
          <td style="width: 611px;">            namenode hdfs-site.xml          </td>
          <td style="width: 611px;">            image传输限速，占用所有带宽会影响namenode rpc请求，重启active namenode才生效          </td>        </tr></tbody> </table> 
        
        <p>          &nbsp;        </p>
        <h2>          HIVE        </h2>
        <table style="width: 1113px;">          <tr>            <td style="width: 105px;">              参数            </td>
            <td style="width: 101px;">              默认值            </td>
            <td style="width: 159px;">              建议值            </td>
            <td style="width: 921px;">              备注            </td>          </tr>
          <tr>            <td style="width: 105px;">              hive.metastore.failure.retries            </td>
            <td style="width: 101px;">              1            </td>
            <td style="width: 159px;">              3            </td>
            <td style="width: 921px;">              metastore中途失败重试的次数，某个版本之前默认值是1，后面变为3            </td>          </tr>
          <tr>            <td style="width: 105px;">              hive.metastore.try.direct.sql            </td>
            <td style="width: 101px;">              false            </td>
            <td style="width: 159px;">            </td>
            <td style="width: 921px;">              Hive Metastore 是否应尝试使用直接 SQL 查询，而不是针对一定读取路径使用 DataNucleus。这样在获取许多分区时可以使 Metastore 性能得到数量级的提升。打开这个开关要确保打了补丁HIVE-15551，否则有内存泄露            </td>          </tr>
          <tr>            <td style="width: 105px;">            </td>
            <td style="width: 101px;">            </td>
            <td style="width: 159px;">            </td>
            <td style="width: 921px;">            </td>          </tr>        </table>
        <h2>          HBASE        </h2>
        <p>          https://github.com/mattshma/bigdata/blob/master/hbase/docs/hbase_rpc.md        </p>
        <p>          hbase.ipc.server.listen.queue.size   默认值 128        </p>
        <p>          hbase.ipc.server.read.threadpool.size 默认值 10        </p>
        <p>          hbase.regionserver.handler.count        </p>
        <p>          hbase.regionserver.metahandler.count        </p>