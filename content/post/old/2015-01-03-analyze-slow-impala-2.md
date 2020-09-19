---
title: 从日志分析impala查询慢的原因（2）
author: fatkun
type: post
date: 2015-01-03T08:51:57+00:00
url: /2015/01/analyze-slow-impala-2.html
duoshuo_thread_id:
  - 6300410881708655362
wp-syntax-cache-content:
  - |
    a:5:{i:1;s:4442:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="other" style="font-family:monospace;"># impalad日志
    I0103 15:09:35.503356 27319 impala-beeswax-server.cc:170] query(): query=select distinct(disp_id) from default_impala.kpi_disp_user_info_stat_tb where pt='2014-04-08'
    I0103 15:11:36.109915 27319 Frontend.java:779] Missing tables were not received in 120000ms. Load request will be retried.
    I0103 15:11:36.110705 27319 Frontend.java:709] Requesting prioritized load of table(s): default_impala.kpi_disp_user_info_stat_tb
    I0103 15:11:50.778054 27319 Frontend.java:833] create plan
    I0103 15:11:50.806649 27319 HdfsScanNode.java:571] collecting partitions for table kpi_disp_user_info_stat_tb
    I0103 15:11:51.070816 27319 impala-server.cc:590] Execution request: TExecRequest {
    &nbsp;
    &nbsp;
    &nbsp;
    # catalog日志
    I0103 15:09:35.892182 29165 rpc-trace.cc:133] RPC call: CatalogService.PrioritizeLoad(from ::ffff:127.0.0.1:44323)
    I0103 15:09:39.563268 29185 HdfsTable.java:916] load table: default_impala.kpi_disp_user_info_stat_tb
    I0103 15:10:48.357046 29185 HdfsTable.java:234] load block md for kpi_disp_user_info_stat_tb
    I0103 15:11:36.110947 29165 rpc-trace.cc:133] RPC call: CatalogService.PrioritizeLoad(from ::ffff:127.0.0.1:44323)
    I0103 15:11:48.948714 29185 HdfsTable.java:1056] table #rows=-1
    &nbsp;
    &nbsp;
    # hive metastore日志
    2015-01-03 15:09:38,991 INFO org.apache.hadoop.hive.metastore.HiveMetaStore: 54032: source:/IP地址 get_table : db=default_impala tbl=kpi_disp_user_info_stat_tb
    2015-01-03 15:09:39,848 INFO org.apache.hadoop.hive.metastore.HiveMetaStore: 54032: source:/IP地址 get_partition_names : db=default_impala tbl=kpi_disp_user_info_stat_tb
    2015-01-03 15:09:39,902 INFO org.apache.hadoop.hive.metastore.HiveMetaStore: 54032: source:/IP地址 get_partitions_by_names : db=default_impala tbl=kpi_disp_user_info_stat_tb
    2015-01-03 15:09:52,839 INFO org.apache.hadoop.hive.metastore.HiveMetaStore: 54032: source:/IP地址 get_partitions_by_names : db=default_impala tbl=kpi_disp_user_info_stat_tb
    2015-01-03 15:10:05,383 INFO org.apache.hadoop.hive.metastore.HiveMetaStore: 54032: source:/IP地址 get_partitions_by_names : db=default_impala tbl=kpi_disp_user_info_stat_tb</pre></td></tr></table><p class="theCode" style="display:none;"># impalad日志
    I0103 15:09:35.503356 27319 impala-beeswax-server.cc:170] query(): query=select distinct(disp_id) from default_impala.kpi_disp_user_info_stat_tb where pt='2014-04-08'
    I0103 15:11:36.109915 27319 Frontend.java:779] Missing tables were not received in 120000ms. Load request will be retried.
    I0103 15:11:36.110705 27319 Frontend.java:709] Requesting prioritized load of table(s): default_impala.kpi_disp_user_info_stat_tb
    I0103 15:11:50.778054 27319 Frontend.java:833] create plan
    I0103 15:11:50.806649 27319 HdfsScanNode.java:571] collecting partitions for table kpi_disp_user_info_stat_tb
    I0103 15:11:51.070816 27319 impala-server.cc:590] Execution request: TExecRequest {
    
    
    
    # catalog日志
    I0103 15:09:35.892182 29165 rpc-trace.cc:133] RPC call: CatalogService.PrioritizeLoad(from ::ffff:127.0.0.1:44323)
    I0103 15:09:39.563268 29185 HdfsTable.java:916] load table: default_impala.kpi_disp_user_info_stat_tb
    I0103 15:10:48.357046 29185 HdfsTable.java:234] load block md for kpi_disp_user_info_stat_tb
    I0103 15:11:36.110947 29165 rpc-trace.cc:133] RPC call: CatalogService.PrioritizeLoad(from ::ffff:127.0.0.1:44323)
    I0103 15:11:48.948714 29185 HdfsTable.java:1056] table #rows=-1
    
    
    # hive metastore日志
    2015-01-03 15:09:38,991 INFO org.apache.hadoop.hive.metastore.HiveMetaStore: 54032: source:/IP地址 get_table : db=default_impala tbl=kpi_disp_user_info_stat_tb
    2015-01-03 15:09:39,848 INFO org.apache.hadoop.hive.metastore.HiveMetaStore: 54032: source:/IP地址 get_partition_names : db=default_impala tbl=kpi_disp_user_info_stat_tb
    2015-01-03 15:09:39,902 INFO org.apache.hadoop.hive.metastore.HiveMetaStore: 54032: source:/IP地址 get_partitions_by_names : db=default_impala tbl=kpi_disp_user_info_stat_tb
    2015-01-03 15:09:52,839 INFO org.apache.hadoop.hive.metastore.HiveMetaStore: 54032: source:/IP地址 get_partitions_by_names : db=default_impala tbl=kpi_disp_user_info_stat_tb
    2015-01-03 15:10:05,383 INFO org.apache.hadoop.hive.metastore.HiveMetaStore: 54032: source:/IP地址 get_partitions_by_names : db=default_impala tbl=kpi_disp_user_info_stat_tb</p></div>
    ";i:2;s:9987:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #666666; font-style: italic;">// Frontend.java</span>
      <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000066; font-weight: bold;">boolean</span> requestTblLoadAndWait<span style="color: #009900;">&#40;</span>Set<span style="color: #339933;">&lt;</span>TableName<span style="color: #339933;">&gt;</span> requestedTbls, <span style="color: #000066; font-weight: bold;">long</span> timeoutMs<span style="color: #009900;">&#41;</span>
          <span style="color: #000000; font-weight: bold;">throws</span> InternalException <span style="color: #009900;">&#123;</span>
    <span style="color: #666666; font-style: italic;">// impala本地缓存了元素据，每个表有一个版本号。本地的缓存一开始只缓存表名，分区信息等都没有缓存</span>
        Set<span style="color: #339933;">&lt;</span>TableName<span style="color: #339933;">&gt;</span> missingTbls <span style="color: #339933;">=</span> getMissingTbls<span style="color: #009900;">&#40;</span>requestedTbls<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #666666; font-style: italic;">// There are no missing tables, return and avoid making an RPC to the CatalogServer.</span>
        <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>missingTbls.<span style="color: #006633;">isEmpty</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">return</span> <span style="color: #000066; font-weight: bold;">true</span><span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #666666; font-style: italic;">// Call into the CatalogServer and request the required tables be loaded.</span>
        LOG.<span style="color: #006633;">info</span><span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span>.<span style="color: #006633;">format</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Requesting prioritized load of table(s): %s&quot;</span>,
            Joiner.<span style="color: #006633;">on</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;, &quot;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">join</span><span style="color: #009900;">&#40;</span>missingTbls<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">// 这里通过jni的方式调用c++写的代码，与catalogd通信获取元素据</span>
        TStatus status <span style="color: #339933;">=</span> FeSupport.<span style="color: #006633;">PrioritizeLoad</span><span style="color: #009900;">&#40;</span>missingTbls<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>status.<span style="color: #006633;">getStatus_code</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">!=</span> TStatusCode.<span style="color: #006633;">OK</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #000000; font-weight: bold;">throw</span> <span style="color: #000000; font-weight: bold;">new</span> InternalException<span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Error requesting prioritized load: &quot;</span> <span style="color: #339933;">+</span>
              Joiner.<span style="color: #006633;">on</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;<span style="color: #000099; font-weight: bold;">\n</span>&quot;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">join</span><span style="color: #009900;">&#40;</span>status.<span style="color: #006633;">getError_msgs</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        <span style="color: #000066; font-weight: bold;">long</span> startTimeMs <span style="color: #339933;">=</span> <span style="color: #003399;">System</span>.<span style="color: #006633;">currentTimeMillis</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #666666; font-style: italic;">// Wait until all the required tables are loaded in the Impalad's catalog cache.</span>
        <span style="color: #666666; font-style: italic;">// 检查是不是在本地缓存里了</span>
        <span style="color: #000000; font-weight: bold;">while</span> <span style="color: #009900;">&#40;</span><span style="color: #339933;">!</span>missingTbls.<span style="color: #006633;">isEmpty</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #666666; font-style: italic;">// Check if the timeout has been reached.</span>
          <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>timeoutMs <span style="color: #339933;">&gt;</span> <span style="color: #cc66cc;">0</span> <span style="color: #339933;">&amp;&amp;</span> <span style="color: #003399;">System</span>.<span style="color: #006633;">currentTimeMillis</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">-</span> startTimeMs <span style="color: #339933;">&gt;</span> timeoutMs<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">return</span> <span style="color: #000066; font-weight: bold;">false</span><span style="color: #339933;">;</span>
          <span style="color: #009900;">&#125;</span>
    &nbsp;
          LOG.<span style="color: #006633;">trace</span><span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span>.<span style="color: #006633;">format</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Waiting for table(s) to complete loading: %s&quot;</span>,
              Joiner.<span style="color: #006633;">on</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;, &quot;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">join</span><span style="color: #009900;">&#40;</span>missingTbls<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          getCatalog<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">waitForCatalogUpdate</span><span style="color: #009900;">&#40;</span>MAX_CATALOG_UPDATE_WAIT_TIME_MS<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          missingTbls <span style="color: #339933;">=</span> getMissingTbls<span style="color: #009900;">&#40;</span>missingTbls<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #666666; font-style: italic;">// TODO: Check for query cancellation here.</span>
        <span style="color: #009900;">&#125;</span>
        <span style="color: #000000; font-weight: bold;">return</span> <span style="color: #000066; font-weight: bold;">true</span><span style="color: #339933;">;</span>
      <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">// Frontend.java
      private boolean requestTblLoadAndWait(Set&lt;TableName&gt; requestedTbls, long timeoutMs)
          throws InternalException {
    // impala本地缓存了元素据，每个表有一个版本号。本地的缓存一开始只缓存表名，分区信息等都没有缓存
        Set&lt;TableName&gt; missingTbls = getMissingTbls(requestedTbls);
        // There are no missing tables, return and avoid making an RPC to the CatalogServer.
        if (missingTbls.isEmpty()) return true;
    
        // Call into the CatalogServer and request the required tables be loaded.
        LOG.info(String.format(&quot;Requesting prioritized load of table(s): %s&quot;,
            Joiner.on(&quot;, &quot;).join(missingTbls)));
    // 这里通过jni的方式调用c++写的代码，与catalogd通信获取元素据
        TStatus status = FeSupport.PrioritizeLoad(missingTbls);
        if (status.getStatus_code() != TStatusCode.OK) {
          throw new InternalException(&quot;Error requesting prioritized load: &quot; +
              Joiner.on(&quot;\n&quot;).join(status.getError_msgs()));
        }
    
        long startTimeMs = System.currentTimeMillis();
        // Wait until all the required tables are loaded in the Impalad's catalog cache.
        // 检查是不是在本地缓存里了
        while (!missingTbls.isEmpty()) {
          // Check if the timeout has been reached.
          if (timeoutMs &gt; 0 &amp;&amp; System.currentTimeMillis() - startTimeMs &gt; timeoutMs) {
            return false;
          }
    
          LOG.trace(String.format(&quot;Waiting for table(s) to complete loading: %s&quot;,
              Joiner.on(&quot;, &quot;).join(missingTbls)));
          getCatalog().waitForCatalogUpdate(MAX_CATALOG_UPDATE_WAIT_TIME_MS);
          missingTbls = getMissingTbls(missingTbls);
          // TODO: Check for query cancellation here.
        }
        return true;
      }</p></div>
    ";i:3;s:5380:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="csharp" style="font-family:monospace;"><span style="color: #0600FF; font-weight: bold;">extern</span> <span style="color: #666666;">&quot;C&quot;</span>
    JNIEXPORT jbyteArray JNICALL
    Java_com_cloudera_impala_service_FeSupport_NativePrioritizeLoad<span style="color: #008000;">&#40;</span>
        JNIEnv<span style="color: #008000;">*</span> env, jclass caller_class, jbyteArray thrift_struct<span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
      TPrioritizeLoadRequest request<span style="color: #008000;">;</span>
      DeserializeThriftMsg<span style="color: #008000;">&#40;</span>env, thrift_struct, <span style="color: #008000;">&amp;</span>request<span style="color: #008000;">&#41;</span><span style="color: #008000;">;</span>
    &nbsp;
      CatalogOpExecutor catalog_op_executor<span style="color: #008000;">&#40;</span>ExecEnv<span style="color: #008000;">::</span><span style="color: #0000FF;">GetInstance</span><span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span>, <span style="color: #0600FF; font-weight: bold;">NULL</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">;</span>
      TPrioritizeLoadResponse result<span style="color: #008000;">;</span>
      Status status <span style="color: #008000;">=</span> catalog_op_executor<span style="color: #008000;">.</span><span style="color: #0000FF;">PrioritizeLoad</span><span style="color: #008000;">&#40;</span>request, <span style="color: #008000;">&amp;</span>result<span style="color: #008000;">&#41;</span><span style="color: #008000;">;</span>
      <span style="color: #0600FF; font-weight: bold;">if</span> <span style="color: #008000;">&#40;</span><span style="color: #008000;">!</span>status<span style="color: #008000;">.</span><span style="color: #0000FF;">ok</span><span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
        LOG<span style="color: #008000;">&#40;</span>ERROR<span style="color: #008000;">&#41;</span> <span style="color: #008000;">&lt;&lt;</span> status<span style="color: #008000;">.</span><span style="color: #0000FF;">GetErrorMsg</span><span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">;</span>
        <span style="color: #008080; font-style: italic;">// Create a new Status, copy in this error, then update the result.</span>
        Status catalog_service_status<span style="color: #008000;">&#40;</span>result<span style="color: #008000;">.</span><span style="color: #0000FF;">status</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">;</span>
        catalog_service_status<span style="color: #008000;">.</span><span style="color: #0000FF;">AddError</span><span style="color: #008000;">&#40;</span>status<span style="color: #008000;">&#41;</span><span style="color: #008000;">;</span>
        status<span style="color: #008000;">.</span><span style="color: #0000FF;">ToThrift</span><span style="color: #008000;">&#40;</span><span style="color: #008000;">&amp;</span>result<span style="color: #008000;">.</span><span style="color: #0000FF;">status</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">;</span>
      <span style="color: #008000;">&#125;</span>
    &nbsp;
      jbyteArray result_bytes <span style="color: #008000;">=</span> <span style="color: #0600FF; font-weight: bold;">NULL</span><span style="color: #008000;">;</span>
      THROW_IF_ERROR_RET<span style="color: #008000;">&#40;</span>SerializeThriftMsg<span style="color: #008000;">&#40;</span>env, <span style="color: #008000;">&amp;</span>result, <span style="color: #008000;">&amp;</span>result_bytes<span style="color: #008000;">&#41;</span>, env,
                         JniUtil<span style="color: #008000;">::</span><span style="color: #0000FF;">internal_exc_class</span><span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span>, result_bytes<span style="color: #008000;">&#41;</span><span style="color: #008000;">;</span>
      <span style="color: #0600FF; font-weight: bold;">return</span> result_bytes<span style="color: #008000;">;</span>
    <span style="color: #008000;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">extern &quot;C&quot;
    JNIEXPORT jbyteArray JNICALL
    Java_com_cloudera_impala_service_FeSupport_NativePrioritizeLoad(
        JNIEnv* env, jclass caller_class, jbyteArray thrift_struct) {
      TPrioritizeLoadRequest request;
      DeserializeThriftMsg(env, thrift_struct, &amp;request);
    
      CatalogOpExecutor catalog_op_executor(ExecEnv::GetInstance(), NULL);
      TPrioritizeLoadResponse result;
      Status status = catalog_op_executor.PrioritizeLoad(request, &amp;result);
      if (!status.ok()) {
        LOG(ERROR) &lt;&lt; status.GetErrorMsg();
        // Create a new Status, copy in this error, then update the result.
        Status catalog_service_status(result.status);
        catalog_service_status.AddError(status);
        status.ToThrift(&amp;result.status);
      }
    
      jbyteArray result_bytes = NULL;
      THROW_IF_ERROR_RET(SerializeThriftMsg(env, &amp;result, &amp;result_bytes), env,
                         JniUtil::internal_exc_class(), result_bytes);
      return result_bytes;
    }</p></div>
    ";i:4;s:7333:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">  <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> load<span style="color: #009900;">&#40;</span>Table cachedEntry, HiveMetaStoreClient client,
          org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">hadoop</span>.<span style="color: #006633;">hive</span>.<span style="color: #006633;">metastore</span>.<span style="color: #006633;">api</span>.<span style="color: #006633;">Table</span> msTbl<span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">throws</span> TableLoadingException <span style="color: #009900;">&#123;</span>
        numHdfsFiles_ <span style="color: #339933;">=</span> <span style="color: #cc66cc;">0</span><span style="color: #339933;">;</span>
        totalHdfsBytes_ <span style="color: #339933;">=</span> <span style="color: #cc66cc;">0</span><span style="color: #339933;">;</span>
        LOG.<span style="color: #006633;">debug</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;load table: &quot;</span> <span style="color: #339933;">+</span> db_.<span style="color: #006633;">getName</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot;.&quot;</span> <span style="color: #339933;">+</span> name_<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    ...
    <span style="color: #006633;">loadColumns</span><span style="color: #009900;">&#40;</span>fieldSchemas, client<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">//这里有一些判断是否使用缓存的代码，如果是完全没有缓存，会通过以下方法获取</span>
            msPartitions.<span style="color: #006633;">addAll</span><span style="color: #009900;">&#40;</span>MetaStoreUtil.<span style="color: #006633;">fetchAllPartitions</span><span style="color: #009900;">&#40;</span>
                client, db_.<span style="color: #006633;">getName</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, name_, NUM_PARTITION_FETCH_RETRIES<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">//如果部分分区已经获取过了，会只获取未知分区的元素据</span>
            LOG.<span style="color: #006633;">info</span><span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span>.<span style="color: #006633;">format</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Incrementally refreshing %d/%d partitions.&quot;</span>,
                modifiedPartitionNames.<span style="color: #006633;">size</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, totalPartitions<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #666666; font-style: italic;">// No need to make the metastore call if no partitions are to be updated.</span>
            <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>modifiedPartitionNames.<span style="color: #006633;">size</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">&gt;</span> <span style="color: #cc66cc;">0</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
              <span style="color: #666666; font-style: italic;">// Now reload the the remaining partitions.</span>
              msPartitions.<span style="color: #006633;">addAll</span><span style="color: #009900;">&#40;</span>MetaStoreUtil.<span style="color: #006633;">fetchPartitionsByName</span><span style="color: #009900;">&#40;</span>client,
                  Lists.<span style="color: #006633;">newArrayList</span><span style="color: #009900;">&#40;</span>modifiedPartitionNames<span style="color: #009900;">&#41;</span>, db_.<span style="color: #006633;">getName</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, name_<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
    ...
    <span style="color: #666666; font-style: italic;">// 加载元素据和获取block信息</span>
          loadPartitions<span style="color: #009900;">&#40;</span>msPartitions, msTbl, oldFileDescMap<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #666666; font-style: italic;">// load table stats</span>
          numRows_ <span style="color: #339933;">=</span> getRowCount<span style="color: #009900;">&#40;</span>msTbl.<span style="color: #006633;">getParameters</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          LOG.<span style="color: #006633;">debug</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;table #rows=&quot;</span> <span style="color: #339933;">+</span> <span style="color: #003399;">Long</span>.<span style="color: #006633;">toString</span><span style="color: #009900;">&#40;</span>numRows_<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">  public void load(Table cachedEntry, HiveMetaStoreClient client,
          org.apache.hadoop.hive.metastore.api.Table msTbl) throws TableLoadingException {
        numHdfsFiles_ = 0;
        totalHdfsBytes_ = 0;
        LOG.debug(&quot;load table: &quot; + db_.getName() + &quot;.&quot; + name_);
    ...
    loadColumns(fieldSchemas, client);
    //这里有一些判断是否使用缓存的代码，如果是完全没有缓存，会通过以下方法获取
            msPartitions.addAll(MetaStoreUtil.fetchAllPartitions(
                client, db_.getName(), name_, NUM_PARTITION_FETCH_RETRIES));
    //如果部分分区已经获取过了，会只获取未知分区的元素据
            LOG.info(String.format(&quot;Incrementally refreshing %d/%d partitions.&quot;,
                modifiedPartitionNames.size(), totalPartitions));
            // No need to make the metastore call if no partitions are to be updated.
            if (modifiedPartitionNames.size() &gt; 0) {
              // Now reload the the remaining partitions.
              msPartitions.addAll(MetaStoreUtil.fetchPartitionsByName(client,
                  Lists.newArrayList(modifiedPartitionNames), db_.getName(), name_));
            }
    ...
    // 加载元素据和获取block信息
          loadPartitions(msPartitions, msTbl, oldFileDescMap);
          // load table stats
          numRows_ = getRowCount(msTbl.getParameters());
          LOG.debug(&quot;table #rows=&quot; + Long.toString(numRows_));
    }</p></div>
    ";i:5;s:18534:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">  <span style="color: #008000; font-style: italic; font-weight: bold;">/**
       * Loads the file block metadata for the given collection of FileDescriptors.
       * The FileDescriptors are passed as a Map of partition location to list of
       * files that exist under that directory.
       */</span>
      <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000066; font-weight: bold;">void</span> loadBlockMd<span style="color: #009900;">&#40;</span>Map<span style="color: #339933;">&lt;</span><span style="color: #003399;">String</span>, List<span style="color: #339933;">&lt;</span>FileDescriptor<span style="color: #339933;">&gt;&gt;</span> fileDescriptors<span style="color: #009900;">&#41;</span>
          <span style="color: #000000; font-weight: bold;">throws</span> <span style="color: #003399;">RuntimeException</span> <span style="color: #009900;">&#123;</span>
        Preconditions.<span style="color: #006633;">checkNotNull</span><span style="color: #009900;">&#40;</span>fileDescriptors<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        LOG.<span style="color: #006633;">debug</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;load block md for &quot;</span> <span style="color: #339933;">+</span> name_<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #666666; font-style: italic;">// Store all BlockLocations so they can be reused when loading the disk IDs.</span>
        List<span style="color: #339933;">&lt;</span>BlockLocation<span style="color: #339933;">&gt;</span> blockLocations <span style="color: #339933;">=</span> Lists.<span style="color: #006633;">newArrayList</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #666666; font-style: italic;">// loop over all files and record their block metadata, minus volume ids</span>
        <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> parentPath<span style="color: #339933;">:</span> fileDescriptors.<span style="color: #006633;">keySet</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">FileDescriptor</span> fileDescriptor<span style="color: #339933;">:</span> fileDescriptors.<span style="color: #006633;">get</span><span style="color: #009900;">&#40;</span>parentPath<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            Path p <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> Path<span style="color: #009900;">&#40;</span>parentPath, fileDescriptor.<span style="color: #006633;">getFileName</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            BlockLocation<span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> locations <span style="color: #339933;">=</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #339933;">;</span>
            <span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#123;</span>
              <span style="color: #666666; font-style: italic;">// 这里可能耗时，每个分区都获取文件信息（已缓存的不获取，但没看懂缓存的机制）</span>
              FileStatus fileStatus <span style="color: #339933;">=</span> DFS.<span style="color: #006633;">getFileStatus</span><span style="color: #009900;">&#40;</span>p<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
              <span style="color: #666666; font-style: italic;">// fileDescriptors should not contain directories.</span>
              Preconditions.<span style="color: #006633;">checkArgument</span><span style="color: #009900;">&#40;</span><span style="color: #339933;">!</span>fileStatus.<span style="color: #006633;">isDirectory</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
              <span style="color: #666666; font-style: italic;">// RPC操作</span>
              locations <span style="color: #339933;">=</span> DFS.<span style="color: #006633;">getFileBlockLocations</span><span style="color: #009900;">&#40;</span>fileStatus, <span style="color: #cc66cc;">0</span>, fileStatus.<span style="color: #006633;">getLen</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
              Preconditions.<span style="color: #006633;">checkNotNull</span><span style="color: #009900;">&#40;</span>locations<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
              blockLocations.<span style="color: #006633;">addAll</span><span style="color: #009900;">&#40;</span><span style="color: #003399;">Arrays</span>.<span style="color: #006633;">asList</span><span style="color: #009900;">&#40;</span>locations<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
              <span style="color: #666666; font-style: italic;">// Loop over all blocks in the file.</span>
              <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span>BlockLocation block<span style="color: #339933;">:</span> locations<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                <span style="color: #003399;">String</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> blockHostPorts <span style="color: #339933;">=</span> block.<span style="color: #006633;">getNames</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#123;</span>
                  blockHostPorts <span style="color: #339933;">=</span> block.<span style="color: #006633;">getNames</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">IOException</span> e<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                  <span style="color: #666666; font-style: italic;">// this shouldn't happen, getNames() doesn't throw anything</span>
                  <span style="color: #003399;">String</span> errorMsg <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;BlockLocation.getNames() failed:<span style="color: #000099; font-weight: bold;">\n</span>&quot;</span> <span style="color: #339933;">+</span> e.<span style="color: #006633;">getMessage</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                  LOG.<span style="color: #006633;">error</span><span style="color: #009900;">&#40;</span>errorMsg<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                  <span style="color: #000000; font-weight: bold;">throw</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">IllegalStateException</span><span style="color: #009900;">&#40;</span>errorMsg<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #009900;">&#125;</span>
                <span style="color: #666666; font-style: italic;">// Now enumerate all replicas of the block, adding any unknown hosts</span>
                <span style="color: #666666; font-style: italic;">// to hostIndex_ and the index for that host to replicaHostIdxs.</span>
                List<span style="color: #339933;">&lt;</span>Integer<span style="color: #339933;">&gt;</span> replicaHostIdxs <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> ArrayList<span style="color: #339933;">&lt;</span>Integer<span style="color: #339933;">&gt;</span><span style="color: #009900;">&#40;</span>blockHostPorts.<span style="color: #006633;">length</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> i <span style="color: #339933;">=</span> <span style="color: #cc66cc;">0</span><span style="color: #339933;">;</span> i <span style="color: #339933;">&lt;</span> blockHostPorts.<span style="color: #006633;">length</span><span style="color: #339933;">;</span> <span style="color: #339933;">++</span>i<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                  <span style="color: #003399;">String</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> ip_port <span style="color: #339933;">=</span> blockHostPorts<span style="color: #009900;">&#91;</span>i<span style="color: #009900;">&#93;</span>.<span style="color: #006633;">split</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;:&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                  Preconditions.<span style="color: #006633;">checkState</span><span style="color: #009900;">&#40;</span>ip_port.<span style="color: #006633;">length</span> <span style="color: #339933;">==</span> <span style="color: #cc66cc;">2</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                  TNetworkAddress network_address <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> TNetworkAddress<span style="color: #009900;">&#40;</span>ip_port<span style="color: #009900;">&#91;</span><span style="color: #cc66cc;">0</span><span style="color: #009900;">&#93;</span>,
                      <span style="color: #003399;">Integer</span>.<span style="color: #006633;">parseInt</span><span style="color: #009900;">&#40;</span>ip_port<span style="color: #009900;">&#91;</span><span style="color: #cc66cc;">1</span><span style="color: #009900;">&#93;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                  replicaHostIdxs.<span style="color: #006633;">add</span><span style="color: #009900;">&#40;</span>hostIndex_.<span style="color: #006633;">getIndex</span><span style="color: #009900;">&#40;</span>network_address<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #009900;">&#125;</span>
                fileDescriptor.<span style="color: #006633;">addFileBlock</span><span style="color: #009900;">&#40;</span>
                    <span style="color: #000000; font-weight: bold;">new</span> FileBlock<span style="color: #009900;">&#40;</span>block.<span style="color: #006633;">getOffset</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, block.<span style="color: #006633;">getLength</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, replicaHostIdxs<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
              <span style="color: #009900;">&#125;</span>
            <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">IOException</span> e<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
              <span style="color: #000000; font-weight: bold;">throw</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">RuntimeException</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;couldn't determine block locations for path '&quot;</span>
                  <span style="color: #339933;">+</span> p <span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot;':<span style="color: #000099; font-weight: bold;">\n</span>&quot;</span> <span style="color: #339933;">+</span> e.<span style="color: #006633;">getMessage</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, e<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
          <span style="color: #009900;">&#125;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>SUPPORTS_VOLUME_ID<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          LOG.<span style="color: #006633;">trace</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;loading disk ids for: &quot;</span> <span style="color: #339933;">+</span> getFullName<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">+</span>
              <span style="color: #0000ff;">&quot;. nodes: &quot;</span> <span style="color: #339933;">+</span> getNumNodes<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          loadDiskIds<span style="color: #009900;">&#40;</span>blockLocations, fileDescriptors<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          LOG.<span style="color: #006633;">trace</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;completed load of disk ids for: &quot;</span> <span style="color: #339933;">+</span> getFullName<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
      <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">  /**
       * Loads the file block metadata for the given collection of FileDescriptors.
       * The FileDescriptors are passed as a Map of partition location to list of
       * files that exist under that directory.
       */
      private void loadBlockMd(Map&lt;String, List&lt;FileDescriptor&gt;&gt; fileDescriptors)
          throws RuntimeException {
        Preconditions.checkNotNull(fileDescriptors);
        LOG.debug(&quot;load block md for &quot; + name_);
    
        // Store all BlockLocations so they can be reused when loading the disk IDs.
        List&lt;BlockLocation&gt; blockLocations = Lists.newArrayList();
    
        // loop over all files and record their block metadata, minus volume ids
        for (String parentPath: fileDescriptors.keySet()) {
          for (FileDescriptor fileDescriptor: fileDescriptors.get(parentPath)) {
            Path p = new Path(parentPath, fileDescriptor.getFileName());
            BlockLocation[] locations = null;
            try {
              // 这里可能耗时，每个分区都获取文件信息（已缓存的不获取，但没看懂缓存的机制）
              FileStatus fileStatus = DFS.getFileStatus(p);
              // fileDescriptors should not contain directories.
              Preconditions.checkArgument(!fileStatus.isDirectory());
              // RPC操作
              locations = DFS.getFileBlockLocations(fileStatus, 0, fileStatus.getLen());
              Preconditions.checkNotNull(locations);
              blockLocations.addAll(Arrays.asList(locations));
    
              // Loop over all blocks in the file.
              for (BlockLocation block: locations) {
                String[] blockHostPorts = block.getNames();
                try {
                  blockHostPorts = block.getNames();
                } catch (IOException e) {
                  // this shouldn't happen, getNames() doesn't throw anything
                  String errorMsg = &quot;BlockLocation.getNames() failed:\n&quot; + e.getMessage();
                  LOG.error(errorMsg);
                  throw new IllegalStateException(errorMsg);
                }
                // Now enumerate all replicas of the block, adding any unknown hosts
                // to hostIndex_ and the index for that host to replicaHostIdxs.
                List&lt;Integer&gt; replicaHostIdxs = new ArrayList&lt;Integer&gt;(blockHostPorts.length);
                for (int i = 0; i &lt; blockHostPorts.length; ++i) {
                  String[] ip_port = blockHostPorts[i].split(&quot;:&quot;);
                  Preconditions.checkState(ip_port.length == 2);
                  TNetworkAddress network_address = new TNetworkAddress(ip_port[0],
                      Integer.parseInt(ip_port[1]));
                  replicaHostIdxs.add(hostIndex_.getIndex(network_address));
                }
                fileDescriptor.addFileBlock(
                    new FileBlock(block.getOffset(), block.getLength(), replicaHostIdxs));
              }
            } catch (IOException e) {
              throw new RuntimeException(&quot;couldn't determine block locations for path '&quot;
                  + p + &quot;':\n&quot; + e.getMessage(), e);
            }
          }
        }
    
        if (SUPPORTS_VOLUME_ID) {
          LOG.trace(&quot;loading disk ids for: &quot; + getFullName() +
              &quot;. nodes: &quot; + getNumNodes());
          loadDiskIds(blockLocations, fileDescriptors);
          LOG.trace(&quot;completed load of disk ids for: &quot; + getFullName());
        }
      }</p></div>
    ";}
categories:
  - hadoop
tags:
  - hadoop
  - impala

---
上一篇文章看到 requestTblLoadAndWait 速度缓慢，继续分析。先上日志
<pre lang="other" escaped="true"># impalad日志
I0103 15:09:35.503356 27319 impala-beeswax-server.cc:170] query(): query=select distinct(disp_id) from default_impala.kpi_disp_user_info_stat_tb where pt='2014-04-08'
I0103 15:11:36.109915 27319 Frontend.java:779] Missing tables were not received in 120000ms. Load request will be retried.
I0103 15:11:36.110705 27319 Frontend.java:709] Requesting prioritized load of table(s): default_impala.kpi_disp_user_info_stat_tb
I0103 15:11:50.778054 27319 Frontend.java:833] create plan
I0103 15:11:50.806649 27319 HdfsScanNode.java:571] collecting partitions for table kpi_disp_user_info_stat_tb
I0103 15:11:51.070816 27319 impala-server.cc:590] Execution request: TExecRequest {



# catalog日志
I0103 15:09:35.892182 29165 rpc-trace.cc:133] RPC call: CatalogService.PrioritizeLoad(from ::ffff:127.0.0.1:44323)
I0103 15:09:39.563268 29185 HdfsTable.java:916] load table: default_impala.kpi_disp_user_info_stat_tb
I0103 15:10:48.357046 29185 HdfsTable.java:234] load block md for kpi_disp_user_info_stat_tb
I0103 15:11:36.110947 29165 rpc-trace.cc:133] RPC call: CatalogService.PrioritizeLoad(from ::ffff:127.0.0.1:44323)
I0103 15:11:48.948714 29185 HdfsTable.java:1056] table #rows=-1


# hive metastore日志
2015-01-03 15:09:38,991 INFO org.apache.hadoop.hive.metastore.HiveMetaStore: 54032: source:/IP地址 get_table : db=default_impala tbl=kpi_disp_user_info_stat_tb
2015-01-03 15:09:39,848 INFO org.apache.hadoop.hive.metastore.HiveMetaStore: 54032: source:/IP地址 get_partition_names : db=default_impala tbl=kpi_disp_user_info_stat_tb
2015-01-03 15:09:39,902 INFO org.apache.hadoop.hive.metastore.HiveMetaStore: 54032: source:/IP地址 get_partitions_by_names : db=default_impala tbl=kpi_disp_user_info_stat_tb
2015-01-03 15:09:52,839 INFO org.apache.hadoop.hive.metastore.HiveMetaStore: 54032: source:/IP地址 get_partitions_by_names : db=default_impala tbl=kpi_disp_user_info_stat_tb
2015-01-03 15:10:05,383 INFO org.apache.hadoop.hive.metastore.HiveMetaStore: 54032: source:/IP地址 get_partitions_by_names : db=default_impala tbl=kpi_disp_user_info_stat_tb</pre>
这次加多了metastore的日志进来
在15:09:35提交了查询语句，可以看到impalad和catalog都有一条日志，metastore在3秒后有一条日志（3秒的原因是hive metastore一个bug，我在测试时没修复，但不影响分析）。
catalogd开始获取这个表的元素据以及文件block信息，15:09:39至15:10:48从metastore获取完元素据，15:10:48开始获取文件block信息。直到15:11:48完成，期间因为impalad获取元素据超过120秒，15:11:36重新获取了一次。
<pre lang="java" escaped="true">// Frontend.java
  private boolean requestTblLoadAndWait(Set&lt;TableName&gt; requestedTbls, long timeoutMs)
      throws InternalException {
// impala本地缓存了元素据，每个表有一个版本号。本地的缓存一开始只缓存表名，分区信息等都没有缓存
    Set&lt;TableName&gt; missingTbls = getMissingTbls(requestedTbls);
    // There are no missing tables, return and avoid making an RPC to the CatalogServer.
    if (missingTbls.isEmpty()) return true;

    // Call into the CatalogServer and request the required tables be loaded.
    LOG.info(String.format("Requesting prioritized load of table(s): %s",
        Joiner.on(", ").join(missingTbls)));
// 这里通过jni的方式调用c++写的代码，与catalogd通信获取元素据
    TStatus status = FeSupport.PrioritizeLoad(missingTbls);
    if (status.getStatus_code() != TStatusCode.OK) {
      throw new InternalException("Error requesting prioritized load: " +
          Joiner.on("\n").join(status.getError_msgs()));
    }

    long startTimeMs = System.currentTimeMillis();
    // Wait until all the required tables are loaded in the Impalad's catalog cache.
    // 检查是不是在本地缓存里了
    while (!missingTbls.isEmpty()) {
      // Check if the timeout has been reached.
      if (timeoutMs &gt; 0 && System.currentTimeMillis() - startTimeMs &gt; timeoutMs) {
        return false;
      }

      LOG.trace(String.format("Waiting for table(s) to complete loading: %s",
          Joiner.on(", ").join(missingTbls)));
      getCatalog().waitForCatalogUpdate(MAX_CATALOG_UPDATE_WAIT_TIME_MS);
      missingTbls = getMissingTbls(missingTbls);
      // TODO: Check for query cancellation here.
    }
    return true;
  }</pre>
继续看FeSupport.PrioritizeLoad的代码，这里实际是调用c++的代码，在fe-support.cc里，直接看
<pre lang="csharp" escaped="true">extern "C"
JNIEXPORT jbyteArray JNICALL
Java_com_cloudera_impala_service_FeSupport_NativePrioritizeLoad(
    JNIEnv* env, jclass caller_class, jbyteArray thrift_struct) {
  TPrioritizeLoadRequest request;
  DeserializeThriftMsg(env, thrift_struct, &request);

  CatalogOpExecutor catalog_op_executor(ExecEnv::GetInstance(), NULL);
  TPrioritizeLoadResponse result;
  Status status = catalog_op_executor.PrioritizeLoad(request, &result);
  if (!status.ok()) {
    LOG(ERROR) &lt;&lt; status.GetErrorMsg();
    // Create a new Status, copy in this error, then update the result.
    Status catalog_service_status(result.status);
    catalog_service_status.AddError(status);
    status.ToThrift(&result.status);
  }

  jbyteArray result_bytes = NULL;
  THROW_IF_ERROR_RET(SerializeThriftMsg(env, &result, &result_bytes), env,
                     JniUtil::internal_exc_class(), result_bytes);
  return result_bytes;
}</pre>
c++代码没看懂，不知道怎么调用到了catalogd的代码，不管了，从日志看执行了这行代码HdfsTable.java:916
<pre lang="java" escaped="true">public void load(Table cachedEntry, HiveMetaStoreClient client,
      org.apache.hadoop.hive.metastore.api.Table msTbl) throws TableLoadingException {
    numHdfsFiles_ = 0;
    totalHdfsBytes_ = 0;
    LOG.debug("load table: " + db_.getName() + "." + name_);
...
loadColumns(fieldSchemas, client);
//这里有一些判断是否使用缓存的代码，如果是完全没有缓存，会通过以下方法获取
        msPartitions.addAll(MetaStoreUtil.fetchAllPartitions(
            client, db_.getName(), name_, NUM_PARTITION_FETCH_RETRIES));
//如果部分分区已经获取过了，会只获取未知分区的元素据
        LOG.info(String.format("Incrementally refreshing %d/%d partitions.",
            modifiedPartitionNames.size(), totalPartitions));
        // No need to make the metastore call if no partitions are to be updated.
        if (modifiedPartitionNames.size() &gt; 0) {
          // Now reload the the remaining partitions.
          msPartitions.addAll(MetaStoreUtil.fetchPartitionsByName(client,
              Lists.newArrayList(modifiedPartitionNames), db_.getName(), name_));
        }
...
// 加载元素据和获取block信息
      loadPartitions(msPartitions, msTbl, oldFileDescMap);
      // load table stats
      numRows_ = getRowCount(msTbl.getParameters());
      LOG.debug("table #rows=" + Long.toString(numRows_));
}</pre>
在MetaStoreUtil.fetchAllPartitions方法里会先get\_partition\_names获取全部的分区名，然后再分批get\_partitions\_by\_names来获取分区的全部信息。每次RPC获取的分区数量由参数HiveConf.ConfVars.METASTORE\_BATCH\_RETRIEVE\_TABLE\_PARTITION\_MAX指定，默认1000个分区一次。
在loadPartitions方法中，会创建一些分区对象和搜集分区的行数（这个应该是要用comput stat才有值，默认搜集不到），然后再调用loadBlockMd(fileDescsToLoad);方法
<pre lang="java" escaped="true">/**
   * Loads the file block metadata for the given collection of FileDescriptors.
   * The FileDescriptors are passed as a Map of partition location to list of
   * files that exist under that directory.
   */
  private void loadBlockMd(Map&lt;String, List&lt;FileDescriptor&gt;&gt; fileDescriptors)
      throws RuntimeException {
    Preconditions.checkNotNull(fileDescriptors);
    LOG.debug("load block md for " + name_);

    // Store all BlockLocations so they can be reused when loading the disk IDs.
    List&lt;BlockLocation&gt; blockLocations = Lists.newArrayList();

    // loop over all files and record their block metadata, minus volume ids
    for (String parentPath: fileDescriptors.keySet()) {
      for (FileDescriptor fileDescriptor: fileDescriptors.get(parentPath)) {
        Path p = new Path(parentPath, fileDescriptor.getFileName());
        BlockLocation[] locations = null;
        try {
          // 这里可能耗时，每个分区都获取文件信息（已缓存的不获取，但没看懂缓存的机制）
          FileStatus fileStatus = DFS.getFileStatus(p);
          // fileDescriptors should not contain directories.
          Preconditions.checkArgument(!fileStatus.isDirectory());
          // RPC操作
          locations = DFS.getFileBlockLocations(fileStatus, 0, fileStatus.getLen());
          Preconditions.checkNotNull(locations);
          blockLocations.addAll(Arrays.asList(locations));

          // Loop over all blocks in the file.
          for (BlockLocation block: locations) {
            String[] blockHostPorts = block.getNames();
            try {
              blockHostPorts = block.getNames();
            } catch (IOException e) {
              // this shouldn't happen, getNames() doesn't throw anything
              String errorMsg = "BlockLocation.getNames() failed:\n" + e.getMessage();
              LOG.error(errorMsg);
              throw new IllegalStateException(errorMsg);
            }
            // Now enumerate all replicas of the block, adding any unknown hosts
            // to hostIndex_ and the index for that host to replicaHostIdxs.
            List&lt;Integer&gt; replicaHostIdxs = new ArrayList&lt;Integer&gt;(blockHostPorts.length);
            for (int i = 0; i &lt; blockHostPorts.length; ++i) {
              String[] ip_port = blockHostPorts[i].split(":");
              Preconditions.checkState(ip_port.length == 2);
              TNetworkAddress network_address = new TNetworkAddress(ip_port[0],
                  Integer.parseInt(ip_port[1]));
              replicaHostIdxs.add(hostIndex_.getIndex(network_address));
            }
            fileDescriptor.addFileBlock(
                new FileBlock(block.getOffset(), block.getLength(), replicaHostIdxs));
          }
        } catch (IOException e) {
          throw new RuntimeException("couldn't determine block locations for path '"
              + p + "':\n" + e.getMessage(), e);
        }
      }
    }

    if (SUPPORTS_VOLUME_ID) {
      LOG.trace("loading disk ids for: " + getFullName() +
          ". nodes: " + getNumNodes());
      loadDiskIds(blockLocations, fileDescriptors);
      LOG.trace("completed load of disk ids for: " + getFullName());
    }
  }</pre>
&nbsp;
另外找到一个有一点关系的issue， IMPALA-1480 [Slow DDL statements for tables with large number of partitions][1]
google group上的讨论 https://groups.google.com/a/cloudera.org/forum/#!topic/impala-user/Xv8d2jndzZ0
<div style="color: #222222;">  Dimitris：</div>
<div style="color: #222222;">  It looks like an issue I am currently working on (<a style="color: #6611cc;" href="https://issues.cloudera.org/browse/IMPALA-1480" target="_blank">https://issues.cloudera.org/<wbr />browse/IMPALA-1480</a>). I have a patch in flight that significantly improves DDL and INSERT statements for partitioned tables. Currently, the issue is that we force-reload the entire table metadata even though only few partitions have been modified.</div>
<div style="color: #222222;">  不过他说的是DDL语句，会强制加载整个元数据，尽管只改几个分区，和这里的查询类似。</div>
## 结论

对于很多分区的表，获取全部元素据以及block信息花费很多时间导致查询变慢。如果impala能够针对查询只获取需要用到的分区信息将会加快很多。
&nbsp;

 [1]: https://issues.cloudera.org/browse/IMPALA-1480