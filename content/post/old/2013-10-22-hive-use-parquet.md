---
title: 在hive中使用parquet (CDH4.3)
author: fatkun
type: post
date: 2013-10-21T17:05:47+00:00
url: /2013/10/hive-use-parquet.html
duoshuo_thread_id:
  - 6300410041346294530
wp-syntax-cache-content:
  - |
    a:6:{i:1;s:2340:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;"><span style="color: #66cc66;">&#91;</span>impala:<span style="color: #cc66cc;">21000</span><span style="color: #66cc66;">&#93;</span> <span style="color: #66cc66;">&gt;</span> <span style="color: #993333; font-weight: bold;">SELECT</span> <span style="color: #66cc66;">*</span> <span style="color: #993333; font-weight: bold;">FROM</span> foo;
    Query: <span style="color: #993333; font-weight: bold;">SELECT</span> <span style="color: #66cc66;">*</span> <span style="color: #993333; font-weight: bold;">FROM</span> foo
    ERROR: AnalysisException: Failed <span style="color: #993333; font-weight: bold;">TO</span> <span style="color: #993333; font-weight: bold;">LOAD</span> metadata <span style="color: #993333; font-weight: bold;">FOR</span> <span style="color: #993333; font-weight: bold;">TABLE</span>: <span style="color: #993333; font-weight: bold;">DEFAULT</span><span style="color: #66cc66;">.</span>foo
    CAUSED <span style="color: #993333; font-weight: bold;">BY</span>: TableLoadingException: Failed <span style="color: #993333; font-weight: bold;">TO</span> <span style="color: #993333; font-weight: bold;">LOAD</span> metadata <span style="color: #993333; font-weight: bold;">FOR</span> <span style="color: #993333; font-weight: bold;">TABLE</span>: foo
    CAUSED <span style="color: #993333; font-weight: bold;">BY</span>: MetaException: org<span style="color: #66cc66;">.</span>apache<span style="color: #66cc66;">.</span>hadoop<span style="color: #66cc66;">.</span>hive<span style="color: #66cc66;">.</span>serde2<span style="color: #66cc66;">.</span>SerDeException SerDe parquet<span style="color: #66cc66;">.</span>hive<span style="color: #66cc66;">.</span>serde<span style="color: #66cc66;">.</span>ParquetHiveSerDe does <span style="color: #993333; font-weight: bold;">NOT</span> exist</pre></td></tr></table><p class="theCode" style="display:none;">[impala:21000] &gt; select * from foo;
    Query: select * from foo
    ERROR: AnalysisException: Failed to load metadata for table: default.foo
    CAUSED BY: TableLoadingException: Failed to load metadata for table: foo
    CAUSED BY: MetaException: org.apache.hadoop.hive.serde2.SerDeException SerDe parquet.hive.serde.ParquetHiveSerDe does not exist</p></div>
    ";i:2;s:2555:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #666666; font-style: italic;">#!/bin/sh</span>
    <span style="color: #666666; font-style: italic;">#parquet-pig parquet-scrooge parquet-test-hadoop2 parquet-thrift parquet-avro parquet-cascading </span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">for</span> f <span style="color: #000000; font-weight: bold;">in</span> parquet-column parquet-common parquet-encoding parquet-generator parquet-hadoop parquet-hive 
    <span style="color: #000000; font-weight: bold;">do</span>
    curl <span style="color: #660033;">-O</span> http:<span style="color: #000000; font-weight: bold;">//</span>repo1.maven.org<span style="color: #000000; font-weight: bold;">/</span>maven2<span style="color: #000000; font-weight: bold;">/</span>com<span style="color: #000000; font-weight: bold;">/</span>twitter<span style="color: #000000; font-weight: bold;">/</span><span style="color: #800000;">${f}</span><span style="color: #000000; font-weight: bold;">/</span>1.2.4<span style="color: #000000; font-weight: bold;">/</span><span style="color: #800000;">${f}</span>-1.2.4.jar
    <span style="color: #666666; font-style: italic;">#curl -O http://oss.sonatype.org/service/local/repositories/releases/content/com/twitter/${f}/1.2.4/${f}-1.2.4.jar</span>
    <span style="color: #000000; font-weight: bold;">done</span>
    curl <span style="color: #660033;">-O</span> http:<span style="color: #000000; font-weight: bold;">//</span>repo1.maven.org<span style="color: #000000; font-weight: bold;">/</span>maven2<span style="color: #000000; font-weight: bold;">/</span>com<span style="color: #000000; font-weight: bold;">/</span>twitter<span style="color: #000000; font-weight: bold;">/</span>parquet-format<span style="color: #000000; font-weight: bold;">/</span>1.0.0<span style="color: #000000; font-weight: bold;">/</span>parquet-format-1.0.0.jar</pre></td></tr></table><p class="theCode" style="display:none;">#!/bin/sh
    #parquet-pig parquet-scrooge parquet-test-hadoop2 parquet-thrift parquet-avro parquet-cascading 
    
    for f in parquet-column parquet-common parquet-encoding parquet-generator parquet-hadoop parquet-hive 
    do
    curl -O http://repo1.maven.org/maven2/com/twitter/${f}/1.2.4/${f}-1.2.4.jar
    #curl -O http://oss.sonatype.org/service/local/repositories/releases/content/com/twitter/${f}/1.2.4/${f}-1.2.4.jar
    done
    curl -O http://repo1.maven.org/maven2/com/twitter/parquet-format/1.0.0/parquet-format-1.0.0.jar</p></div>
    ";i:3;s:812:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #c20cb9; font-weight: bold;">cp</span> parquet-<span style="color: #000000; font-weight: bold;">*</span>  <span style="color: #000000; font-weight: bold;">/</span>opt<span style="color: #000000; font-weight: bold;">/</span>cloudera<span style="color: #000000; font-weight: bold;">/</span>parcels<span style="color: #000000; font-weight: bold;">/</span>CDH<span style="color: #000000; font-weight: bold;">/</span>lib<span style="color: #000000; font-weight: bold;">/</span>hive<span style="color: #000000; font-weight: bold;">/</span>lib</pre></td></tr></table><p class="theCode" style="display:none;">cp parquet-*  /opt/cloudera/parcels/CDH/lib/hive/lib</p></div>
    ";i:4;s:243:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;">INVALIDATE METADATA;</pre></td></tr></table><p class="theCode" style="display:none;">INVALIDATE METADATA;</p></div>
    ";i:5;s:434:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">create table test2 <span style="color: #7a0874; font-weight: bold;">&#40;</span>name STRING<span style="color: #7a0874; font-weight: bold;">&#41;</span> STORED AS PARQUETFILE;</pre></td></tr></table><p class="theCode" style="display:none;">create table test2 (name STRING) STORED AS PARQUETFILE;</p></div>
    ";i:6;s:446:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">insert into test2 <span style="color: #000000; font-weight: bold;">select</span> <span style="color: #000000; font-weight: bold;">*</span> from <span style="color: #7a0874; font-weight: bold;">test</span>;</pre></td></tr></table><p class="theCode" style="display:none;">insert into test2 select * from test;</p></div>
    ";}
categories:
  - hadoop
  - hive
tags:
  - hive
  - impala

---
hadoop版本 cdh4.3
使用impala创建parquet表后，查询会出错。
<pre lang="sql" escaped="true">[impala:21000] &gt; select * from foo;
Query: select * from foo
ERROR: AnalysisException: Failed to load metadata for table: default.foo
CAUSED BY: TableLoadingException: Failed to load metadata for table: foo
CAUSED BY: MetaException: org.apache.hadoop.hive.serde2.SerDeException SerDe parquet.hive.serde.ParquetHiveSerDe does not exist</pre>
原因是hive并没有这些lib，下载它们并放入/opt/cloudera/parcels/CDH/lib/hive/lib目录（我是使用cloudera manager部署的）,创建脚本下载
<pre lang="bash" escaped="true">#!/bin/sh
#parquet-pig parquet-scrooge parquet-test-hadoop2 parquet-thrift parquet-avro parquet-cascading 

for f in parquet-column parquet-common parquet-encoding parquet-generator parquet-hadoop parquet-hive 
do
curl -O http://repo1.maven.org/maven2/com/twitter/${f}/1.2.4/${f}-1.2.4.jar
#curl -O http://oss.sonatype.org/service/local/repositories/releases/content/com/twitter/${f}/1.2.4/${f}-1.2.4.jar
done
curl -O http://repo1.maven.org/maven2/com/twitter/parquet-format/1.0.0/parquet-format-1.0.0.jar
</pre>
然后把他们拷贝进去
<pre lang="bash" escaped="true">cp parquet-*  /opt/cloudera/parcels/CDH/lib/hive/lib</pre>
可能要重启metastore，然后在impala中刷新metastore
<pre lang="sql" escaped="true">INVALIDATE METADATA;</pre>
在impala修改parquet表
<pre lang="bash" escaped="true">create table test2 (name STRING) STORED AS PARQUETFILE;</pre>
插入数据
<pre lang="bash" escaped="true">insert into test2 select * from test;</pre>
## 参考

<https://issues.cloudera.org/browse/IMPALA-574>
&nbsp;