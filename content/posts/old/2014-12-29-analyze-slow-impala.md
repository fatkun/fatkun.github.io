---
title: 从日志分析impala查询慢的原因（1）
author: fatkun
type: post
date: 2014-12-28T18:42:52+00:00
url: /2014/12/analyze-slow-impala.html
duoshuo_thread_id:
  - 6300410881607992065
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:8782:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">  <span style="color: #000000; font-weight: bold;">private</span> AnalysisContext.<span style="color: #006633;">AnalysisResult</span> analyzeStmt<span style="color: #009900;">&#40;</span>TQueryCtx queryCtx<span style="color: #009900;">&#41;</span>
          <span style="color: #000000; font-weight: bold;">throws</span> AnalysisException, InternalException, AuthorizationException <span style="color: #009900;">&#123;</span>
        AnalysisContext analysisCtx <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> AnalysisContext<span style="color: #009900;">&#40;</span>impaladCatalog_, queryCtx,
            authzConfig_<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        LOG.<span style="color: #006633;">debug</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;analyze query &quot;</span> <span style="color: #339933;">+</span> queryCtx.<span style="color: #006633;">request</span>.<span style="color: #006633;">stmt</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #666666; font-style: italic;">// Run analysis in a loop until it any of the following events occur:</span>
        <span style="color: #666666; font-style: italic;">// 1) Analysis completes successfully.</span>
        <span style="color: #666666; font-style: italic;">// 2) Analysis fails with an AnalysisException AND there are no missing tables.</span>
        <span style="color: #666666; font-style: italic;">// 3) Analysis fails with an AuthorizationException.</span>
        <span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #000000; font-weight: bold;">while</span> <span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">true</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#123;</span>
              analysisCtx.<span style="color: #006633;">analyze</span><span style="color: #009900;">&#40;</span>queryCtx.<span style="color: #006633;">request</span>.<span style="color: #006633;">stmt</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
              Preconditions.<span style="color: #006633;">checkState</span><span style="color: #009900;">&#40;</span>analysisCtx.<span style="color: #006633;">getAnalyzer</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getMissingTbls</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">isEmpty</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
              <span style="color: #000000; font-weight: bold;">return</span> analysisCtx.<span style="color: #006633;">getAnalysisResult</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span>AnalysisException e<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
              Set<span style="color: #339933;">&lt;</span>TableName<span style="color: #339933;">&gt;</span> missingTbls <span style="color: #339933;">=</span> analysisCtx.<span style="color: #006633;">getAnalyzer</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getMissingTbls</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
              <span style="color: #666666; font-style: italic;">// Only re-throw the AnalysisException if there were no missing tables.</span>
              <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>missingTbls.<span style="color: #006633;">isEmpty</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">throw</span> e<span style="color: #339933;">;</span>
    &nbsp;
              <span style="color: #666666; font-style: italic;">// Some tables/views were missing, request and wait for them to load.</span>
              <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span><span style="color: #339933;">!</span>requestTblLoadAndWait<span style="color: #009900;">&#40;</span>missingTbls, MISSING_TBL_LOAD_WAIT_TIMEOUT_MS<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                LOG.<span style="color: #006633;">info</span><span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span>.<span style="color: #006633;">format</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Missing tables were not received in %dms. Load &quot;</span> <span style="color: #339933;">+</span>
                    <span style="color: #0000ff;">&quot;request will be retried.&quot;</span>, MISSING_TBL_LOAD_WAIT_TIMEOUT_MS<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
              <span style="color: #009900;">&#125;</span>
            <span style="color: #009900;">&#125;</span>
          <span style="color: #009900;">&#125;</span>
        <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">finally</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #666666; font-style: italic;">// Authorize all accesses.</span>
          <span style="color: #666666; font-style: italic;">// AuthorizationExceptions must take precedence over any AnalysisException</span>
          <span style="color: #666666; font-style: italic;">// that has been thrown, so perform the authorization first.</span>
          analysisCtx.<span style="color: #006633;">getAnalyzer</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">authorize</span><span style="color: #009900;">&#40;</span>getAuthzChecker<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
      <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">  private AnalysisContext.AnalysisResult analyzeStmt(TQueryCtx queryCtx)
          throws AnalysisException, InternalException, AuthorizationException {
        AnalysisContext analysisCtx = new AnalysisContext(impaladCatalog_, queryCtx,
            authzConfig_);
        LOG.debug(&quot;analyze query &quot; + queryCtx.request.stmt);
    
        // Run analysis in a loop until it any of the following events occur:
        // 1) Analysis completes successfully.
        // 2) Analysis fails with an AnalysisException AND there are no missing tables.
        // 3) Analysis fails with an AuthorizationException.
        try {
          while (true) {
            try {
              analysisCtx.analyze(queryCtx.request.stmt);
              Preconditions.checkState(analysisCtx.getAnalyzer().getMissingTbls().isEmpty());
              return analysisCtx.getAnalysisResult();
            } catch (AnalysisException e) {
              Set&lt;TableName&gt; missingTbls = analysisCtx.getAnalyzer().getMissingTbls();
              // Only re-throw the AnalysisException if there were no missing tables.
              if (missingTbls.isEmpty()) throw e;
    
              // Some tables/views were missing, request and wait for them to load.
              if (!requestTblLoadAndWait(missingTbls, MISSING_TBL_LOAD_WAIT_TIMEOUT_MS)) {
                LOG.info(String.format(&quot;Missing tables were not received in %dms. Load &quot; +
                    &quot;request will be retried.&quot;, MISSING_TBL_LOAD_WAIT_TIMEOUT_MS));
              }
            }
          }
        } finally {
          // Authorize all accesses.
          // AuthorizationExceptions must take precedence over any AnalysisException
          // that has been thrown, so perform the authorization first.
          analysisCtx.getAnalyzer().authorize(getAuthzChecker());
        }
      }</p></div>
    ";i:2;s:10778:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">  <span style="color: #008000; font-style: italic; font-weight: bold;">/**
       * Requests the catalog server load the given set of tables and waits until
       * these tables show up in the local catalog, or the given timeout has been reached.
       * The timeout is specified in milliseconds, with a value &lt;= 0 indicating no timeout.
       * The exact steps taken are:
       * 1) Collect the tables that are missing (not yet loaded locally).
       * 2) Make an RPC to the CatalogServer to prioritize the loading of these tables.
       * 3) Wait until the local catalog contains all missing tables by (re)checking the
       *    catalog each time a new catalog update is received.
       *
       * Returns true if all missing tables were received before timing out and false if
       * the timeout was reached before all tables were received.
       */</span>
      <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000066; font-weight: bold;">boolean</span> requestTblLoadAndWait<span style="color: #009900;">&#40;</span>Set<span style="color: #339933;">&lt;</span>TableName<span style="color: #339933;">&gt;</span> requestedTbls, <span style="color: #000066; font-weight: bold;">long</span> timeoutMs<span style="color: #009900;">&#41;</span>
          <span style="color: #000000; font-weight: bold;">throws</span> InternalException <span style="color: #009900;">&#123;</span>
        Set<span style="color: #339933;">&lt;</span>TableName<span style="color: #339933;">&gt;</span> missingTbls <span style="color: #339933;">=</span> getMissingTbls<span style="color: #009900;">&#40;</span>requestedTbls<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #666666; font-style: italic;">// There are no missing tables, return and avoid making an RPC to the CatalogServer.</span>
        <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>missingTbls.<span style="color: #006633;">isEmpty</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">return</span> <span style="color: #000066; font-weight: bold;">true</span><span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #666666; font-style: italic;">// Call into the CatalogServer and request the required tables be loaded.</span>
        LOG.<span style="color: #006633;">info</span><span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span>.<span style="color: #006633;">format</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Requesting prioritized load of table(s): %s&quot;</span>,
            Joiner.<span style="color: #006633;">on</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;, &quot;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">join</span><span style="color: #009900;">&#40;</span>missingTbls<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        TStatus status <span style="color: #339933;">=</span> FeSupport.<span style="color: #006633;">PrioritizeLoad</span><span style="color: #009900;">&#40;</span>missingTbls<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>status.<span style="color: #006633;">getStatus_code</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">!=</span> TStatusCode.<span style="color: #006633;">OK</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #000000; font-weight: bold;">throw</span> <span style="color: #000000; font-weight: bold;">new</span> InternalException<span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Error requesting prioritized load: &quot;</span> <span style="color: #339933;">+</span>
              Joiner.<span style="color: #006633;">on</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;<span style="color: #000099; font-weight: bold;">\n</span>&quot;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">join</span><span style="color: #009900;">&#40;</span>status.<span style="color: #006633;">getError_msgs</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        <span style="color: #000066; font-weight: bold;">long</span> startTimeMs <span style="color: #339933;">=</span> <span style="color: #003399;">System</span>.<span style="color: #006633;">currentTimeMillis</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #666666; font-style: italic;">// Wait until all the required tables are loaded in the Impalad's catalog cache.</span>
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
      <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">  /**
       * Requests the catalog server load the given set of tables and waits until
       * these tables show up in the local catalog, or the given timeout has been reached.
       * The timeout is specified in milliseconds, with a value &lt;= 0 indicating no timeout.
       * The exact steps taken are:
       * 1) Collect the tables that are missing (not yet loaded locally).
       * 2) Make an RPC to the CatalogServer to prioritize the loading of these tables.
       * 3) Wait until the local catalog contains all missing tables by (re)checking the
       *    catalog each time a new catalog update is received.
       *
       * Returns true if all missing tables were received before timing out and false if
       * the timeout was reached before all tables were received.
       */
      private boolean requestTblLoadAndWait(Set&lt;TableName&gt; requestedTbls, long timeoutMs)
          throws InternalException {
        Set&lt;TableName&gt; missingTbls = getMissingTbls(requestedTbls);
        // There are no missing tables, return and avoid making an RPC to the CatalogServer.
        if (missingTbls.isEmpty()) return true;
    
        // Call into the CatalogServer and request the required tables be loaded.
        LOG.info(String.format(&quot;Requesting prioritized load of table(s): %s&quot;,
            Joiner.on(&quot;, &quot;).join(missingTbls)));
        TStatus status = FeSupport.PrioritizeLoad(missingTbls);
        if (status.getStatus_code() != TStatusCode.OK) {
          throw new InternalException(&quot;Error requesting prioritized load: &quot; +
              Joiner.on(&quot;\n&quot;).join(status.getError_msgs()));
        }
    
        long startTimeMs = System.currentTimeMillis();
        // Wait until all the required tables are loaded in the Impalad's catalog cache.
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
    ";}
categories:
  - hadoop
tags:
  - impala

---
本文只是分析和代码的关联，并没有解决慢的问题。
有些语句在impala查询很慢，尝试把日志和代码关联起来，便于之后的分析。由于impala涉及到多个对象，有些代码搞不清楚是如何调用的。
当前发现在获取元数据的过程很慢。
代码中有fe和be两个目录,be是c++写的，fe是java写的。
c++通过jni调用java代码（或许还有rpc调用）
在be\src\service\impala-hs2-server.cc里是我们使用的hiveserver2协议的服务端
## 开始

先把impalad的debug日志记录下来，修改/etc/default/impala里，增加一行export GLOG_v=2
通过impala-shell查询 select distinct(disp\_id) from default\_impala.kpi\_disp\_user\_info\_stat_tb where pt=&#8217;2014-04-08&#8242;
等查询完后的时间分析为：
<pre>Query Timeline: 2m34s
       - Start execution: 77.818us (77.818us)
       - Planning finished: 2m33s (2m33s)
       - Ready to start remote fragments: 2m33s (4.473ms)
       - Remote fragments started: 2m34s (580.800ms)
       - Rows available: 2m34s (353.883ms)
       - First row fetched: 2m34s (51.765ms)
       - Unregister query: 2m34s (13.51ms)</pre>
其中大部分时间在Planning里面
在日志可以看到这两条
I1228 17:22:53.467937 11982 rpc-trace.cc:133] RPC call: BeeswaxService.query(from ::ffff:IP:39274)  
I1228 17:22:53.467978 11982 impala-beeswax-server.cc:170] query(): query=select distinct(disp\_id) from default\_impala.kpi\_disp\_user\_info\_stat_tb where pt=&#8217;2014-04-08&#8242;
已经开始查询
I1228 17:22:53.471019 11982 Frontend.java:760] analyze query select distinct(disp\_id) from default\_impala.kpi\_disp\_user\_info\_stat_tb where pt=&#8217;2014-04-08&#8242;  
I1228 17:22:53.472192 11982 Frontend.java:709] Requesting prioritized load of table(s): default\_impala.kpi\_disp\_user\_info\_stat\_tb  
I1228 17:24:54.335124 11982 Frontend.java:779] Missing tables were not received in 120000ms. Load request will be retried.  
I1228 17:24:54.335906 11982 Frontend.java:709] Requesting prioritized load of table(s): default\_impala.kpi\_disp\_user\_info\_stat\_tb  
I1228 17:25:27.136531 11982 Frontend.java:833] create plan
impala-beeswax-server.cc中通过jni的方式调用Frontend.java的代码，这里日志中有一次超时了（120秒），重试了一次。第一次花了120秒，第二次重试后，在17:25:27后获取成功，第二次花了30秒。
<pre lang="java" escaped="true">private AnalysisContext.AnalysisResult analyzeStmt(TQueryCtx queryCtx)
      throws AnalysisException, InternalException, AuthorizationException {
    AnalysisContext analysisCtx = new AnalysisContext(impaladCatalog_, queryCtx,
        authzConfig_);
    LOG.debug("analyze query " + queryCtx.request.stmt);

    // Run analysis in a loop until it any of the following events occur:
    // 1) Analysis completes successfully.
    // 2) Analysis fails with an AnalysisException AND there are no missing tables.
    // 3) Analysis fails with an AuthorizationException.
    try {
      while (true) {
        try {
          analysisCtx.analyze(queryCtx.request.stmt);
          Preconditions.checkState(analysisCtx.getAnalyzer().getMissingTbls().isEmpty());
          return analysisCtx.getAnalysisResult();
        } catch (AnalysisException e) {
          Set&lt;TableName&gt; missingTbls = analysisCtx.getAnalyzer().getMissingTbls();
          // Only re-throw the AnalysisException if there were no missing tables.
          if (missingTbls.isEmpty()) throw e;

          // Some tables/views were missing, request and wait for them to load.
          if (!requestTblLoadAndWait(missingTbls, MISSING_TBL_LOAD_WAIT_TIMEOUT_MS)) {
            LOG.info(String.format("Missing tables were not received in %dms. Load " +
                "request will be retried.", MISSING_TBL_LOAD_WAIT_TIMEOUT_MS));
          }
        }
      }
    } finally {
      // Authorize all accesses.
      // AuthorizationExceptions must take precedence over any AnalysisException
      // that has been thrown, so perform the authorization first.
      analysisCtx.getAnalyzer().authorize(getAuthzChecker());
    }
  }</pre>
进去看requestTblLoadAndWait这个方法
<pre lang="java" escaped="true">/**
   * Requests the catalog server load the given set of tables and waits until
   * these tables show up in the local catalog, or the given timeout has been reached.
   * The timeout is specified in milliseconds, with a value &lt;= 0 indicating no timeout.
   * The exact steps taken are:
   * 1) Collect the tables that are missing (not yet loaded locally).
   * 2) Make an RPC to the CatalogServer to prioritize the loading of these tables.
   * 3) Wait until the local catalog contains all missing tables by (re)checking the
   *    catalog each time a new catalog update is received.
   *
   * Returns true if all missing tables were received before timing out and false if
   * the timeout was reached before all tables were received.
   */
  private boolean requestTblLoadAndWait(Set&lt;TableName&gt; requestedTbls, long timeoutMs)
      throws InternalException {
    Set&lt;TableName&gt; missingTbls = getMissingTbls(requestedTbls);
    // There are no missing tables, return and avoid making an RPC to the CatalogServer.
    if (missingTbls.isEmpty()) return true;

    // Call into the CatalogServer and request the required tables be loaded.
    LOG.info(String.format("Requesting prioritized load of table(s): %s",
        Joiner.on(", ").join(missingTbls)));
    TStatus status = FeSupport.PrioritizeLoad(missingTbls);
    if (status.getStatus_code() != TStatusCode.OK) {
      throw new InternalException("Error requesting prioritized load: " +
          Joiner.on("\n").join(status.getError_msgs()));
    }

    long startTimeMs = System.currentTimeMillis();
    // Wait until all the required tables are loaded in the Impalad's catalog cache.
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
这里没看懂怎么调用的，调用的是FeSupport.PrioritizeLoad，是放到一个SET里面，并且移到第一位。猜测是impalad自己有个catalog的缓存，如果在缓存找不到(missingTbls)，会通过rpc调用中心的catalogd服务。
看中心catalogd的日志，可以看到被调用了两次。时间上和impalad的日志一致。（因为在线上测试，catalogd没有打开更详细日志）
I1228 17:22:53.448292 9209 TableLoader.java:60] Loading metadata for: default\_impala.kpi\_disp\_user\_info\_stat\_tb  
I1228 17:22:53.448468 9209 HiveMetaStoreClient.java:238] Trying to connect to metastore with URI thrift://vdc22:9083  
I1228 17:22:53.449069 9209 HiveMetaStoreClient.java:326] Connected to metastore.  
I1228 17:23:07.808981 15118 HiveMetaStoreClient.java:238] Trying to connect to metastore with URI thrift://vdc22:9083  
I1228 17:23:07.809939 15118 HiveMetaStoreClient.java:326] Connected to metastore.  
I1228 17:23:20.419278 26716 HiveMetaStoreClient.java:238] Trying to connect to metastore with URI thrift://vdc22:9083  
I1228 17:23:20.419970 26716 HiveMetaStoreClient.java:326] Connected to metastore.  
I1228 17:24:54.308159  3044 TableLoader.java:60] Loading metadata for: default\_impala.kpi\_disp\_user\_info\_stat\_tb
这里日志的代码在这里com.cloudera.impala.catalog.TableLoader
后面的步骤花费的时间不多，不继续分析了。