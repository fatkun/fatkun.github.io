---
title: Hive MetaStore建表与修改表分析
author: fatkun
type: post
date: 2012-04-10T15:57:54+00:00
url: /2012/04/hive-metastore-create-table-and-alter-table.html
duoshuo_thread_id:
  - 6300408840810660609
wp-syntax-cache-content:
  - |
    a:5:{i:1;s:1052:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> create_table<span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">final</span> Table tbl<span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">throws</span> AlreadyExistsException,
            MetaException, <span style="color: #003399;">InvalidObjectException</span> <span style="color: #009900;">&#123;</span>
    ...
    <span style="color: #006633;">create_table_core</span><span style="color: #009900;">&#40;</span>ms, tbl<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span></pre></td></tr></table><p class="theCode" style="display:none;">public void create_table(final Table tbl) throws AlreadyExistsException,
            MetaException, InvalidObjectException {
    ...
    create_table_core(ms, tbl);</p></div>
    ";i:2;s:7887:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">    <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000066; font-weight: bold;">void</span> create_table_core<span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">final</span> RawStore ms, <span style="color: #000000; font-weight: bold;">final</span> Table tbl<span style="color: #009900;">&#41;</span>
            <span style="color: #000000; font-weight: bold;">throws</span> AlreadyExistsException, MetaException, <span style="color: #003399;">InvalidObjectException</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #666666; font-style: italic;">//检查了一些名称，列名，分区之类的</span>
          <span style="color: #666666; font-style: italic;">//...</span>
            ms.<span style="color: #006633;">openTransaction</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #666666; font-style: italic;">//....</span>
            <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span><span style="color: #339933;">!</span>TableType.<span style="color: #006633;">VIRTUAL_VIEW</span>.<span style="color: #006633;">toString</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">equals</span><span style="color: #009900;">&#40;</span>tbl.<span style="color: #006633;">getTableType</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
              <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>tbl.<span style="color: #006633;">getSd</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getLocation</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">==</span> <span style="color: #000066; font-weight: bold;">null</span>
                <span style="color: #339933;">||</span> tbl.<span style="color: #006633;">getSd</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getLocation</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">isEmpty</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                tblPath <span style="color: #339933;">=</span> wh.<span style="color: #006633;">getDefaultTablePath</span><span style="color: #009900;">&#40;</span>
                  tbl.<span style="color: #006633;">getDbName</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, tbl.<span style="color: #006633;">getTableName</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
              <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">else</span> <span style="color: #009900;">&#123;</span>
                <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span><span style="color: #339933;">!</span>isExternal<span style="color: #009900;">&#40;</span>tbl<span style="color: #009900;">&#41;</span> <span style="color: #339933;">&amp;&amp;</span> <span style="color: #339933;">!</span>MetaStoreUtils.<span style="color: #006633;">isNonNativeTable</span><span style="color: #009900;">&#40;</span>tbl<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                  LOG.<span style="color: #006633;">warn</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Location: &quot;</span> <span style="color: #339933;">+</span> tbl.<span style="color: #006633;">getSd</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getLocation</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>
                    <span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot; specified for non-external table:&quot;</span> <span style="color: #339933;">+</span> tbl.<span style="color: #006633;">getTableName</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #009900;">&#125;</span>
                <span style="color: #666666; font-style: italic;">// 主要就是这里啦！getDnsPath！！！帮我们把dataurl补全</span>
                tblPath <span style="color: #339933;">=</span> wh.<span style="color: #006633;">getDnsPath</span><span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">new</span> Path<span style="color: #009900;">&#40;</span>tbl.<span style="color: #006633;">getSd</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getLocation</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
              <span style="color: #009900;">&#125;</span>
              tbl.<span style="color: #006633;">getSd</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">setLocation</span><span style="color: #009900;">&#40;</span>tblPath.<span style="color: #006633;">toString</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
    &nbsp;
            <span style="color: #666666; font-style: italic;">//...</span>
            ms.<span style="color: #006633;">createTable</span><span style="color: #009900;">&#40;</span>tbl<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">    private void create_table_core(final RawStore ms, final Table tbl)
            throws AlreadyExistsException, MetaException, InvalidObjectException {
    //检查了一些名称，列名，分区之类的
          //...
            ms.openTransaction();
            //....
            if (!TableType.VIRTUAL_VIEW.toString().equals(tbl.getTableType())) {
              if (tbl.getSd().getLocation() == null
                || tbl.getSd().getLocation().isEmpty()) {
                tblPath = wh.getDefaultTablePath(
                  tbl.getDbName(), tbl.getTableName());
              } else {
                if (!isExternal(tbl) &amp;&amp; !MetaStoreUtils.isNonNativeTable(tbl)) {
                  LOG.warn(&quot;Location: &quot; + tbl.getSd().getLocation()
                    + &quot; specified for non-external table:&quot; + tbl.getTableName());
                }
                // 主要就是这里啦！getDnsPath！！！帮我们把dataurl补全
                tblPath = wh.getDnsPath(new Path(tbl.getSd().getLocation()));
              }
              tbl.getSd().setLocation(tblPath.toString());
            }
    
            //...
            ms.createTable(tbl);
    
        }</p></div>
    ";i:3;s:2077:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">  <span style="color: #000000; font-weight: bold;">public</span> Path getDnsPath<span style="color: #009900;">&#40;</span>Path path<span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">throws</span> MetaException <span style="color: #009900;">&#123;</span>
        FileSystem fs <span style="color: #339933;">=</span> getFs<span style="color: #009900;">&#40;</span>path<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #000000; font-weight: bold;">return</span> <span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">new</span> Path<span style="color: #009900;">&#40;</span>fs.<span style="color: #006633;">getUri</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getScheme</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, fs.<span style="color: #006633;">getUri</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getAuthority</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, path
            .<span style="color: #006633;">toUri</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getPath</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
      <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">  public Path getDnsPath(Path path) throws MetaException {
        FileSystem fs = getFs(path);
        return (new Path(fs.getUri().getScheme(), fs.getUri().getAuthority(), path
            .toUri().getPath()));
      }</p></div>
    ";i:4;s:1356:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> alter_table<span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">final</span> <span style="color: #003399;">String</span> dbname, <span style="color: #000000; font-weight: bold;">final</span> <span style="color: #003399;">String</span> name, <span style="color: #000000; font-weight: bold;">final</span> Table newTable<span style="color: #009900;">&#41;</span>
            <span style="color: #000000; font-weight: bold;">throws</span> InvalidOperationException, MetaException <span style="color: #009900;">&#123;</span>
    \\...
     <span style="color: #006633;">alterHandler</span>.<span style="color: #006633;">alterTable</span><span style="color: #009900;">&#40;</span>ms, wh, dbname, name, newTable<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span></pre></td></tr></table><p class="theCode" style="display:none;">    public void alter_table(final String dbname, final String name, final Table newTable)
            throws InvalidOperationException, MetaException {
    \\...
     alterHandler.alterTable(ms, wh, dbname, name, newTable);</p></div>
    ";i:5;s:2456:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> alterTable<span style="color: #009900;">&#40;</span>RawStore msdb, Warehouse wh, <span style="color: #003399;">String</span> dbname,
          <span style="color: #003399;">String</span> name, Table newt<span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">throws</span> InvalidOperationException, MetaException <span style="color: #009900;">&#123;</span>
    <span style="color: #666666; font-style: italic;">//这里主要判断表名有没有改</span>
    <span style="color: #666666; font-style: italic;">//如果改了分区字段则抛错误</span>
    <span style="color: #666666; font-style: italic;">//如果改了表名但location没改或者为空，并且不是外部表，则把数据给移了~</span>
    &nbsp;
    <span style="color: #666666; font-style: italic;">//最后，直接的alterTable了。。？虾米，location就这样保存进去了？！</span>
          <span style="color: #666666; font-style: italic;">// now finally call alter table</span>
          msdb.<span style="color: #006633;">alterTable</span><span style="color: #009900;">&#40;</span>dbname, name, newt<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #666666; font-style: italic;">// commit the changes</span>
          success <span style="color: #339933;">=</span> msdb.<span style="color: #006633;">commitTransaction</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">public void alterTable(RawStore msdb, Warehouse wh, String dbname,
          String name, Table newt) throws InvalidOperationException, MetaException {
    //这里主要判断表名有没有改
    //如果改了分区字段则抛错误
    //如果改了表名但location没改或者为空，并且不是外部表，则把数据给移了~
    
    //最后，直接的alterTable了。。？虾米，location就这样保存进去了？！
          // now finally call alter table
          msdb.alterTable(dbname, name, newt);
          // commit the changes
          success = msdb.commitTransaction();
    }</p></div>
    ";}
categories:
  - J2EE
tags:
  - alter table
  - hive
  - MetaStore
  - table

---
## 问题

使用Hive MetaStore（这里指的是通过thrift连接hiveserver） Create table 和 Alter table的时候遇到一个问题  
建表时指定的location为 /mnt/dfs/xxx，实质上使用hiveMetastore会帮你做一个转换，最后location变成 hdfs://hostname:port/mnt/dfs/xxx的路径  
但在修改表的时候，却不会帮你做这样的转换！！坑爹啊。。你指定的是什么就是什么~
注：通过hive命令行方式执行sql命令建表也是这样，不过修改表的时候，location必须是这样的路径hdfs://hostname:port/mnt/dfs/xxx才可以修改成功，否则报错。
## 分析问题

从代码入手吧。。  
进入这个目录  
hive-0.7.1-cdh3u3\src\metastore\src\java\org\apache\hadoop\hive\metastore  
这里都是hiveserver的代码了。
打开HiveMetaStore.java代码，咱们直奔主题，找create\_table和alter\_table去
<pre escaped="true" lang="java">public void create_table(final Table tbl) throws AlreadyExistsException,
        MetaException, InvalidObjectException {
...
create_table_core(ms, tbl);
</pre>
调用了create\_table\_core(ms, tbl);继续
<pre escaped="true" lang="java">private void create_table_core(final RawStore ms, final Table tbl)
        throws AlreadyExistsException, MetaException, InvalidObjectException {
//检查了一些名称，列名，分区之类的
      //...
        ms.openTransaction();
        //....
        if (!TableType.VIRTUAL_VIEW.toString().equals(tbl.getTableType())) {
          if (tbl.getSd().getLocation() == null
            || tbl.getSd().getLocation().isEmpty()) {
            tblPath = wh.getDefaultTablePath(
              tbl.getDbName(), tbl.getTableName());
          } else {
            if (!isExternal(tbl) && !MetaStoreUtils.isNonNativeTable(tbl)) {
              LOG.warn("Location: " + tbl.getSd().getLocation()
                + " specified for non-external table:" + tbl.getTableName());
            }
            // 主要就是这里啦！getDnsPath！！！帮我们把dataurl补全
            tblPath = wh.getDnsPath(new Path(tbl.getSd().getLocation()));
          }
          tbl.getSd().setLocation(tblPath.toString());
        }

        //...
        ms.createTable(tbl);

    }</pre>
因为我们的location不为空~所以..  
主要就是这一句：tblPath = wh.getDnsPath(new Path(tbl.getSd().getLocation()));  
看看getDnsPath()做了什么，打开代码Warehouse.java
<pre escaped="true" lang="java">public Path getDnsPath(Path path) throws MetaException {
    FileSystem fs = getFs(path);
    return (new Path(fs.getUri().getScheme(), fs.getUri().getAuthority(), path
        .toUri().getPath()));
  }</pre>
就帮我们做了些转换。。。我们建表看到的hdfs://hostname:port就是这里加上的。
再来看一下alter_table
<pre escaped="true" lang="java">public void alter_table(final String dbname, final String name, final Table newTable)
        throws InvalidOperationException, MetaException {
\\...
 alterHandler.alterTable(ms, wh, dbname, name, newTable);</pre>
跳入这个类HiveAlterHandler.java，只有一个方法：
<pre escaped="true" lang="java">public void alterTable(RawStore msdb, Warehouse wh, String dbname,
      String name, Table newt) throws InvalidOperationException, MetaException {
//这里主要判断表名有没有改
//如果改了分区字段则抛错误
//如果改了表名但location没改或者为空，并且不是外部表，则把数据给移了~

//最后，直接的alterTable了。。？虾米，location就这样保存进去了？！
      // now finally call alter table
      msdb.alterTable(dbname, name, newt);
      // commit the changes
      success = msdb.commitTransaction();
}</pre>
location没做什么处理就保存进去了。。。
RawStore是什么东西？代码中很多用了反射的方式调用。。貌似实质上是ObjectStore.java类。。  
这个类使用jdo来操作metastore数据库