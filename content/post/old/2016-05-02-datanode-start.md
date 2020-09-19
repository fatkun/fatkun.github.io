---
title: DataNode启动流程源码分析
author: fatkun
type: post
date: 2016-05-02T09:28:42+00:00
url: /2016/05/datanode-start.html
duoshuo_thread_id:
  - 6300421658679182082
wp-syntax-cache-content:
  - |
    a:13:{i:1;s:1942:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">  <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000066; font-weight: bold;">void</span> main<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> args<span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
        <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>DFSUtil.<span style="color: #006633;">parseHelpArgument</span><span style="color: #009900;">&#40;</span>args, DataNode.<span style="color: #006633;">USAGE</span>, <span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>, <span style="color: #000066; font-weight: bold;">true</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #003399;">System</span>.<span style="color: #006633;">exit</span><span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">0</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        secureMain<span style="color: #009900;">&#40;</span>args, <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
      <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">  public static void main(String args[]) {
        if (DFSUtil.parseHelpArgument(args, DataNode.USAGE, System.out, true)) {
          System.exit(0);
        }
    
        secureMain(args, null);
      }</p></div>
    ";i:2;s:2251:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">  <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">static</span> DataNode createDataNode<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> args<span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span>, Configuration conf,
          SecureResources resources<span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">throws</span> <span style="color: #003399;">IOException</span> <span style="color: #009900;">&#123;</span>
        <span style="color: #666666; font-style: italic;">// 实例化datanode</span>
        DataNode dn <span style="color: #339933;">=</span> instantiateDataNode<span style="color: #009900;">&#40;</span>args, conf, resources<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>dn <span style="color: #339933;">!=</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #666666; font-style: italic;">// 启动BPOfferService、dataXceiverServer、ipcServer等</span>
          dn.<span style="color: #006633;">runDatanodeDaemon</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
        <span style="color: #000000; font-weight: bold;">return</span> dn<span style="color: #339933;">;</span>
      <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">  public static DataNode createDataNode(String args[], Configuration conf,
          SecureResources resources) throws IOException {
        // 实例化datanode
        DataNode dn = instantiateDataNode(args, conf, resources);
        if (dn != null) {
          // 启动BPOfferService、dataXceiverServer、ipcServer等
          dn.runDatanodeDaemon();
        }
        return dn;
      }</p></div>
    ";i:3;s:5100:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">  <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">static</span> DataNode instantiateDataNode<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> args <span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span>, Configuration conf,
          SecureResources resources<span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">throws</span> <span style="color: #003399;">IOException</span> <span style="color: #009900;">&#123;</span>
        <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>conf <span style="color: #339933;">==</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span>
          conf <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> HdfsConfiguration<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>args <span style="color: #339933;">!=</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #666666; font-style: italic;">// parse generic hadoop options</span>
          GenericOptionsParser hParser <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> GenericOptionsParser<span style="color: #009900;">&#40;</span>conf, args<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          args <span style="color: #339933;">=</span> hParser.<span style="color: #006633;">getRemainingArgs</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span><span style="color: #339933;">!</span>parseArguments<span style="color: #009900;">&#40;</span>args, conf<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          printUsage<span style="color: #009900;">&#40;</span><span style="color: #003399;">System</span>.<span style="color: #006633;">err</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #000000; font-weight: bold;">return</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
        <span style="color: #666666; font-style: italic;">// 获取实际的存储路径（根据配置dfs.datanode.data.dir）</span>
        Collection<span style="color: #339933;">&lt;</span>StorageLocation<span style="color: #339933;">&gt;</span> dataLocations <span style="color: #339933;">=</span> getStorageLocations<span style="color: #009900;">&#40;</span>conf<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        UserGroupInformation.<span style="color: #006633;">setConfiguration</span><span style="color: #009900;">&#40;</span>conf<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        SecurityUtil.<span style="color: #006633;">login</span><span style="color: #009900;">&#40;</span>conf, DFS_DATANODE_KEYTAB_FILE_KEY,
            DFS_DATANODE_KERBEROS_PRINCIPAL_KEY<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #000000; font-weight: bold;">return</span> makeInstance<span style="color: #009900;">&#40;</span>dataLocations, conf, resources<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
      <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">  public static DataNode instantiateDataNode(String args [], Configuration conf,
          SecureResources resources) throws IOException {
        if (conf == null)
          conf = new HdfsConfiguration();
        
        if (args != null) {
          // parse generic hadoop options
          GenericOptionsParser hParser = new GenericOptionsParser(conf, args);
          args = hParser.getRemainingArgs();
        }
        
        if (!parseArguments(args, conf)) {
          printUsage(System.err);
          return null;
        }
        // 获取实际的存储路径（根据配置dfs.datanode.data.dir）
        Collection&lt;StorageLocation&gt; dataLocations = getStorageLocations(conf);
        UserGroupInformation.setConfiguration(conf);
        SecurityUtil.login(conf, DFS_DATANODE_KEYTAB_FILE_KEY,
            DFS_DATANODE_KERBEROS_PRINCIPAL_KEY);
        return makeInstance(dataLocations, conf, resources);
      }</p></div>
    ";i:4;s:4297:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">  <span style="color: #000000; font-weight: bold;">static</span> DataNode makeInstance<span style="color: #009900;">&#40;</span>Collection<span style="color: #339933;">&lt;</span>StorageLocation<span style="color: #339933;">&gt;</span> dataDirs,
          Configuration conf, SecureResources resources<span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">throws</span> <span style="color: #003399;">IOException</span> <span style="color: #009900;">&#123;</span>
        LocalFileSystem localFS <span style="color: #339933;">=</span> FileSystem.<span style="color: #006633;">getLocal</span><span style="color: #009900;">&#40;</span>conf<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        FsPermission permission <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> FsPermission<span style="color: #009900;">&#40;</span>
            conf.<span style="color: #006633;">get</span><span style="color: #009900;">&#40;</span>DFS_DATANODE_DATA_DIR_PERMISSION_KEY,
                     DFS_DATANODE_DATA_DIR_PERMISSION_DEFAULT<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #666666; font-style: italic;">// DataNode磁盘检查类，检查目录权限以及是否能够创建目录</span>
        DataNodeDiskChecker dataNodeDiskChecker <span style="color: #339933;">=</span>
            <span style="color: #000000; font-weight: bold;">new</span> DataNodeDiskChecker<span style="color: #009900;">&#40;</span>permission<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #666666; font-style: italic;">// 找出能够正常读写的路径</span>
        List<span style="color: #339933;">&lt;</span>StorageLocation<span style="color: #339933;">&gt;</span> locations <span style="color: #339933;">=</span>
            checkStorageLocations<span style="color: #009900;">&#40;</span>dataDirs, localFS, dataNodeDiskChecker<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        DefaultMetricsSystem.<span style="color: #006633;">initialize</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;DataNode&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">assert</span> locations.<span style="color: #006633;">size</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">&gt;</span> <span style="color: #cc66cc;">0</span> <span style="color: #339933;">:</span> <span style="color: #0000ff;">&quot;number of data directories should be &gt; 0&quot;</span><span style="color: #339933;">;</span>
        <span style="color: #000000; font-weight: bold;">return</span> <span style="color: #000000; font-weight: bold;">new</span> DataNode<span style="color: #009900;">&#40;</span>conf, locations, resources<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
      <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">  static DataNode makeInstance(Collection&lt;StorageLocation&gt; dataDirs,
          Configuration conf, SecureResources resources) throws IOException {
        LocalFileSystem localFS = FileSystem.getLocal(conf);
        FsPermission permission = new FsPermission(
            conf.get(DFS_DATANODE_DATA_DIR_PERMISSION_KEY,
                     DFS_DATANODE_DATA_DIR_PERMISSION_DEFAULT));
        // DataNode磁盘检查类，检查目录权限以及是否能够创建目录
        DataNodeDiskChecker dataNodeDiskChecker =
            new DataNodeDiskChecker(permission);
        // 找出能够正常读写的路径
        List&lt;StorageLocation&gt; locations =
            checkStorageLocations(dataDirs, localFS, dataNodeDiskChecker);
        DefaultMetricsSystem.initialize(&quot;DataNode&quot;);
    
        assert locations.size() &gt; 0 : &quot;number of data directories should be &gt; 0&quot;;
        return new DataNode(conf, locations, resources);
      }</p></div>
    ";i:5;s:16351:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">  <span style="color: #000066; font-weight: bold;">void</span> startDataNode<span style="color: #009900;">&#40;</span>Configuration conf, 
                         List<span style="color: #339933;">&lt;</span>StorageLocation<span style="color: #339933;">&gt;</span> dataDirs,
                         SecureResources resources
                         <span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">throws</span> <span style="color: #003399;">IOException</span> <span style="color: #009900;">&#123;</span>
    &nbsp;
        <span style="color: #666666; font-style: italic;">// settings global for all BPs in the Data Node</span>
        <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">secureResources</span> <span style="color: #339933;">=</span> resources<span style="color: #339933;">;</span>
        <span style="color: #000000; font-weight: bold;">synchronized</span> <span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">this</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">dataDirs</span> <span style="color: #339933;">=</span> dataDirs<span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
        <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">conf</span> <span style="color: #339933;">=</span> conf<span style="color: #339933;">;</span>
        <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">dnConf</span> <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> DNConf<span style="color: #009900;">&#40;</span>conf<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        checkSecureConfig<span style="color: #009900;">&#40;</span>dnConf, conf, resources<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">spanReceiverHost</span> <span style="color: #339933;">=</span> SpanReceiverHost.<span style="color: #006633;">getInstance</span><span style="color: #009900;">&#40;</span>conf<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>dnConf.<span style="color: #006633;">maxLockedMemory</span> <span style="color: #339933;">&gt;</span> <span style="color: #cc66cc;">0</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span><span style="color: #339933;">!</span>NativeIO.<span style="color: #006633;">POSIX</span>.<span style="color: #006633;">getCacheManipulator</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">verifyCanMlock</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">throw</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">RuntimeException</span><span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span>.<span style="color: #006633;">format</span><span style="color: #009900;">&#40;</span>
                <span style="color: #0000ff;">&quot;Cannot start datanode because the configured max locked memory&quot;</span> <span style="color: #339933;">+</span>
                <span style="color: #0000ff;">&quot; size (%s) is greater than zero and native code is not available.&quot;</span>,
                DFS_DATANODE_MAX_LOCKED_MEMORY_KEY<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #009900;">&#125;</span>
          <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>Path.<span style="color: #006633;">WINDOWS</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            NativeIO.<span style="color: #006633;">Windows</span>.<span style="color: #006633;">extendWorkingSetSize</span><span style="color: #009900;">&#40;</span>dnConf.<span style="color: #006633;">maxLockedMemory</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">else</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000066; font-weight: bold;">long</span> ulimit <span style="color: #339933;">=</span> NativeIO.<span style="color: #006633;">POSIX</span>.<span style="color: #006633;">getCacheManipulator</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getMemlockLimit</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>dnConf.<span style="color: #006633;">maxLockedMemory</span> <span style="color: #339933;">&gt;</span> ulimit<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
              <span style="color: #000000; font-weight: bold;">throw</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">RuntimeException</span><span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span>.<span style="color: #006633;">format</span><span style="color: #009900;">&#40;</span>
                <span style="color: #0000ff;">&quot;Cannot start datanode because the configured max locked memory&quot;</span> <span style="color: #339933;">+</span>
                <span style="color: #0000ff;">&quot; size (%s) of %d bytes is more than the datanode's available&quot;</span> <span style="color: #339933;">+</span>
                <span style="color: #0000ff;">&quot; RLIMIT_MEMLOCK ulimit of %d bytes.&quot;</span>,
                DFS_DATANODE_MAX_LOCKED_MEMORY_KEY,
                dnConf.<span style="color: #006633;">maxLockedMemory</span>,
                ulimit<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
          <span style="color: #009900;">&#125;</span>
        <span style="color: #009900;">&#125;</span>
        LOG.<span style="color: #006633;">info</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Starting DataNode with maxLockedMemory = &quot;</span> <span style="color: #339933;">+</span>
            dnConf.<span style="color: #006633;">maxLockedMemory</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
        storage <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> DataStorage<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #666666; font-style: italic;">// global DN settings</span>
        registerMXBean<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #666666; font-style: italic;">// 初始化xceiverServer一些对象</span>
        initDataXceiver<span style="color: #009900;">&#40;</span>conf<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #666666; font-style: italic;">// 启动http web hdfs</span>
        startInfoServer<span style="color: #009900;">&#40;</span>conf<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        pauseMonitor <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> JvmPauseMonitor<span style="color: #009900;">&#40;</span>conf<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        pauseMonitor.<span style="color: #006633;">start</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #666666; font-style: italic;">// BlockPoolTokenSecretManager is required to create ipc server.</span>
        <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">blockPoolTokenSecretManager</span> <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> BlockPoolTokenSecretManager<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #666666; font-style: italic;">// Login is done by now. Set the DN user name.</span>
        dnUserName <span style="color: #339933;">=</span> UserGroupInformation.<span style="color: #006633;">getCurrentUser</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getShortUserName</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        LOG.<span style="color: #006633;">info</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;dnUserName = &quot;</span> <span style="color: #339933;">+</span> dnUserName<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        LOG.<span style="color: #006633;">info</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;supergroup = &quot;</span> <span style="color: #339933;">+</span> supergroup<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #666666; font-style: italic;">// 初始化ipc服务</span>
        initIpcServer<span style="color: #009900;">&#40;</span>conf<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
        metrics <span style="color: #339933;">=</span> DataNodeMetrics.<span style="color: #006633;">create</span><span style="color: #009900;">&#40;</span>conf, getDisplayName<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        metrics.<span style="color: #006633;">getJvmMetrics</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">setPauseMonitor</span><span style="color: #009900;">&#40;</span>pauseMonitor<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #666666; font-style: italic;">// 重要，构造BlockPoolManager</span>
        blockPoolManager <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> BlockPoolManager<span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">this</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        blockPoolManager.<span style="color: #006633;">refreshNamenodes</span><span style="color: #009900;">&#40;</span>conf<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #666666; font-style: italic;">// Create the ReadaheadPool from the DataNode context so we can</span>
        <span style="color: #666666; font-style: italic;">// exit without having to explicitly shutdown its thread pool.</span>
        readaheadPool <span style="color: #339933;">=</span> ReadaheadPool.<span style="color: #006633;">getInstance</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        saslClient <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> SaslDataTransferClient<span style="color: #009900;">&#40;</span>dnConf.<span style="color: #006633;">conf</span>, 
            dnConf.<span style="color: #006633;">saslPropsResolver</span>, dnConf.<span style="color: #006633;">trustedChannelResolver</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        saslServer <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> SaslDataTransferServer<span style="color: #009900;">&#40;</span>dnConf, blockPoolTokenSecretManager<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
      <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">  void startDataNode(Configuration conf, 
                         List&lt;StorageLocation&gt; dataDirs,
                         SecureResources resources
                         ) throws IOException {
    
        // settings global for all BPs in the Data Node
        this.secureResources = resources;
        synchronized (this) {
          this.dataDirs = dataDirs;
        }
        this.conf = conf;
        this.dnConf = new DNConf(conf);
        checkSecureConfig(dnConf, conf, resources);
    
        this.spanReceiverHost = SpanReceiverHost.getInstance(conf);
    
        if (dnConf.maxLockedMemory &gt; 0) {
          if (!NativeIO.POSIX.getCacheManipulator().verifyCanMlock()) {
            throw new RuntimeException(String.format(
                &quot;Cannot start datanode because the configured max locked memory&quot; +
                &quot; size (%s) is greater than zero and native code is not available.&quot;,
                DFS_DATANODE_MAX_LOCKED_MEMORY_KEY));
          }
          if (Path.WINDOWS) {
            NativeIO.Windows.extendWorkingSetSize(dnConf.maxLockedMemory);
          } else {
            long ulimit = NativeIO.POSIX.getCacheManipulator().getMemlockLimit();
            if (dnConf.maxLockedMemory &gt; ulimit) {
              throw new RuntimeException(String.format(
                &quot;Cannot start datanode because the configured max locked memory&quot; +
                &quot; size (%s) of %d bytes is more than the datanode's available&quot; +
                &quot; RLIMIT_MEMLOCK ulimit of %d bytes.&quot;,
                DFS_DATANODE_MAX_LOCKED_MEMORY_KEY,
                dnConf.maxLockedMemory,
                ulimit));
            }
          }
        }
        LOG.info(&quot;Starting DataNode with maxLockedMemory = &quot; +
            dnConf.maxLockedMemory);
    
        storage = new DataStorage();
        
        // global DN settings
        registerMXBean();
        // 初始化xceiverServer一些对象
        initDataXceiver(conf);
        // 启动http web hdfs
        startInfoServer(conf);
        pauseMonitor = new JvmPauseMonitor(conf);
        pauseMonitor.start();
      
        // BlockPoolTokenSecretManager is required to create ipc server.
        this.blockPoolTokenSecretManager = new BlockPoolTokenSecretManager();
    
        // Login is done by now. Set the DN user name.
        dnUserName = UserGroupInformation.getCurrentUser().getShortUserName();
        LOG.info(&quot;dnUserName = &quot; + dnUserName);
        LOG.info(&quot;supergroup = &quot; + supergroup);
        // 初始化ipc服务
        initIpcServer(conf);
    
        metrics = DataNodeMetrics.create(conf, getDisplayName());
        metrics.getJvmMetrics().setPauseMonitor(pauseMonitor);
        
        // 重要，构造BlockPoolManager
        blockPoolManager = new BlockPoolManager(this);
        blockPoolManager.refreshNamenodes(conf);
    
        // Create the ReadaheadPool from the DataNode context so we can
        // exit without having to explicitly shutdown its thread pool.
        readaheadPool = ReadaheadPool.getInstance();
        saslClient = new SaslDataTransferClient(dnConf.conf, 
            dnConf.saslPropsResolver, dnConf.trustedChannelResolver);
        saslServer = new SaslDataTransferServer(dnConf, blockPoolTokenSecretManager);
      }</p></div>
    ";i:6;s:13556:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">  <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000066; font-weight: bold;">void</span> doRefreshNamenodes<span style="color: #009900;">&#40;</span>
          Map<span style="color: #339933;">&lt;</span><span style="color: #003399;">String</span>, Map<span style="color: #339933;">&lt;</span><span style="color: #003399;">String</span>, InetSocketAddress<span style="color: #339933;">&gt;&gt;</span> addrMap<span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">throws</span> <span style="color: #003399;">IOException</span> <span style="color: #009900;">&#123;</span>
        <span style="color: #000000; font-weight: bold;">assert</span> <span style="color: #003399;">Thread</span>.<span style="color: #006633;">holdsLock</span><span style="color: #009900;">&#40;</span>refreshNamenodesLock<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
        Set<span style="color: #339933;">&lt;</span>String<span style="color: #339933;">&gt;</span> toRefresh <span style="color: #339933;">=</span> Sets.<span style="color: #006633;">newLinkedHashSet</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        Set<span style="color: #339933;">&lt;</span>String<span style="color: #339933;">&gt;</span> toAdd <span style="color: #339933;">=</span> Sets.<span style="color: #006633;">newLinkedHashSet</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        Set<span style="color: #339933;">&lt;</span>String<span style="color: #339933;">&gt;</span> toRemove<span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">synchronized</span> <span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">this</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #666666; font-style: italic;">// Step 1. For each of the new nameservices, figure out whether</span>
          <span style="color: #666666; font-style: italic;">// it's an update of the set of NNs for an existing NS,</span>
          <span style="color: #666666; font-style: italic;">// or an entirely new nameservice.</span>
          <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> nameserviceId <span style="color: #339933;">:</span> addrMap.<span style="color: #006633;">keySet</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>bpByNameserviceId.<span style="color: #006633;">containsKey</span><span style="color: #009900;">&#40;</span>nameserviceId<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
              toRefresh.<span style="color: #006633;">add</span><span style="color: #009900;">&#40;</span>nameserviceId<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">else</span> <span style="color: #009900;">&#123;</span>
              toAdd.<span style="color: #006633;">add</span><span style="color: #009900;">&#40;</span>nameserviceId<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
          <span style="color: #009900;">&#125;</span>
    &nbsp;
          <span style="color: #666666; font-style: italic;">// Step 2. Any nameservices we currently have but are no longer present</span>
          <span style="color: #666666; font-style: italic;">// need to be removed.</span>
          toRemove <span style="color: #339933;">=</span> Sets.<span style="color: #006633;">newHashSet</span><span style="color: #009900;">&#40;</span>Sets.<span style="color: #006633;">difference</span><span style="color: #009900;">&#40;</span>
              bpByNameserviceId.<span style="color: #006633;">keySet</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, addrMap.<span style="color: #006633;">keySet</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
          <span style="color: #000000; font-weight: bold;">assert</span> toRefresh.<span style="color: #006633;">size</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">+</span> toAdd.<span style="color: #006633;">size</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">==</span>
            addrMap.<span style="color: #006633;">size</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">:</span>
              <span style="color: #0000ff;">&quot;toAdd: &quot;</span> <span style="color: #339933;">+</span> Joiner.<span style="color: #006633;">on</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;,&quot;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">useForNull</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;&lt;default&gt;&quot;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">join</span><span style="color: #009900;">&#40;</span>toAdd<span style="color: #009900;">&#41;</span> <span style="color: #339933;">+</span>
              <span style="color: #0000ff;">&quot;  toRemove: &quot;</span> <span style="color: #339933;">+</span> Joiner.<span style="color: #006633;">on</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;,&quot;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">useForNull</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;&lt;default&gt;&quot;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">join</span><span style="color: #009900;">&#40;</span>toRemove<span style="color: #009900;">&#41;</span> <span style="color: #339933;">+</span>
              <span style="color: #0000ff;">&quot;  toRefresh: &quot;</span> <span style="color: #339933;">+</span> Joiner.<span style="color: #006633;">on</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;,&quot;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">useForNull</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;&lt;default&gt;&quot;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">join</span><span style="color: #009900;">&#40;</span>toRefresh<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
    &nbsp;
           <span style="color: #666666; font-style: italic;">// 由于是重启，所以都是在toAdd里面</span>
          <span style="color: #666666; font-style: italic;">// Step 3. Start new nameservices</span>
          <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span><span style="color: #339933;">!</span>toAdd.<span style="color: #006633;">isEmpty</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            LOG.<span style="color: #006633;">info</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Starting BPOfferServices for nameservices: &quot;</span> <span style="color: #339933;">+</span>
                Joiner.<span style="color: #006633;">on</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;,&quot;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">useForNull</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;&lt;default&gt;&quot;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">join</span><span style="color: #009900;">&#40;</span>toAdd<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #666666; font-style: italic;">// 这里遍历的是nameServices，如果用了hdfs federation就会有多个</span>
            <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> nsToAdd <span style="color: #339933;">:</span> toAdd<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
              ArrayList<span style="color: #339933;">&lt;</span>InetSocketAddress<span style="color: #339933;">&gt;</span> addrs <span style="color: #339933;">=</span>
                Lists.<span style="color: #006633;">newArrayList</span><span style="color: #009900;">&#40;</span>addrMap.<span style="color: #006633;">get</span><span style="color: #009900;">&#40;</span>nsToAdd<span style="color: #009900;">&#41;</span>.<span style="color: #006633;">values</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
              <span style="color: #666666; font-style: italic;">// 创建BPOfferService</span>
              BPOfferService bpos <span style="color: #339933;">=</span> createBPOS<span style="color: #009900;">&#40;</span>addrs<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
              <span style="color: #666666; font-style: italic;">// 加入bpByNameserviceId里面，下次再执行这个方法的话，就是加入toRefresh里面了</span>
              bpByNameserviceId.<span style="color: #006633;">put</span><span style="color: #009900;">&#40;</span>nsToAdd, bpos<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
              offerServices.<span style="color: #006633;">add</span><span style="color: #009900;">&#40;</span>bpos<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
          <span style="color: #009900;">&#125;</span>
          <span style="color: #666666; font-style: italic;">// 启动所有offerServices的BPOfferService</span>
          startAll<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">  private void doRefreshNamenodes(
          Map&lt;String, Map&lt;String, InetSocketAddress&gt;&gt; addrMap) throws IOException {
        assert Thread.holdsLock(refreshNamenodesLock);
    
        Set&lt;String&gt; toRefresh = Sets.newLinkedHashSet();
        Set&lt;String&gt; toAdd = Sets.newLinkedHashSet();
        Set&lt;String&gt; toRemove;
        
        synchronized (this) {
          // Step 1. For each of the new nameservices, figure out whether
          // it's an update of the set of NNs for an existing NS,
          // or an entirely new nameservice.
          for (String nameserviceId : addrMap.keySet()) {
            if (bpByNameserviceId.containsKey(nameserviceId)) {
              toRefresh.add(nameserviceId);
            } else {
              toAdd.add(nameserviceId);
            }
          }
          
          // Step 2. Any nameservices we currently have but are no longer present
          // need to be removed.
          toRemove = Sets.newHashSet(Sets.difference(
              bpByNameserviceId.keySet(), addrMap.keySet()));
          
          assert toRefresh.size() + toAdd.size() ==
            addrMap.size() :
              &quot;toAdd: &quot; + Joiner.on(&quot;,&quot;).useForNull(&quot;&lt;default&gt;&quot;).join(toAdd) +
              &quot;  toRemove: &quot; + Joiner.on(&quot;,&quot;).useForNull(&quot;&lt;default&gt;&quot;).join(toRemove) +
              &quot;  toRefresh: &quot; + Joiner.on(&quot;,&quot;).useForNull(&quot;&lt;default&gt;&quot;).join(toRefresh);
    
          
           // 由于是重启，所以都是在toAdd里面
          // Step 3. Start new nameservices
          if (!toAdd.isEmpty()) {
            LOG.info(&quot;Starting BPOfferServices for nameservices: &quot; +
                Joiner.on(&quot;,&quot;).useForNull(&quot;&lt;default&gt;&quot;).join(toAdd));
            // 这里遍历的是nameServices，如果用了hdfs federation就会有多个
            for (String nsToAdd : toAdd) {
              ArrayList&lt;InetSocketAddress&gt; addrs =
                Lists.newArrayList(addrMap.get(nsToAdd).values());
              // 创建BPOfferService
              BPOfferService bpos = createBPOS(addrs);
              // 加入bpByNameserviceId里面，下次再执行这个方法的话，就是加入toRefresh里面了
              bpByNameserviceId.put(nsToAdd, bpos);
              offerServices.add(bpos);
            }
          }
          // 启动所有offerServices的BPOfferService
          startAll();
        }</p></div>
    ";i:7;s:3299:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">  <span style="color: #000000; font-weight: bold;">protected</span> BPOfferService createBPOS<span style="color: #009900;">&#40;</span>List<span style="color: #339933;">&lt;</span>InetSocketAddress<span style="color: #339933;">&gt;</span> nnAddrs<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
        <span style="color: #000000; font-weight: bold;">return</span> <span style="color: #000000; font-weight: bold;">new</span> BPOfferService<span style="color: #009900;">&#40;</span>nnAddrs, dn<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
      <span style="color: #009900;">&#125;</span>
    &nbsp;
      BPOfferService<span style="color: #009900;">&#40;</span>List<span style="color: #339933;">&lt;</span>InetSocketAddress<span style="color: #339933;">&gt;</span> nnAddrs, DataNode dn<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
        Preconditions.<span style="color: #006633;">checkArgument</span><span style="color: #009900;">&#40;</span><span style="color: #339933;">!</span>nnAddrs.<span style="color: #006633;">isEmpty</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>,
            <span style="color: #0000ff;">&quot;Must pass at least one NN.&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">dn</span> <span style="color: #339933;">=</span> dn<span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #666666; font-style: italic;">// 如果有standby和active两个namenode，就会创建两个BPServiceActor</span>
        <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span>InetSocketAddress addr <span style="color: #339933;">:</span> nnAddrs<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">bpServices</span>.<span style="color: #006633;">add</span><span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">new</span> BPServiceActor<span style="color: #009900;">&#40;</span>addr, <span style="color: #000000; font-weight: bold;">this</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
      <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">  protected BPOfferService createBPOS(List&lt;InetSocketAddress&gt; nnAddrs) {
        return new BPOfferService(nnAddrs, dn);
      }
    
      BPOfferService(List&lt;InetSocketAddress&gt; nnAddrs, DataNode dn) {
        Preconditions.checkArgument(!nnAddrs.isEmpty(),
            &quot;Must pass at least one NN.&quot;);
        this.dn = dn;
    
        // 如果有standby和active两个namenode，就会创建两个BPServiceActor
        for (InetSocketAddress addr : nnAddrs) {
          this.bpServices.add(new BPServiceActor(addr, this));
        }
      }</p></div>
    ";i:8;s:10073:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">  <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> run<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
        LOG.<span style="color: #006633;">info</span><span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">this</span> <span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot; starting to offer service&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #000000; font-weight: bold;">while</span> <span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">true</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #666666; font-style: italic;">// init stuff</span>
            <span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#123;</span>
              <span style="color: #666666; font-style: italic;">// 向namenode注册以及初始化blockPool</span>
              <span style="color: #666666; font-style: italic;">// setup storage</span>
              connectToNNAndHandshake<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
              <span style="color: #000000; font-weight: bold;">break</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">IOException</span> ioe<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
              <span style="color: #666666; font-style: italic;">// Initial handshake, storage recovery or registration failed</span>
              runningState <span style="color: #339933;">=</span> RunningState.<span style="color: #006633;">INIT_FAILED</span><span style="color: #339933;">;</span>
              <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>shouldRetryInit<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                <span style="color: #666666; font-style: italic;">// Retry until all namenode's of BPOS failed initialization</span>
                LOG.<span style="color: #006633;">error</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Initialization failed for &quot;</span> <span style="color: #339933;">+</span> <span style="color: #000000; font-weight: bold;">this</span> <span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot; &quot;</span>
                    <span style="color: #339933;">+</span> ioe.<span style="color: #006633;">getLocalizedMessage</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                sleepAndLogInterrupts<span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">5000</span>, <span style="color: #0000ff;">&quot;initializing&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
              <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">else</span> <span style="color: #009900;">&#123;</span>
                runningState <span style="color: #339933;">=</span> RunningState.<span style="color: #006633;">FAILED</span><span style="color: #339933;">;</span>
                LOG.<span style="color: #006633;">fatal</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Initialization failed for &quot;</span> <span style="color: #339933;">+</span> <span style="color: #000000; font-weight: bold;">this</span> <span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot;. Exiting. &quot;</span>, ioe<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #000000; font-weight: bold;">return</span><span style="color: #339933;">;</span>
              <span style="color: #009900;">&#125;</span>
            <span style="color: #009900;">&#125;</span>
          <span style="color: #009900;">&#125;</span>
    &nbsp;
          runningState <span style="color: #339933;">=</span> RunningState.<span style="color: #006633;">RUNNING</span><span style="color: #339933;">;</span>
    &nbsp;
          <span style="color: #000000; font-weight: bold;">while</span> <span style="color: #009900;">&#40;</span>shouldRun<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#123;</span>
              <span style="color: #666666; font-style: italic;">// 更新当前那个是active actor，发送blockReport给namenode等</span>
              offerService<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">Exception</span> ex<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
              LOG.<span style="color: #006633;">error</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Exception in BPOfferService for &quot;</span> <span style="color: #339933;">+</span> <span style="color: #000000; font-weight: bold;">this</span>, ex<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
              sleepAndLogInterrupts<span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">5000</span>, <span style="color: #0000ff;">&quot;offering service&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
          <span style="color: #009900;">&#125;</span>
          runningState <span style="color: #339933;">=</span> RunningState.<span style="color: #006633;">EXITED</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">Throwable</span> ex<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          LOG.<span style="color: #006633;">warn</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Unexpected exception in block pool &quot;</span> <span style="color: #339933;">+</span> <span style="color: #000000; font-weight: bold;">this</span>, ex<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          runningState <span style="color: #339933;">=</span> RunningState.<span style="color: #006633;">FAILED</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">finally</span> <span style="color: #009900;">&#123;</span>
          LOG.<span style="color: #006633;">warn</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Ending block pool service for: &quot;</span> <span style="color: #339933;">+</span> <span style="color: #000000; font-weight: bold;">this</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          cleanUp<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
      <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">  public void run() {
        LOG.info(this + &quot; starting to offer service&quot;);
    
        try {
          while (true) {
            // init stuff
            try {
              // 向namenode注册以及初始化blockPool
              // setup storage
              connectToNNAndHandshake();
              break;
            } catch (IOException ioe) {
              // Initial handshake, storage recovery or registration failed
              runningState = RunningState.INIT_FAILED;
              if (shouldRetryInit()) {
                // Retry until all namenode's of BPOS failed initialization
                LOG.error(&quot;Initialization failed for &quot; + this + &quot; &quot;
                    + ioe.getLocalizedMessage());
                sleepAndLogInterrupts(5000, &quot;initializing&quot;);
              } else {
                runningState = RunningState.FAILED;
                LOG.fatal(&quot;Initialization failed for &quot; + this + &quot;. Exiting. &quot;, ioe);
                return;
              }
            }
          }
    
          runningState = RunningState.RUNNING;
    
          while (shouldRun()) {
            try {
              // 更新当前那个是active actor，发送blockReport给namenode等
              offerService();
            } catch (Exception ex) {
              LOG.error(&quot;Exception in BPOfferService for &quot; + this, ex);
              sleepAndLogInterrupts(5000, &quot;offering service&quot;);
            }
          }
          runningState = RunningState.EXITED;
        } catch (Throwable ex) {
          LOG.warn(&quot;Unexpected exception in block pool &quot; + this, ex);
          runningState = RunningState.FAILED;
        } finally {
          LOG.warn(&quot;Ending block pool service for: &quot; + this);
          cleanUp();
        }
      }</p></div>
    ";i:9;s:3225:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">  <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000066; font-weight: bold;">void</span> connectToNNAndHandshake<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">throws</span> <span style="color: #003399;">IOException</span> <span style="color: #009900;">&#123;</span>
        <span style="color: #666666; font-style: italic;">// get NN proxy</span>
        bpNamenode <span style="color: #339933;">=</span> dn.<span style="color: #006633;">connectToNN</span><span style="color: #009900;">&#40;</span>nnAddr<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
         <span style="color: #666666; font-style: italic;">// 从namenode获取一些版本等信息用于校验</span>
        <span style="color: #666666; font-style: italic;">// First phase of the handshake with NN - get the namespace</span>
        <span style="color: #666666; font-style: italic;">// info.</span>
        NamespaceInfo nsInfo <span style="color: #339933;">=</span> retrieveNamespaceInfo<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #666666; font-style: italic;">// Verify that this matches the other NN in this HA pair.</span>
        <span style="color: #666666; font-style: italic;">// This also initializes our block pool in the DN if we are</span>
        <span style="color: #666666; font-style: italic;">// the first NN connection for this BP.</span>
        bpos.<span style="color: #006633;">verifyAndSetNamespaceInfo</span><span style="color: #009900;">&#40;</span>nsInfo<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
         <span style="color: #666666; font-style: italic;">// 向namenode注册，并且设定了一下blockReport的时间（当前时间 - (blockReportInterval - delay)），默认是马上</span>
        <span style="color: #666666; font-style: italic;">// Second phase of the handshake with the NN.</span>
        register<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
      <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">  private void connectToNNAndHandshake() throws IOException {
        // get NN proxy
        bpNamenode = dn.connectToNN(nnAddr);
    
         // 从namenode获取一些版本等信息用于校验
        // First phase of the handshake with NN - get the namespace
        // info.
        NamespaceInfo nsInfo = retrieveNamespaceInfo();
        
        // Verify that this matches the other NN in this HA pair.
        // This also initializes our block pool in the DN if we are
        // the first NN connection for this BP.
        bpos.verifyAndSetNamespaceInfo(nsInfo);
        
         // 向namenode注册，并且设定了一下blockReport的时间（当前时间 - (blockReportInterval - delay)），默认是马上
        // Second phase of the handshake with the NN.
        register();
      }</p></div>
    ";i:10;s:5777:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">  <span style="color: #000066; font-weight: bold;">void</span> initBlockPool<span style="color: #009900;">&#40;</span>BPOfferService bpos<span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">throws</span> <span style="color: #003399;">IOException</span> <span style="color: #009900;">&#123;</span>
        NamespaceInfo nsInfo <span style="color: #339933;">=</span> bpos.<span style="color: #006633;">getNamespaceInfo</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>nsInfo <span style="color: #339933;">==</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #000000; font-weight: bold;">throw</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">IOException</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;NamespaceInfo not found: Block pool &quot;</span> <span style="color: #339933;">+</span> bpos
              <span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot; should have retrieved namespace info before initBlockPool.&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        setClusterId<span style="color: #009900;">&#40;</span>nsInfo.<span style="color: #006633;">clusterID</span>, nsInfo.<span style="color: #006633;">getBlockPoolID</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #666666; font-style: italic;">// 把BlockPoolId和BPOfferService关联起来，存放在bpByBlockPoolId</span>
        <span style="color: #666666; font-style: italic;">// Register the new block pool with the BP manager.</span>
        blockPoolManager.<span style="color: #006633;">addBlockPool</span><span style="color: #009900;">&#40;</span>bpos<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #666666; font-style: italic;">// 初始化data变量，创建出FsDatasetImpl</span>
        <span style="color: #666666; font-style: italic;">// In the case that this is the first block pool to connect, initialize</span>
        <span style="color: #666666; font-style: italic;">// the dataset, block scanners, etc.</span>
        initStorage<span style="color: #009900;">&#40;</span>nsInfo<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #666666; font-style: italic;">// 去掉坏了的磁盘</span>
        <span style="color: #666666; font-style: italic;">// Exclude failed disks before initializing the block pools to avoid startup</span>
        <span style="color: #666666; font-style: italic;">// failures.</span>
        checkDiskError<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #666666; font-style: italic;">// 开启DirectoryScanner，定期运行，用于处理内存中的对象和实际存储文件的差异</span>
        initDirectoryScanner<span style="color: #009900;">&#40;</span>conf<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #666666; font-style: italic;">// 添加blockPool</span>
        data.<span style="color: #006633;">addBlockPool</span><span style="color: #009900;">&#40;</span>nsInfo.<span style="color: #006633;">getBlockPoolID</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, conf<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        blockScanner.<span style="color: #006633;">enableBlockPoolId</span><span style="color: #009900;">&#40;</span>bpos.<span style="color: #006633;">getBlockPoolId</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
      <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">  void initBlockPool(BPOfferService bpos) throws IOException {
        NamespaceInfo nsInfo = bpos.getNamespaceInfo();
        if (nsInfo == null) {
          throw new IOException(&quot;NamespaceInfo not found: Block pool &quot; + bpos
              + &quot; should have retrieved namespace info before initBlockPool.&quot;);
        }
        
        setClusterId(nsInfo.clusterID, nsInfo.getBlockPoolID());
    
        // 把BlockPoolId和BPOfferService关联起来，存放在bpByBlockPoolId
        // Register the new block pool with the BP manager.
        blockPoolManager.addBlockPool(bpos);
        
        // 初始化data变量，创建出FsDatasetImpl
        // In the case that this is the first block pool to connect, initialize
        // the dataset, block scanners, etc.
        initStorage(nsInfo);
    
        // 去掉坏了的磁盘
        // Exclude failed disks before initializing the block pools to avoid startup
        // failures.
        checkDiskError();
    
        // 开启DirectoryScanner，定期运行，用于处理内存中的对象和实际存储文件的差异
        initDirectoryScanner(conf);
        // 添加blockPool
        data.addBlockPool(nsInfo.getBlockPoolID(), conf);
        blockScanner.enableBlockPoolId(bpos.getBlockPoolId());
      }</p></div>
    ";i:11;s:2770:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">  <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> addBlockPool<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> bpid, Configuration conf<span style="color: #009900;">&#41;</span>
          <span style="color: #000000; font-weight: bold;">throws</span> <span style="color: #003399;">IOException</span> <span style="color: #009900;">&#123;</span>
        LOG.<span style="color: #006633;">info</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Adding block pool &quot;</span> <span style="color: #339933;">+</span> bpid<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #000000; font-weight: bold;">synchronized</span><span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">this</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #666666; font-style: italic;">// 创建BlockPoolSlice对象，加入bpSlices变量内</span>
          volumes.<span style="color: #006633;">addBlockPool</span><span style="color: #009900;">&#40;</span>bpid, conf<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #666666; font-style: italic;">// 初始化ReplicaMap对象（ReplicaMap：Maintains the replica map）</span>
          volumeMap.<span style="color: #006633;">initBlockPool</span><span style="color: #009900;">&#40;</span>bpid<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
        <span style="color: #666666; font-style: italic;">// 获取所有磁盘的副本map</span>
        volumes.<span style="color: #006633;">getAllVolumesMap</span><span style="color: #009900;">&#40;</span>bpid, volumeMap, ramDiskReplicaTracker<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
      <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">  public void addBlockPool(String bpid, Configuration conf)
          throws IOException {
        LOG.info(&quot;Adding block pool &quot; + bpid);
        synchronized(this) {
          // 创建BlockPoolSlice对象，加入bpSlices变量内
          volumes.addBlockPool(bpid, conf);
          // 初始化ReplicaMap对象（ReplicaMap：Maintains the replica map）
          volumeMap.initBlockPool(bpid);
        }
        // 获取所有磁盘的副本map
        volumes.getAllVolumesMap(bpid, volumeMap, ramDiskReplicaTracker);
      }</p></div>
    ";i:12;s:8808:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">  <span style="color: #000066; font-weight: bold;">void</span> addBlockPool<span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">final</span> <span style="color: #003399;">String</span> bpid, <span style="color: #000000; font-weight: bold;">final</span> Configuration conf<span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">throws</span> <span style="color: #003399;">IOException</span> <span style="color: #009900;">&#123;</span>
        <span style="color: #000066; font-weight: bold;">long</span> totalStartTime <span style="color: #339933;">=</span> <span style="color: #003399;">Time</span>.<span style="color: #006633;">monotonicNow</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">final</span> List<span style="color: #339933;">&lt;</span>IOException<span style="color: #339933;">&gt;</span> exceptions <span style="color: #339933;">=</span> <span style="color: #003399;">Collections</span>.<span style="color: #006633;">synchronizedList</span><span style="color: #009900;">&#40;</span>
            <span style="color: #000000; font-weight: bold;">new</span> ArrayList<span style="color: #339933;">&lt;</span>IOException<span style="color: #339933;">&gt;</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        List<span style="color: #339933;">&lt;</span>Thread<span style="color: #339933;">&gt;</span> blockPoolAddingThreads <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> ArrayList<span style="color: #339933;">&lt;</span>Thread<span style="color: #339933;">&gt;</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">final</span> FsVolumeImpl v <span style="color: #339933;">:</span> volumes.<span style="color: #006633;">get</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #003399;">Thread</span> t <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">Thread</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> run<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
              <span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#40;</span>FsVolumeReference ref <span style="color: #339933;">=</span> v.<span style="color: #006633;">obtainReference</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                FsDatasetImpl.<span style="color: #006633;">LOG</span>.<span style="color: #006633;">info</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Scanning block pool &quot;</span> <span style="color: #339933;">+</span> bpid <span style="color: #339933;">+</span>
                    <span style="color: #0000ff;">&quot; on volume &quot;</span> <span style="color: #339933;">+</span> v <span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot;...&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #000066; font-weight: bold;">long</span> startTime <span style="color: #339933;">=</span> <span style="color: #003399;">Time</span>.<span style="color: #006633;">monotonicNow</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #666666; font-style: italic;">// 创建BlockPoolSlice</span>
                v.<span style="color: #006633;">addBlockPool</span><span style="color: #009900;">&#40;</span>bpid, conf<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #000066; font-weight: bold;">long</span> timeTaken <span style="color: #339933;">=</span> <span style="color: #003399;">Time</span>.<span style="color: #006633;">monotonicNow</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">-</span> startTime<span style="color: #339933;">;</span>
                FsDatasetImpl.<span style="color: #006633;">LOG</span>.<span style="color: #006633;">info</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Time taken to scan block pool &quot;</span> <span style="color: #339933;">+</span> bpid <span style="color: #339933;">+</span>
                    <span style="color: #0000ff;">&quot; on &quot;</span> <span style="color: #339933;">+</span> v <span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot;: &quot;</span> <span style="color: #339933;">+</span> timeTaken <span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot;ms&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
              <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span>ClosedChannelException e<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                <span style="color: #666666; font-style: italic;">// ignore.</span>
              <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">IOException</span> ioe<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                FsDatasetImpl.<span style="color: #006633;">LOG</span>.<span style="color: #006633;">info</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Caught exception while scanning &quot;</span> <span style="color: #339933;">+</span> v <span style="color: #339933;">+</span>
                    <span style="color: #0000ff;">&quot;. Will throw later.&quot;</span>, ioe<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                exceptions.<span style="color: #006633;">add</span><span style="color: #009900;">&#40;</span>ioe<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
              <span style="color: #009900;">&#125;</span>
            <span style="color: #009900;">&#125;</span>
          <span style="color: #009900;">&#125;</span><span style="color: #339933;">;</span></pre></td></tr></table><p class="theCode" style="display:none;">  void addBlockPool(final String bpid, final Configuration conf) throws IOException {
        long totalStartTime = Time.monotonicNow();
        
        final List&lt;IOException&gt; exceptions = Collections.synchronizedList(
            new ArrayList&lt;IOException&gt;());
        List&lt;Thread&gt; blockPoolAddingThreads = new ArrayList&lt;Thread&gt;();
        for (final FsVolumeImpl v : volumes.get()) {
          Thread t = new Thread() {
            public void run() {
              try (FsVolumeReference ref = v.obtainReference()) {
                FsDatasetImpl.LOG.info(&quot;Scanning block pool &quot; + bpid +
                    &quot; on volume &quot; + v + &quot;...&quot;);
                long startTime = Time.monotonicNow();
                // 创建BlockPoolSlice
                v.addBlockPool(bpid, conf);
                long timeTaken = Time.monotonicNow() - startTime;
                FsDatasetImpl.LOG.info(&quot;Time taken to scan block pool &quot; + bpid +
                    &quot; on &quot; + v + &quot;: &quot; + timeTaken + &quot;ms&quot;);
              } catch (ClosedChannelException e) {
                // ignore.
              } catch (IOException ioe) {
                FsDatasetImpl.LOG.info(&quot;Caught exception while scanning &quot; + v +
                    &quot;. Will throw later.&quot;, ioe);
                exceptions.add(ioe);
              }
            }
          };</p></div>
    ";i:13;s:3669:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">  <span style="color: #000066; font-weight: bold;">void</span> getVolumeMap<span style="color: #009900;">&#40;</span>ReplicaMap volumeMap,
                        <span style="color: #000000; font-weight: bold;">final</span> RamDiskReplicaTracker lazyWriteReplicaMap<span style="color: #009900;">&#41;</span>
          <span style="color: #000000; font-weight: bold;">throws</span> <span style="color: #003399;">IOException</span> <span style="color: #009900;">&#123;</span>
        <span style="color: #666666; font-style: italic;">// Recover lazy persist replicas, they will be added to the volumeMap</span>
        <span style="color: #666666; font-style: italic;">// when we scan the finalized directory.</span>
        <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>lazypersistDir.<span style="color: #006633;">exists</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #000066; font-weight: bold;">int</span> numRecovered <span style="color: #339933;">=</span> moveLazyPersistReplicasToFinalized<span style="color: #009900;">&#40;</span>lazypersistDir<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          FsDatasetImpl.<span style="color: #006633;">LOG</span>.<span style="color: #006633;">info</span><span style="color: #009900;">&#40;</span>
              <span style="color: #0000ff;">&quot;Recovered &quot;</span> <span style="color: #339933;">+</span> numRecovered <span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot; replicas from &quot;</span> <span style="color: #339933;">+</span> lazypersistDir<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        <span style="color: #666666; font-style: italic;">// 遍历底下所有目录，构造副本map</span>
        <span style="color: #666666; font-style: italic;">// add finalized replicas</span>
        addToReplicasMap<span style="color: #009900;">&#40;</span>volumeMap, finalizedDir, lazyWriteReplicaMap, <span style="color: #000066; font-weight: bold;">true</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #666666; font-style: italic;">// add rbw replicas</span>
        addToReplicasMap<span style="color: #009900;">&#40;</span>volumeMap, rbwDir, lazyWriteReplicaMap, <span style="color: #000066; font-weight: bold;">false</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
      <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">  void getVolumeMap(ReplicaMap volumeMap,
                        final RamDiskReplicaTracker lazyWriteReplicaMap)
          throws IOException {
        // Recover lazy persist replicas, they will be added to the volumeMap
        // when we scan the finalized directory.
        if (lazypersistDir.exists()) {
          int numRecovered = moveLazyPersistReplicasToFinalized(lazypersistDir);
          FsDatasetImpl.LOG.info(
              &quot;Recovered &quot; + numRecovered + &quot; replicas from &quot; + lazypersistDir);
        }
    
        // 遍历底下所有目录，构造副本map
        // add finalized replicas
        addToReplicasMap(volumeMap, finalizedDir, lazyWriteReplicaMap, true);
        // add rbw replicas
        addToReplicasMap(volumeMap, rbwDir, lazyWriteReplicaMap, false);
      }</p></div>
    ";}
categories:
  - hadoop
tags:
  - datanode
  - hadoop
  - hdfs

---
## 背景

最近打算要重启DataNode，之前有试过重启过程中导致业务任务失败的情况。所以想了解DataNode什么时候才算启动完成，以及能否检测DataNode是否已经准备好了。  
本文分析的源码版本是hadoop cdh5.4.0
## 源码分析

从Datanode.java main方法开始
<pre lang="java" escaped="true">public static void main(String args[]) {
    if (DFSUtil.parseHelpArgument(args, DataNode.USAGE, System.out, true)) {
      System.exit(0);
    }

    secureMain(args, null);
  }</pre>
进入secureMain方法，这里调用了createDataNode方法
<pre lang="java" escaped="true">public static DataNode createDataNode(String args[], Configuration conf,
      SecureResources resources) throws IOException {
    // 实例化datanode
    DataNode dn = instantiateDataNode(args, conf, resources);
    if (dn != null) {
      // 启动BPOfferService、dataXceiverServer、ipcServer等
      dn.runDatanodeDaemon();
    }
    return dn;
  }</pre>
<pre lang="java" escaped="true">public static DataNode instantiateDataNode(String args [], Configuration conf,
      SecureResources resources) throws IOException {
    if (conf == null)
      conf = new HdfsConfiguration();
    
    if (args != null) {
      // parse generic hadoop options
      GenericOptionsParser hParser = new GenericOptionsParser(conf, args);
      args = hParser.getRemainingArgs();
    }
    
    if (!parseArguments(args, conf)) {
      printUsage(System.err);
      return null;
    }
    // 获取实际的存储路径（根据配置dfs.datanode.data.dir）
    Collection&lt;StorageLocation&gt; dataLocations = getStorageLocations(conf);
    UserGroupInformation.setConfiguration(conf);
    SecurityUtil.login(conf, DFS_DATANODE_KEYTAB_FILE_KEY,
        DFS_DATANODE_KERBEROS_PRINCIPAL_KEY);
    return makeInstance(dataLocations, conf, resources);
  }</pre>
<pre lang="java" escaped="true">static DataNode makeInstance(Collection&lt;StorageLocation&gt; dataDirs,
      Configuration conf, SecureResources resources) throws IOException {
    LocalFileSystem localFS = FileSystem.getLocal(conf);
    FsPermission permission = new FsPermission(
        conf.get(DFS_DATANODE_DATA_DIR_PERMISSION_KEY,
                 DFS_DATANODE_DATA_DIR_PERMISSION_DEFAULT));
    // DataNode磁盘检查类，检查目录权限以及是否能够创建目录
    DataNodeDiskChecker dataNodeDiskChecker =
        new DataNodeDiskChecker(permission);
    // 找出能够正常读写的路径
    List&lt;StorageLocation&gt; locations =
        checkStorageLocations(dataDirs, localFS, dataNodeDiskChecker);
    DefaultMetricsSystem.initialize("DataNode");

    assert locations.size() &gt; 0 : "number of data directories should be &gt; 0";
    return new DataNode(conf, locations, resources);
  }</pre>
进入DataNode构造方法，主要看startDataNode(conf, dataDirs, resources)方法
<pre lang="java" escaped="true">void startDataNode(Configuration conf, 
                     List&lt;StorageLocation&gt; dataDirs,
                     SecureResources resources
                     ) throws IOException {

    // settings global for all BPs in the Data Node
    this.secureResources = resources;
    synchronized (this) {
      this.dataDirs = dataDirs;
    }
    this.conf = conf;
    this.dnConf = new DNConf(conf);
    checkSecureConfig(dnConf, conf, resources);

    this.spanReceiverHost = SpanReceiverHost.getInstance(conf);

    if (dnConf.maxLockedMemory &gt; 0) {
      if (!NativeIO.POSIX.getCacheManipulator().verifyCanMlock()) {
        throw new RuntimeException(String.format(
            "Cannot start datanode because the configured max locked memory" +
            " size (%s) is greater than zero and native code is not available.",
            DFS_DATANODE_MAX_LOCKED_MEMORY_KEY));
      }
      if (Path.WINDOWS) {
        NativeIO.Windows.extendWorkingSetSize(dnConf.maxLockedMemory);
      } else {
        long ulimit = NativeIO.POSIX.getCacheManipulator().getMemlockLimit();
        if (dnConf.maxLockedMemory &gt; ulimit) {
          throw new RuntimeException(String.format(
            "Cannot start datanode because the configured max locked memory" +
            " size (%s) of %d bytes is more than the datanode's available" +
            " RLIMIT_MEMLOCK ulimit of %d bytes.",
            DFS_DATANODE_MAX_LOCKED_MEMORY_KEY,
            dnConf.maxLockedMemory,
            ulimit));
        }
      }
    }
    LOG.info("Starting DataNode with maxLockedMemory = " +
        dnConf.maxLockedMemory);

    storage = new DataStorage();
    
    // global DN settings
    registerMXBean();
    // 初始化xceiverServer一些对象
    initDataXceiver(conf);
    // 启动http web hdfs
    startInfoServer(conf);
    pauseMonitor = new JvmPauseMonitor(conf);
    pauseMonitor.start();
  
    // BlockPoolTokenSecretManager is required to create ipc server.
    this.blockPoolTokenSecretManager = new BlockPoolTokenSecretManager();

    // Login is done by now. Set the DN user name.
    dnUserName = UserGroupInformation.getCurrentUser().getShortUserName();
    LOG.info("dnUserName = " + dnUserName);
    LOG.info("supergroup = " + supergroup);
    // 初始化ipc服务
    initIpcServer(conf);

    metrics = DataNodeMetrics.create(conf, getDisplayName());
    metrics.getJvmMetrics().setPauseMonitor(pauseMonitor);
    
    // 重要，构造BlockPoolManager
    blockPoolManager = new BlockPoolManager(this);
    blockPoolManager.refreshNamenodes(conf);

    // Create the ReadaheadPool from the DataNode context so we can
    // exit without having to explicitly shutdown its thread pool.
    readaheadPool = ReadaheadPool.getInstance();
    saslClient = new SaslDataTransferClient(dnConf.conf, 
        dnConf.saslPropsResolver, dnConf.trustedChannelResolver);
    saslServer = new SaslDataTransferServer(dnConf, blockPoolTokenSecretManager);
  }</pre>
在blockPoolManager.refreshNamenodes里面调用了doRefreshNamenodes()方法
<pre lang="java" escaped="true">private void doRefreshNamenodes(
      Map&lt;String, Map&lt;String, InetSocketAddress&gt;&gt; addrMap) throws IOException {
    assert Thread.holdsLock(refreshNamenodesLock);

    Set&lt;String&gt; toRefresh = Sets.newLinkedHashSet();
    Set&lt;String&gt; toAdd = Sets.newLinkedHashSet();
    Set&lt;String&gt; toRemove;
    
    synchronized (this) {
      // Step 1. For each of the new nameservices, figure out whether
      // it's an update of the set of NNs for an existing NS,
      // or an entirely new nameservice.
      for (String nameserviceId : addrMap.keySet()) {
        if (bpByNameserviceId.containsKey(nameserviceId)) {
          toRefresh.add(nameserviceId);
        } else {
          toAdd.add(nameserviceId);
        }
      }
      
      // Step 2. Any nameservices we currently have but are no longer present
      // need to be removed.
      toRemove = Sets.newHashSet(Sets.difference(
          bpByNameserviceId.keySet(), addrMap.keySet()));
      
      assert toRefresh.size() + toAdd.size() ==
        addrMap.size() :
          "toAdd: " + Joiner.on(",").useForNull("&lt;default&gt;").join(toAdd) +
          "  toRemove: " + Joiner.on(",").useForNull("&lt;default&gt;").join(toRemove) +
          "  toRefresh: " + Joiner.on(",").useForNull("&lt;default&gt;").join(toRefresh);

      
       // 由于是重启，所以都是在toAdd里面
      // Step 3. Start new nameservices
      if (!toAdd.isEmpty()) {
        LOG.info("Starting BPOfferServices for nameservices: " +
            Joiner.on(",").useForNull("&lt;default&gt;").join(toAdd));
        // 这里遍历的是nameServices，如果用了hdfs federation就会有多个
        for (String nsToAdd : toAdd) {
          ArrayList&lt;InetSocketAddress&gt; addrs =
            Lists.newArrayList(addrMap.get(nsToAdd).values());
          // 创建BPOfferService
          BPOfferService bpos = createBPOS(addrs);
          // 加入bpByNameserviceId里面，下次再执行这个方法的话，就是加入toRefresh里面了
          bpByNameserviceId.put(nsToAdd, bpos);
          offerServices.add(bpos);
        }
      }
      // 启动所有offerServices的BPOfferService
      startAll();
    }</pre>
关注一下createBPOS方法，里面会包含多个BPServiceActor，存储在 BPOfferService.bpServices 变量内
<pre lang="java" escaped="true">protected BPOfferService createBPOS(List&lt;InetSocketAddress&gt; nnAddrs) {
    return new BPOfferService(nnAddrs, dn);
  }

  BPOfferService(List&lt;InetSocketAddress&gt; nnAddrs, DataNode dn) {
    Preconditions.checkArgument(!nnAddrs.isEmpty(),
        "Must pass at least one NN.");
    this.dn = dn;

    // 如果有standby和active两个namenode，就会创建两个BPServiceActor
    for (InetSocketAddress addr : nnAddrs) {
      this.bpServices.add(new BPServiceActor(addr, this));
    }
  }</pre>
上面的startAll()把所有的BPOfferService都启动了，实际是调用下面的BPServiceActor.start()，BPServiceActor的作用在这文件的最上面注释写着：1.和namenode预注册，2.和namenode注册，3.周期性发送心跳到namenode，4.处理来自于namenode的命令。继续看这个类的run()方法
<pre lang="java" escaped="true">public void run() {
    LOG.info(this + " starting to offer service");

    try {
      while (true) {
        // init stuff
        try {
          // 向namenode注册以及初始化blockPool
          // setup storage
          connectToNNAndHandshake();
          break;
        } catch (IOException ioe) {
          // Initial handshake, storage recovery or registration failed
          runningState = RunningState.INIT_FAILED;
          if (shouldRetryInit()) {
            // Retry until all namenode's of BPOS failed initialization
            LOG.error("Initialization failed for " + this + " "
                + ioe.getLocalizedMessage());
            sleepAndLogInterrupts(5000, "initializing");
          } else {
            runningState = RunningState.FAILED;
            LOG.fatal("Initialization failed for " + this + ". Exiting. ", ioe);
            return;
          }
        }
      }

      runningState = RunningState.RUNNING;

      while (shouldRun()) {
        try {
          // 更新当前那个是active actor，发送blockReport给namenode等
          offerService();
        } catch (Exception ex) {
          LOG.error("Exception in BPOfferService for " + this, ex);
          sleepAndLogInterrupts(5000, "offering service");
        }
      }
      runningState = RunningState.EXITED;
    } catch (Throwable ex) {
      LOG.warn("Unexpected exception in block pool " + this, ex);
      runningState = RunningState.FAILED;
    } finally {
      LOG.warn("Ending block pool service for: " + this);
      cleanUp();
    }
  }</pre>
关注connectToNNAndHandshake()方法，这里初始化了blockPool
<pre lang="java" escaped="true">private void connectToNNAndHandshake() throws IOException {
    // get NN proxy
    bpNamenode = dn.connectToNN(nnAddr);

     // 从namenode获取一些版本等信息用于校验
    // First phase of the handshake with NN - get the namespace
    // info.
    NamespaceInfo nsInfo = retrieveNamespaceInfo();
    
    // Verify that this matches the other NN in this HA pair.
    // This also initializes our block pool in the DN if we are
    // the first NN connection for this BP.
    bpos.verifyAndSetNamespaceInfo(nsInfo);
    
     // 向namenode注册，并且设定了一下blockReport的时间（当前时间 - (blockReportInterval - delay)），默认是马上
    // Second phase of the handshake with the NN.
    register();
  }</pre>
在verifyAndSetNamespaceInfo()方法里，主要看dn.initBlockPool(this);
<pre lang="java" escaped="true">void initBlockPool(BPOfferService bpos) throws IOException {
    NamespaceInfo nsInfo = bpos.getNamespaceInfo();
    if (nsInfo == null) {
      throw new IOException("NamespaceInfo not found: Block pool " + bpos
          + " should have retrieved namespace info before initBlockPool.");
    }
    
    setClusterId(nsInfo.clusterID, nsInfo.getBlockPoolID());

    // 把BlockPoolId和BPOfferService关联起来，存放在bpByBlockPoolId
    // Register the new block pool with the BP manager.
    blockPoolManager.addBlockPool(bpos);
    
    // 初始化data变量，创建出FsDatasetImpl
    // In the case that this is the first block pool to connect, initialize
    // the dataset, block scanners, etc.
    initStorage(nsInfo);

    // 去掉坏了的磁盘
    // Exclude failed disks before initializing the block pools to avoid startup
    // failures.
    checkDiskError();

    // 开启DirectoryScanner，定期运行，用于处理内存中的对象和实际存储文件的差异
    initDirectoryScanner(conf);
    // 添加blockPool
    data.addBlockPool(nsInfo.getBlockPoolID(), conf);
    blockScanner.enableBlockPoolId(bpos.getBlockPoolId());
  }</pre>
这里面关注的是data.addBlockPool方法
<pre lang="java" escaped="true">public void addBlockPool(String bpid, Configuration conf)
      throws IOException {
    LOG.info("Adding block pool " + bpid);
    synchronized(this) {
      // 创建BlockPoolSlice对象，加入bpSlices变量内
      volumes.addBlockPool(bpid, conf);
      // 初始化ReplicaMap对象（ReplicaMap：Maintains the replica map）
      volumeMap.initBlockPool(bpid);
    }
    // 获取所有磁盘的副本map
    volumes.getAllVolumesMap(bpid, volumeMap, ramDiskReplicaTracker);
  }</pre>
volumes.addBlockPool方法里，是创建BlockPoolSlice。BlockPoolSlice的介绍是说这是BlockPool存储在一个磁盘的一部分，里面主要是记录一些目录，还有使用大小等。注意这个有个计算磁盘使用大小非常耗时，这里使用了缓存，每600秒更新一次，在datanode退出的时候会写把数值写到文件里。
<pre lang="java" escaped="true">void addBlockPool(final String bpid, final Configuration conf) throws IOException {
    long totalStartTime = Time.monotonicNow();
    
    final List&lt;IOException&gt; exceptions = Collections.synchronizedList(
        new ArrayList&lt;IOException&gt;());
    List&lt;Thread&gt; blockPoolAddingThreads = new ArrayList&lt;Thread&gt;();
    for (final FsVolumeImpl v : volumes.get()) {
      Thread t = new Thread() {
        public void run() {
          try (FsVolumeReference ref = v.obtainReference()) {
            FsDatasetImpl.LOG.info("Scanning block pool " + bpid +
                " on volume " + v + "...");
            long startTime = Time.monotonicNow();
            // 创建BlockPoolSlice
            v.addBlockPool(bpid, conf);
            long timeTaken = Time.monotonicNow() - startTime;
            FsDatasetImpl.LOG.info("Time taken to scan block pool " + bpid +
                " on " + v + ": " + timeTaken + "ms");
          } catch (ClosedChannelException e) {
            // ignore.
          } catch (IOException ioe) {
            FsDatasetImpl.LOG.info("Caught exception while scanning " + v +
                ". Will throw later.", ioe);
            exceptions.add(ioe);
          }
        }
      };</pre>
volumes.getAllVolumesMap()方法，实际是调用每一个BlockPoolSlice.getVolumeMap()，我们当前版本在这里没有cache，因为要遍历目录，所以这里的操作比较耗时。添加cache具体见[HDFS-7928][1]补丁。
<pre lang="java" escaped="true">void getVolumeMap(ReplicaMap volumeMap,
                    final RamDiskReplicaTracker lazyWriteReplicaMap)
      throws IOException {
    // Recover lazy persist replicas, they will be added to the volumeMap
    // when we scan the finalized directory.
    if (lazypersistDir.exists()) {
      int numRecovered = moveLazyPersistReplicasToFinalized(lazypersistDir);
      FsDatasetImpl.LOG.info(
          "Recovered " + numRecovered + " replicas from " + lazypersistDir);
    }

    // 遍历底下所有目录，构造副本map
    // add finalized replicas
    addToReplicasMap(volumeMap, finalizedDir, lazyWriteReplicaMap, true);
    // add rbw replicas
    addToReplicasMap(volumeMap, rbwDir, lazyWriteReplicaMap, false);
  }</pre>
回到最上面，执行完bpos.verifyAndSetNamespaceInfo(nsInfo);后，执行register()方法，向namenode注册。执行完后，再往上就是调用offerService()，发送心跳，blockMap等。
## 结论

namenode启动过程中会有多个线程，http和rpc的端口会先启动，但是这个时候还是不能提供服务的。当前版本主要耗时在构建volumeMap上，需要遍历磁盘目录。  
初始化完volumeMap会向namenode注册，注册成功后会在日志打印successfully registered with NN（有两条，active和standby namenode）  
之后datanode向namenode汇报块信息，发送完成后在日志打印Successfully sent block report（同样有两条）  
只有在blockReport完成后才算真的启动完成。
在重启的过程中，如果时间不算太长，在namenode中还没有判定这个datanode为dead node，里面的block map信息还保留着，所以在完成磁盘扫描 volumeMap 之后也算完成了。
## 其他

代码比较多，限于个人能力，可能理解也有误，如果发现错误以后再更新。  
<del>同时也没找出可编程的方法来判断datanode是否启动完成，除非修改datanode代码自己加标志位。</del>
update(2017-07-18)：判断datanode是否启动完成核心在判断两次blockreport是否完成（分别向active和standby namenode发送），所以可以通过访问datanode jmx地址http://xxx:50075/jmx,检查参数&#8221;BlockReportsNumOps&#8221; : 大于等于2来判断。
&nbsp;
## 参考

[第七章：小朱笔记hadoop之源码分析-hdfs分析 第五节：Datanode 分析][2] 版本差异比较大  
[记一次DataNode慢启动问题][3]

 [1]: https://issues.apache.org/jira/browse/HDFS-7928
 [2]: http://huashuizhuhui.iteye.com/blog/1869512
 [3]: http://blog.csdn.net/androidlushangderen/article/details/50500136