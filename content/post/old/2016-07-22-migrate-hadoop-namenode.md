---
title: 迁移Hadoop NameNode
author: fatkun
type: post
date: 2016-07-22T09:55:06+00:00
url: /2016/07/migrate-hadoop-namenode.html
duoshuo_thread_id:
  - 6310086010940162817
categories:
  - hadoop

---
<div id="wmd-preview-section-16098" class="wmd-preview-section preview-content">  版本：hadoop cdh5.4</p> 
  
  <h2 id="迁移hadoop-namenode">    传输文件  </h2></div>
<div id="wmd-preview-section-9638" class="wmd-preview-section preview-content">  <pre class="prettyprint"><code class=" hljs 1c">接收方  nc -l &lt;span class="hljs-number">19999&lt;/span> &lt;span class="hljs-string">| tar zxvf -&lt;/span>
发送方 tar czvf - ./current &lt;span class="hljs-string">| nc serverip 19999&lt;/span></code></pre></div>
<div id="wmd-preview-section-9639" class="wmd-preview-section preview-content">  <h3 id="迁移方案">    迁移方案  </h3>
  <p>    采用修改/etc/hosts的方式，把原hostname指向新的IP，新机器更改hostname  </p></div>
<div id="wmd-preview-section-9640" class="wmd-preview-section preview-content">  <h3 id="迁移前准备">    迁移前准备  </h3>
  <ul>    <li>      迁移旧namenode机器上的其他服务，只保留HDFS Failover Controller、HDFS JournalNode、HDFS NameNode、ZooKeeper（如有）    </li>
    <li>      在hdfs配置中找出元数据存放目录(dfs.name.dir)：/home/cloudera/var/dfs/nn    </li>
    <li>      在新NameNode机器建立好用户和组（否则权限不正确）    </li>
    <li>      如果要迁移Hive Metastore，要注意mysql-connector.jar是否部署好（放在 /usr/share/java/mysql-connector-java.jar）    </li>
    <li>      更改/etc/hosts准备    </li>
    <li>      在新机器部署cloudera    </li>  </ul></div>
<div id="wmd-preview-section-9641" class="wmd-preview-section preview-content">  <h3 id="开始迁移">    开始迁移  </h3></div>
<div id="wmd-preview-section-9642" class="wmd-preview-section preview-content">  <h4 id="1备份元数据">    1.备份元数据  </h4>
  <ul>    <li>      让备机NameNode进入安全模式    </li>
    <li>      保存Namespace    </li>
    <li>      进入元数据目录，新建目录，备份fsimage_*（最新的一份）、fsimage_*.md5、seen_txid、VERSION、edits_*    </li>
    <li>      把元数据传到新机器    </li>  </ul></div>
<div id="wmd-preview-section-9643" class="wmd-preview-section preview-content">  <pre class="prettyprint"><code class=" hljs vala">&lt;span class="hljs-preprocessor"># 在新机器执行&lt;/span>
mkdir -p /home/cloudera/&lt;span class="hljs-keyword">var&lt;/span>/dfs/nn/current
chown -R hdfs:hdfs /home/cloudera/&lt;span class="hljs-keyword">var&lt;/span>/dfs

&lt;span class="hljs-preprocessor"># 传输文件（要注意nc的版本）&lt;/span>
&lt;span class="hljs-preprocessor">#接收方 &lt;/span>
nc -l &lt;span class="hljs-number">19999&lt;/span> | tar zxvf -
&lt;span class="hljs-preprocessor">#传送方&lt;/span>
tar czvf - ./fsimage_0000000000006460983*  seen_txid &lt;span class="hljs-constant"> VERSION &lt;/span>edits_* | nc serverip &lt;span class="hljs-number">19999&lt;/span>  </code></pre></div>
<div id="wmd-preview-section-13170" class="wmd-preview-section preview-content">  <h4 id="2停止namenode备机服务">    2.停止NameNode备机服务  </h4>
  <ul>    <li>      把这台机器的所有服务停止，并且删除掉（停止前记录一下上面有哪些服务）    </li>
    <li>      停止两个HDFS Failover Controller    </li>
    <li>      停止旧机器的agent /etc/init.d/cloudera-scm-agent stop    </li>
    <li>      从主机中删除旧机器    </li>  </ul></div>
<div id="wmd-preview-section-12219" class="wmd-preview-section preview-content">  <h4 id="3修改ip和hostname">    3.修改IP和Hostname  </h4>
  <ul>    <li>      修改所有机器的旧hostname指向新IP    </li>
    <li>      修改旧机器的hostname为其他名称（可以不操作）    </li>
    <li>      修改新机器的hostname为旧机器hostname，注意/etc/hosts里面本机的原有hostname/IP注释掉    </li>
    <li>      重启新机器的cloudera agent：/etc/init.d/cloudera-scm-agent restart    </li>
    <li>      重启完成检查主机名称是否变更    </li>
    <li>      重启agent后要重新部署CDH    </li>  </ul></div>
<div id="wmd-preview-section-16054" class="wmd-preview-section preview-content">  <h4 id="4重新添加回服务">    4.重新添加回服务  </h4>
  <ul>    <li>      添加ZooKeeper    </li>
    <li>      添加Hive Metastore    </li>
    <li>      添加NameNode、JournalNode、Failover Controller，需要改nameservice，先启动NameNode    </li>
    <li>      等namenode汇报完块后    </li>  </ul></div>
<div id="wmd-preview-section-17102" class="wmd-preview-section preview-content">  <h4 id="5重启">    5.重启  </h4>
  <ul>    <li>      重启zookeeper（全部重启）    </li>
    <li>      重启hbase    </li>
    <li>      重启impala    </li>
    <li>      重启nodemanager、history server    </li>
    <li>      重启spark    </li>
    <li>      重启所有用了hdfs常驻型的程序    </li>  </ul>
  <p>    等新机器NameNode正常后，切换为主NameNode  </p></div>
<div id="wmd-preview-section-9648" class="wmd-preview-section preview-content">  <h3 id="错误处理">    错误处理  </h3>
  <p>    <code>namenode (osg13-vm05) 在其主机上不具备自动故障转移所必需的 Failover Controller。</code><br /> 没有添加Failover Controller，添加一个  </p></div>
<div id="wmd-preview-section-13874" class="wmd-preview-section preview-content">  <h3 id="检查">    检查  </h3>
  <p>    hdfs：hdfs dfs -ls /tmp<br /> hive：show tables;<br /> <strong><em>impala</em></strong><br /> show tables; desc xxx; select<br /> <strong><em>hbase</em></strong>  </p></div>
<div id="wmd-preview-section-13911" class="wmd-preview-section preview-content">  <pre class="prettyprint"><code class=" hljs php">hbase shell
&lt;span class="hljs-keyword">list&lt;/span>
desc &lt;span class="hljs-string">"gjtt_uid"&lt;/span>
scan &lt;span class="hljs-string">'gjtt_uid'&lt;/span>,{LIMIT =&gt;&lt;span class="hljs-number">2&lt;/span>}</code></pre>
  <p>    <strong><em>hadoop</em></strong>  </p></div>
<div id="wmd-preview-section-13534" class="wmd-preview-section preview-content">  <pre class="prettyprint"><code class=" hljs lasso">hadoop jar /home/cloudera/parcels/CDH/lib/hadoop&lt;span class="hljs-attribute">-mapreduce&lt;/span>/hadoop&lt;span class="hljs-attribute">-mapreduce&lt;/span>&lt;span class="hljs-attribute">-examples&lt;/span>&lt;span class="hljs-built_in">.&lt;/span>jar pi &lt;span class="hljs-number">1&lt;/span> &lt;span class="hljs-number">10&lt;/span></code></pre>
  <p>    <strong><em>spark</em></strong><br /> spark-shell  </p></div>
<div id="wmd-preview-section-38061" class="wmd-preview-section preview-content">  <pre class="prettyprint"><code class=" hljs avrasm">val input = sc&lt;span class="hljs-preprocessor">.textFile&lt;/span>(&lt;span class="hljs-string">"/tmp/issue"&lt;/span>)
input&lt;span class="hljs-preprocessor">.flatMap&lt;/span>(_&lt;span class="hljs-preprocessor">.split&lt;/span>(&lt;span class="hljs-string">" "&lt;/span>))&lt;span class="hljs-preprocessor">.map&lt;/span>((_, &lt;span class="hljs-number">1&lt;/span>))&lt;span class="hljs-preprocessor">.reduceByKey&lt;/span>(_ + _)&lt;span class="hljs-preprocessor">.foreach&lt;/span>(println)</code></pre></div>
<div id="wmd-preview-section-39422" class="wmd-preview-section preview-content">  <h3 id="回滚">    回滚  </h3>
  <p>    把hosts改回去，namenode切换回去  </p></div>
<div id="wmd-preview-section-43963" class="wmd-preview-section preview-content">  <h3 id="做不到不影响服务的原因">    做不到不影响服务的原因  </h3>
  <p>    一开始以为是java缓存了host/IP，但测试之后发现java只缓存30秒。<br /> 原因是DfsClient在建立rpcProxy对象的时候，已经把namenode两台机器的host解析出来，并且放在ConnectionId里，这个对象会一直使用。<br /> 补丁<a href="https://issues.apache.org/jira/browse/HADOOP-7472">HADOOP-7472</a> 只解决了在没有HA的场景，不过也让datanode可以不用重启。<br /> 在HA场景下，恰好让上面的补丁失效了。<br /> 在社区找了一下新的ISSUE <a href="https://issues.apache.org/jira/browse/HADOOP-12125">https://issues.apache.org/jira/browse/HADOOP-12125</a> ，但可能不是重要的问题，也没人提交补丁。因为涉及比较基础的类，影响比较大，也不打算修改，采取重启的方式。<br /> 也尝试了一些奇怪的方法，但是没有很好的解决问题，还是选择重启服务。  </p></div>