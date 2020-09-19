---
title: hbase shell创建表命令
author: fatkun
type: post
date: 2016-01-20T10:43:55+00:00
url: /2016/01/hbase-shell创建表命令.html
duoshuo_thread_id:
  - 6300421658444301057
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:3439:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">create <span style="color: #ff0000;">'ucbrowser_imei2'</span>, <span style="color: #7a0874; font-weight: bold;">&#123;</span><span style="color: #007800;">NAME</span>=<span style="color: #000000; font-weight: bold;">&gt;</span><span style="color: #ff0000;">'date'</span>, <span style="color: #007800;">VERSIONS</span>=<span style="color: #000000; font-weight: bold;">&gt;</span><span style="color: #000000;">5</span><span style="color: #7a0874; font-weight: bold;">&#125;</span>
    &nbsp;
    disable <span style="color: #ff0000;">'test_imei'</span>
    &nbsp;
    drop <span style="color: #ff0000;">'test_imei'</span>
    &nbsp;
    <span style="color: #666666; font-style: italic;"># 预先指定分区</span>
    create <span style="color: #ff0000;">'ucbrowser_utdid'</span>, <span style="color: #ff0000;">'date'</span>, <span style="color: #7a0874; font-weight: bold;">&#123;</span> VERSIONS =<span style="color: #000000; font-weight: bold;">&gt;</span> <span style="color: #ff0000;">'5'</span>, DATA_BLOCK_ENCODING =<span style="color: #000000; font-weight: bold;">&gt;</span> <span style="color: #ff0000;">'PREFIX'</span>, COMPRESSION =<span style="color: #000000; font-weight: bold;">&gt;</span> <span style="color: #ff0000;">'SNAPPY'</span>, <span style="color: #007800;">SPLITS</span>=<span style="color: #000000; font-weight: bold;">&gt;</span><span style="color: #7a0874; font-weight: bold;">&#91;</span><span style="color: #ff0000;">'03ufUX/IWscQABV+EwvaHDOo'</span><span style="color: #7a0874; font-weight: bold;">&#93;</span><span style="color: #7a0874; font-weight: bold;">&#125;</span>
    <span style="color: #666666; font-style: italic;"># 预先分区（200个region）</span>
    hbase org.apache.hadoop.hbase.util.RegionSplitter <span style="color: #660033;">-c</span> <span style="color: #000000;">200</span> <span style="color: #660033;">-f</span> <span style="color: #ff0000;">&quot;date&quot;</span> <span style="color: #ff0000;">&quot;ucbrowser_imei2&quot;</span> <span style="color: #ff0000;">&quot;HexStringSplit&quot;</span>
    &nbsp;
    <span style="color: #666666; font-style: italic;"># 修改版本</span>
    alter <span style="color: #ff0000;">'test_imei'</span>, <span style="color: #7a0874; font-weight: bold;">&#123;</span>NAME =<span style="color: #000000; font-weight: bold;">&gt;</span> <span style="color: #ff0000;">'date'</span>, VERSIONS =<span style="color: #000000; font-weight: bold;">&gt;</span> <span style="color: #000000;">5</span> <span style="color: #7a0874; font-weight: bold;">&#125;</span>
    &nbsp;
    <span style="color: #666666; font-style: italic;"># 查看表描述</span>
    describe <span style="color: #ff0000;">&quot;test_imei&quot;</span></pre></td></tr></table><p class="theCode" style="display:none;">create 'ucbrowser_imei2', {NAME=&gt;'date', VERSIONS=&gt;5}
    
    disable 'test_imei'
    
    drop 'test_imei'
    
    # 预先指定分区
    create 'ucbrowser_utdid', 'date', { VERSIONS =&gt; '5', DATA_BLOCK_ENCODING =&gt; 'PREFIX', COMPRESSION =&gt; 'SNAPPY', SPLITS=&gt;['03ufUX/IWscQABV+EwvaHDOo']}
    # 预先分区（200个region）
    hbase org.apache.hadoop.hbase.util.RegionSplitter -c 200 -f &quot;date&quot; &quot;ucbrowser_imei2&quot; &quot;HexStringSplit&quot;
    
    # 修改版本
    alter 'test_imei', {NAME =&gt; 'date', VERSIONS =&gt; 5 }
    
    # 查看表描述
    describe &quot;test_imei&quot;</p></div>
    ";i:2;s:2022:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #666666; font-style: italic;"># 在原集群执行</span>
    snapshot <span style="color: #ff0000;">'ucbrowser_utdid'</span>, <span style="color: #ff0000;">'ucbrowser_utdid_20171208'</span>
    &nbsp;
    <span style="color: #666666; font-style: italic;"># 导出镜像</span>
    hbase org.apache.hadoop.hbase.snapshot.ExportSnapshot <span style="color: #660033;">-snapshot</span> ucbrowser_utdid_20171208 <span style="color: #660033;">-copy-to</span> hdfs:<span style="color: #000000; font-weight: bold;">//</span><span style="color: #000000;">10</span>.xx.xx.xx:<span style="color: #000000;">8020</span><span style="color: #000000; font-weight: bold;">/</span>hbase 
    &nbsp;
    <span style="color: #666666; font-style: italic;"># 检查目标集群的文件权限是否正确</span>
    hdfs dfs <span style="color: #c20cb9; font-weight: bold;">chown</span> <span style="color: #660033;">-R</span> hbase:hbase <span style="color: #000000; font-weight: bold;">/</span>hbase<span style="color: #000000; font-weight: bold;">/</span>archive
    &nbsp;
    <span style="color: #666666; font-style: italic;"># 在目标集群恢复</span>
    disable  <span style="color: #ff0000;">'ucbrowser_utdid'</span>
    restore_snapshot <span style="color: #ff0000;">'ucbrowser_utdid_20171208'</span>
    &nbsp;
    <span style="color: #666666; font-style: italic;"># 查看镜像</span>
    list_snapshots</pre></td></tr></table><p class="theCode" style="display:none;"># 在原集群执行
    snapshot 'ucbrowser_utdid', 'ucbrowser_utdid_20171208'
    
    # 导出镜像
    hbase org.apache.hadoop.hbase.snapshot.ExportSnapshot -snapshot ucbrowser_utdid_20171208 -copy-to hdfs://10.xx.xx.xx:8020/hbase 
    
    # 检查目标集群的文件权限是否正确
    hdfs dfs chown -R hbase:hbase /hbase/archive
    
    # 在目标集群恢复
    disable  'ucbrowser_utdid'
    restore_snapshot 'ucbrowser_utdid_20171208'
    
    # 查看镜像
    list_snapshots</p></div>
    ";}
categories:
  - hbase
tags:
  - hbase
  - shell

---
<pre lang="bash" escaped="true">create 'ucbrowser_imei2', {NAME=&gt;'date', VERSIONS=&gt;5}

disable 'test_imei'

drop 'test_imei'

# 预先指定分区
create 'ucbrowser_utdid', 'date', { VERSIONS =&gt; '5', DATA_BLOCK_ENCODING =&gt; 'PREFIX', COMPRESSION =&gt; 'SNAPPY', SPLITS=&gt;['03ufUX/IWscQABV+EwvaHDOo']}
# 预先分区（200个region）
hbase org.apache.hadoop.hbase.util.RegionSplitter -c 200 -f "date" "ucbrowser_imei2" "HexStringSplit"

# 修改版本
alter 'test_imei', {NAME =&gt; 'date', VERSIONS =&gt; 5 }

# 查看表描述
describe "test_imei"

</pre>
## snapshot

<pre lang="bash" escaped="true"># 在原集群执行
snapshot 'ucbrowser_utdid', 'ucbrowser_utdid_20171208'

# 导出镜像
hbase org.apache.hadoop.hbase.snapshot.ExportSnapshot -snapshot ucbrowser_utdid_20171208 -copy-to hdfs://10.xx.xx.xx:8020/hbase 

# 检查目标集群的文件权限是否正确
hdfs dfs chown -R hbase:hbase /hbase/archive

# 在目标集群恢复
disable  'ucbrowser_utdid'
restore_snapshot 'ucbrowser_utdid_20171208'

# 查看镜像
list_snapshots
</pre>
&nbsp;
<p class="csdn_top">  HBase备份之ExportSnapshot或CopyTable</p>
<http://blog.csdn.net/iam333/article/details/38538073>