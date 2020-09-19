---
title: impala因为invalidate语句导致执行DDL语句卡住
author: fatkun
type: post
date: 2015-02-01T16:06:11+00:00
url: /2015/02/impala-invalidate-metadata.html
duoshuo_thread_id:
  - 6300410881872233217
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:1767:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">  <span style="color: #008000; font-style: italic; font-weight: bold;">/**
       * Executes a TResetMetadataRequest and returns the result as a
       * TResetMetadataResponse. Based on the request parameters, this operation
       * may do one of three things:
       * 1) invalidate the entire catalog, forcing the metadata for all catalog
       *    objects to be reloaded.
       * 2) invalidate a specific table, forcing the metadata to be reloaded
       *    on the next access.
       * 3) perform a synchronous incremental refresh of a specific table.
       *
       * For details on the specific commands see comments on their respective
       * methods in CatalogServiceCatalog.java.
       */</span>
      <span style="color: #000000; font-weight: bold;">public</span> TResetMetadataResponse execResetMetadata<span style="color: #009900;">&#40;</span>TResetMetadataRequest req<span style="color: #009900;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">  /**
       * Executes a TResetMetadataRequest and returns the result as a
       * TResetMetadataResponse. Based on the request parameters, this operation
       * may do one of three things:
       * 1) invalidate the entire catalog, forcing the metadata for all catalog
       *    objects to be reloaded.
       * 2) invalidate a specific table, forcing the metadata to be reloaded
       *    on the next access.
       * 3) perform a synchronous incremental refresh of a specific table.
       *
       * For details on the specific commands see comments on their respective
       * methods in CatalogServiceCatalog.java.
       */
      public TResetMetadataResponse execResetMetadata(TResetMetadataRequest req)</p></div>
    ";i:2;s:19926:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #666666; font-style: italic;">///impala-fe/src/main/java/com/cloudera/impala/catalog/CatalogServiceCatalog.java</span>
    &nbsp;
      <span style="color: #008000; font-style: italic; font-weight: bold;">/**
       * Resets this catalog instance by clearing all cached table and database metadata.
       */</span>
      <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> reset<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">throws</span> CatalogException <span style="color: #009900;">&#123;</span>
        catalogLock_.<span style="color: #006633;">writeLock</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">lock</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#123;</span>
          nextTableId_.<span style="color: #006633;">set</span><span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">0</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
          <span style="color: #666666; font-style: italic;">// Since UDFs/UDAs are not persisted in the metastore, we won't clear</span>
          <span style="color: #666666; font-style: italic;">// them across reset. To do this, we store all the functions before</span>
          <span style="color: #666666; font-style: italic;">// clearing and restore them after.</span>
          <span style="color: #666666; font-style: italic;">// TODO: Everything about this. Persist them.</span>
          List<span style="color: #339933;">&lt;</span>Pair<span style="color: #339933;">&lt;</span><span style="color: #003399;">String</span>, HashMap<span style="color: #339933;">&lt;</span><span style="color: #003399;">String</span>, List<span style="color: #339933;">&lt;</span>Function<span style="color: #339933;">&gt;&gt;&gt;&gt;</span> functions <span style="color: #339933;">=</span>
              Lists.<span style="color: #006633;">newArrayList</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span>Db db<span style="color: #339933;">:</span> dbCache_.<span style="color: #006633;">get</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">values</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>db.<span style="color: #006633;">numFunctions</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">==</span> <span style="color: #cc66cc;">0</span><span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">continue</span><span style="color: #339933;">;</span>
            functions.<span style="color: #006633;">add</span><span style="color: #009900;">&#40;</span>Pair.<span style="color: #006633;">create</span><span style="color: #009900;">&#40;</span>db.<span style="color: #006633;">getName</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, db.<span style="color: #006633;">getAllFunctions</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #009900;">&#125;</span>
    &nbsp;
          <span style="color: #666666; font-style: italic;">// Build a new DB cache, populate it, and replace the existing cache in one</span>
          <span style="color: #666666; font-style: italic;">// step.</span>
          ConcurrentHashMap<span style="color: #339933;">&lt;</span><span style="color: #003399;">String</span>, Db<span style="color: #339933;">&gt;</span> newDbCache <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> ConcurrentHashMap<span style="color: #339933;">&lt;</span><span style="color: #003399;">String</span>, Db<span style="color: #339933;">&gt;</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          List<span style="color: #339933;">&lt;</span>TTableName<span style="color: #339933;">&gt;</span> tblsToBackgroundLoad <span style="color: #339933;">=</span> Lists.<span style="color: #006633;">newArrayList</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          MetaStoreClient msClient <span style="color: #339933;">=</span> metaStoreClientPool_.<span style="color: #006633;">getClient</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> dbName<span style="color: #339933;">:</span> msClient.<span style="color: #006633;">getHiveClient</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getAllDatabases</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
              Db db <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> Db<span style="color: #009900;">&#40;</span>dbName, <span style="color: #000000; font-weight: bold;">this</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
              db.<span style="color: #006633;">setCatalogVersion</span><span style="color: #009900;">&#40;</span>incrementAndGetCatalogVersion<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
              newDbCache.<span style="color: #006633;">put</span><span style="color: #009900;">&#40;</span>db.<span style="color: #006633;">getName</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">toLowerCase</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, db<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
              <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> tableName<span style="color: #339933;">:</span> msClient.<span style="color: #006633;">getHiveClient</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getAllTables</span><span style="color: #009900;">&#40;</span>dbName<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                Table incompleteTbl <span style="color: #339933;">=</span> IncompleteTable.<span style="color: #006633;">createUninitializedTable</span><span style="color: #009900;">&#40;</span>
                    getNextTableId<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, db, tableName<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                incompleteTbl.<span style="color: #006633;">setCatalogVersion</span><span style="color: #009900;">&#40;</span>incrementAndGetCatalogVersion<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                db.<span style="color: #006633;">addTable</span><span style="color: #009900;">&#40;</span>incompleteTbl<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>loadInBackground_<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                  tblsToBackgroundLoad.<span style="color: #006633;">add</span><span style="color: #009900;">&#40;</span>
                      <span style="color: #000000; font-weight: bold;">new</span> TTableName<span style="color: #009900;">&#40;</span>dbName.<span style="color: #006633;">toLowerCase</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, tableName.<span style="color: #006633;">toLowerCase</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #009900;">&#125;</span>
              <span style="color: #009900;">&#125;</span>
            <span style="color: #009900;">&#125;</span>
          <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">finally</span> <span style="color: #009900;">&#123;</span>
            msClient.<span style="color: #006633;">release</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #009900;">&#125;</span>
    &nbsp;
          <span style="color: #666666; font-style: italic;">// Restore UDFs/UDAs.</span>
          <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span>Pair<span style="color: #339933;">&lt;</span><span style="color: #003399;">String</span>, HashMap<span style="color: #339933;">&lt;</span><span style="color: #003399;">String</span>, List<span style="color: #339933;">&lt;</span>Function<span style="color: #339933;">&gt;&gt;&gt;</span> dbFns<span style="color: #339933;">:</span> functions<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            Db db <span style="color: #339933;">=</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #339933;">;</span>
            <span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#123;</span>
              db <span style="color: #339933;">=</span> newDbCache.<span style="color: #006633;">get</span><span style="color: #009900;">&#40;</span>dbFns.<span style="color: #006633;">first</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">Exception</span> e<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
              <span style="color: #000000; font-weight: bold;">continue</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
            <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>db <span style="color: #339933;">==</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
              <span style="color: #666666; font-style: italic;">// DB no longer exists - it was probably dropped externally.</span>
              <span style="color: #666666; font-style: italic;">// TODO: We could restore this DB and then add the functions back?</span>
              <span style="color: #000000; font-weight: bold;">continue</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
    &nbsp;
            <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span>List<span style="color: #339933;">&lt;</span>Function<span style="color: #339933;">&gt;</span> fns<span style="color: #339933;">:</span> dbFns.<span style="color: #006633;">second</span>.<span style="color: #006633;">values</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
              <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span>Function fn<span style="color: #339933;">:</span> fns<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>fn.<span style="color: #006633;">getBinaryType</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">==</span> TFunctionBinaryType.<span style="color: #006633;">BUILTIN</span><span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">continue</span><span style="color: #339933;">;</span>
                fn.<span style="color: #006633;">setCatalogVersion</span><span style="color: #009900;">&#40;</span>incrementAndGetCatalogVersion<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                db.<span style="color: #006633;">addFunction</span><span style="color: #009900;">&#40;</span>fn<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
              <span style="color: #009900;">&#125;</span>
            <span style="color: #009900;">&#125;</span>
          <span style="color: #009900;">&#125;</span>
          dbCache_.<span style="color: #006633;">set</span><span style="color: #009900;">&#40;</span>newDbCache<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #666666; font-style: italic;">// Submit tables for background loading.</span>
          <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span>TTableName tblName<span style="color: #339933;">:</span> tblsToBackgroundLoad<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            tableLoadingMgr_.<span style="color: #006633;">backgroundLoad</span><span style="color: #009900;">&#40;</span>tblName<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #009900;">&#125;</span>
        <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">Exception</span> e<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          LOG.<span style="color: #006633;">error</span><span style="color: #009900;">&#40;</span>e<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #000000; font-weight: bold;">throw</span> <span style="color: #000000; font-weight: bold;">new</span> CatalogException<span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Error initializing Catalog. Catalog may be empty.&quot;</span>, e<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">finally</span> <span style="color: #009900;">&#123;</span>
          catalogLock_.<span style="color: #006633;">writeLock</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">unlock</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
      <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">///impala-fe/src/main/java/com/cloudera/impala/catalog/CatalogServiceCatalog.java
    
      /**
       * Resets this catalog instance by clearing all cached table and database metadata.
       */
      public void reset() throws CatalogException {
        catalogLock_.writeLock().lock();
        try {
          nextTableId_.set(0);
    
          // Since UDFs/UDAs are not persisted in the metastore, we won't clear
          // them across reset. To do this, we store all the functions before
          // clearing and restore them after.
          // TODO: Everything about this. Persist them.
          List&lt;Pair&lt;String, HashMap&lt;String, List&lt;Function&gt;&gt;&gt;&gt; functions =
              Lists.newArrayList();
          for (Db db: dbCache_.get().values()) {
            if (db.numFunctions() == 0) continue;
            functions.add(Pair.create(db.getName(), db.getAllFunctions()));
          }
    
          // Build a new DB cache, populate it, and replace the existing cache in one
          // step.
          ConcurrentHashMap&lt;String, Db&gt; newDbCache = new ConcurrentHashMap&lt;String, Db&gt;();
          List&lt;TTableName&gt; tblsToBackgroundLoad = Lists.newArrayList();
          MetaStoreClient msClient = metaStoreClientPool_.getClient();
          try {
            for (String dbName: msClient.getHiveClient().getAllDatabases()) {
              Db db = new Db(dbName, this);
              db.setCatalogVersion(incrementAndGetCatalogVersion());
              newDbCache.put(db.getName().toLowerCase(), db);
    
              for (String tableName: msClient.getHiveClient().getAllTables(dbName)) {
                Table incompleteTbl = IncompleteTable.createUninitializedTable(
                    getNextTableId(), db, tableName);
                incompleteTbl.setCatalogVersion(incrementAndGetCatalogVersion());
                db.addTable(incompleteTbl);
                if (loadInBackground_) {
                  tblsToBackgroundLoad.add(
                      new TTableName(dbName.toLowerCase(), tableName.toLowerCase()));
                }
              }
            }
          } finally {
            msClient.release();
          }
    
          // Restore UDFs/UDAs.
          for (Pair&lt;String, HashMap&lt;String, List&lt;Function&gt;&gt;&gt; dbFns: functions) {
            Db db = null;
            try {
              db = newDbCache.get(dbFns.first);
            } catch (Exception e) {
              continue;
            }
            if (db == null) {
              // DB no longer exists - it was probably dropped externally.
              // TODO: We could restore this DB and then add the functions back?
              continue;
            }
    
            for (List&lt;Function&gt; fns: dbFns.second.values()) {
              for (Function fn: fns) {
                if (fn.getBinaryType() == TFunctionBinaryType.BUILTIN) continue;
                fn.setCatalogVersion(incrementAndGetCatalogVersion());
                db.addFunction(fn);
              }
            }
          }
          dbCache_.set(newDbCache);
          // Submit tables for background loading.
          for (TTableName tblName: tblsToBackgroundLoad) {
            tableLoadingMgr_.backgroundLoad(tblName);
          }
        } catch (Exception e) {
          LOG.error(e);
          throw new CatalogException(&quot;Error initializing Catalog. Catalog may be empty.&quot;, e);
        } finally {
          catalogLock_.writeLock().unlock();
        }
      }</p></div>
    ";}
categories:
  - hadoop
tags:
  - hadoop
  - impala

---
## 现象

impala突然无法执行DDL语句，一直卡住，累积的很多任务。初步怀疑impala并发有问题，采取了一些减少并发的方法，有一点作用，但故障没有完全消除。
## 排查

怀疑超时时间太短（2分钟），修改代码更改超时时间到10分钟，没效果，但发现一个规律，有些任务在超时后17秒成功。
开启详细debug日志。发现impalad的日志显示是获取元数据超时，但发现catalogd的获取元素据只需要10+秒。catalogd没有把结果返回给impalad？
这里解释一下impalad和catalogd的关系。客户端直接访问impalad，impalad在本地缓存找不到这个表的元素据，就会向catalogd发起请求，catalogd从hive metastore获取元数据以及namenode获取block信息，返回给impalad。impalad在获取的过程中，每隔2秒检查一下本地的缓存，看这个表获取完元素据了没有，直到超时。
但是。。。由于代码太复杂，C++和java的代码互相调用，我看不懂传递的过程。期望从代码了解为什么丢了结果是没办法了。另外还有一个办法是在代码里加上一些跟踪的日志重新编译，但耗时可能很长，没有继续下去。
偶然发现有些卡住的语句，在我执行refresh语句时居然不卡了。想起我们执行语句前加了-r参数，每次都会执行invalidate metadata语句，猜想是不是因为这个引起。取消这个参数后一切正常，之前加这个参数是为了避免有些表没有更新元素据，可能会导致table not found的错误。（现在不需要这个参数，建表和更改时会执行这个语句）
## 代码分析

由于看不懂全部代码，所以以下分析可能有误。来看一下invalidate metadata做了什么。从注释来看应该没找错方法=。=
<pre lang="java" escaped="true">/**
   * Executes a TResetMetadataRequest and returns the result as a
   * TResetMetadataResponse. Based on the request parameters, this operation
   * may do one of three things:
   * 1) invalidate the entire catalog, forcing the metadata for all catalog
   *    objects to be reloaded.
   * 2) invalidate a specific table, forcing the metadata to be reloaded
   *    on the next access.
   * 3) perform a synchronous incremental refresh of a specific table.
   *
   * For details on the specific commands see comments on their respective
   * methods in CatalogServiceCatalog.java.
   */
  public TResetMetadataResponse execResetMetadata(TResetMetadataRequest req)</pre>
这个方法里调用了catalog_.reset();
<pre lang="java" escaped="true">///impala-fe/src/main/java/com/cloudera/impala/catalog/CatalogServiceCatalog.java

  /**
   * Resets this catalog instance by clearing all cached table and database metadata.
   */
  public void reset() throws CatalogException {
    catalogLock_.writeLock().lock();
    try {
      nextTableId_.set(0);

      // Since UDFs/UDAs are not persisted in the metastore, we won't clear
      // them across reset. To do this, we store all the functions before
      // clearing and restore them after.
      // TODO: Everything about this. Persist them.
      List&lt;Pair&lt;String, HashMap&lt;String, List&lt;Function&gt;&gt;&gt;&gt; functions =
          Lists.newArrayList();
      for (Db db: dbCache_.get().values()) {
        if (db.numFunctions() == 0) continue;
        functions.add(Pair.create(db.getName(), db.getAllFunctions()));
      }

      // Build a new DB cache, populate it, and replace the existing cache in one
      // step.
      ConcurrentHashMap&lt;String, Db&gt; newDbCache = new ConcurrentHashMap&lt;String, Db&gt;();
      List&lt;TTableName&gt; tblsToBackgroundLoad = Lists.newArrayList();
      MetaStoreClient msClient = metaStoreClientPool_.getClient();
      try {
        for (String dbName: msClient.getHiveClient().getAllDatabases()) {
          Db db = new Db(dbName, this);
          db.setCatalogVersion(incrementAndGetCatalogVersion());
          newDbCache.put(db.getName().toLowerCase(), db);

          for (String tableName: msClient.getHiveClient().getAllTables(dbName)) {
            Table incompleteTbl = IncompleteTable.createUninitializedTable(
                getNextTableId(), db, tableName);
            incompleteTbl.setCatalogVersion(incrementAndGetCatalogVersion());
            db.addTable(incompleteTbl);
            if (loadInBackground_) {
              tblsToBackgroundLoad.add(
                  new TTableName(dbName.toLowerCase(), tableName.toLowerCase()));
            }
          }
        }
      } finally {
        msClient.release();
      }

      // Restore UDFs/UDAs.
      for (Pair&lt;String, HashMap&lt;String, List&lt;Function&gt;&gt;&gt; dbFns: functions) {
        Db db = null;
        try {
          db = newDbCache.get(dbFns.first);
        } catch (Exception e) {
          continue;
        }
        if (db == null) {
          // DB no longer exists - it was probably dropped externally.
          // TODO: We could restore this DB and then add the functions back?
          continue;
        }

        for (List&lt;Function&gt; fns: dbFns.second.values()) {
          for (Function fn: fns) {
            if (fn.getBinaryType() == TFunctionBinaryType.BUILTIN) continue;
            fn.setCatalogVersion(incrementAndGetCatalogVersion());
            db.addFunction(fn);
          }
        }
      }
      dbCache_.set(newDbCache);
      // Submit tables for background loading.
      for (TTableName tblName: tblsToBackgroundLoad) {
        tableLoadingMgr_.backgroundLoad(tblName);
      }
    } catch (Exception e) {
      LOG.error(e);
      throw new CatalogException("Error initializing Catalog. Catalog may be empty.", e);
    } finally {
      catalogLock_.writeLock().unlock();
    }
  }</pre>
reset里面，dbCache\_可能是impalad的本地缓存(又或者是catalogd的&#8230;)，里面存有各个表的元数据信息（包含block信息）。这里重新从metastore获取了所有的表信息（不包含分区和block信息），这些表称之为incomplete Table，因为还没有获取分区和block信息。如果启用了loadInBackground，就会在后台获取分区等信息，没启用的话就等使用的时候获取。最后设为dbCache\_，相当于清空所有元素据缓存。
## 结论

从代码上解释，impalad在向catalogd获取元素据信息过程中，执行了invalidate metadata，导致本地缓存清空，impalad在检查缓存时，发现元素据还是空的，一直等到超时重试。这也能解释并发多时，一直失败，因为出现invalidate metadata的概率多了。
另外取消这个后，应该能提高impalad的查询速度，能够利用本地缓存。
## 后续关注

去掉这个参数后会不会导致元素据不同步，导致读取不到最新的数据。