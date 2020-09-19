---
title: parquet-hive列裁剪和谓词下推
author: fatkun
type: post
date: 2016-11-20T13:36:21+00:00
url: /2016/11/parquet-hive-projection-and-push-down.html
duoshuo_thread_id:
  - 6355045281741931265
wp-syntax-cache-content:
  - |
    a:4:{i:1;s:2697:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;"><span style="color: #993333; font-weight: bold;">CREATE</span> <span style="color: #993333; font-weight: bold;">TABLE</span> parquet <span style="color: #66cc66;">&#40;</span>x <span style="color: #993333; font-weight: bold;">INT</span><span style="color: #66cc66;">,</span> y STRING<span style="color: #66cc66;">&#41;</span> STORED <span style="color: #993333; font-weight: bold;">AS</span> PARQUET;
    <span style="color: #993333; font-weight: bold;">CREATE</span> <span style="color: #993333; font-weight: bold;">TABLE</span> parquet2 <span style="color: #66cc66;">&#40;</span>x <span style="color: #993333; font-weight: bold;">INT</span><span style="color: #66cc66;">,</span> y STRING<span style="color: #66cc66;">&#41;</span> STORED <span style="color: #993333; font-weight: bold;">AS</span> PARQUET;
    <span style="color: #993333; font-weight: bold;">CREATE</span> <span style="color: #993333; font-weight: bold;">TABLE</span> test <span style="color: #66cc66;">&#40;</span>x <span style="color: #993333; font-weight: bold;">INT</span><span style="color: #66cc66;">,</span> y STRING<span style="color: #66cc66;">&#41;</span> <span style="color: #993333; font-weight: bold;">ROW</span> FORMAT DELIMITED <span style="color: #993333; font-weight: bold;">FIELDS</span> <span style="color: #993333; font-weight: bold;">TERMINATED</span> <span style="color: #993333; font-weight: bold;">BY</span> <span style="color: #ff0000;">'`'</span>;
    <span style="color: #808080; font-style: italic;">-- 手工构造数据进test表</span>
    <span style="color: #993333; font-weight: bold;">INSERT</span> OVERWRITE <span style="color: #993333; font-weight: bold;">TABLE</span> parquet <span style="color: #993333; font-weight: bold;">SELECT</span> x<span style="color: #66cc66;">,</span>y <span style="color: #993333; font-weight: bold;">FROM</span> test;
    <span style="color: #993333; font-weight: bold;">INSERT</span> OVERWRITE <span style="color: #993333; font-weight: bold;">TABLE</span> parquet2 <span style="color: #993333; font-weight: bold;">SELECT</span> x<span style="color: #66cc66;">,</span>y <span style="color: #993333; font-weight: bold;">FROM</span> test;</pre></td></tr></table><p class="theCode" style="display:none;">CREATE TABLE parquet (x INT, y STRING) STORED AS PARQUET;
    CREATE TABLE parquet2 (x INT, y STRING) STORED AS PARQUET;
    CREATE TABLE test (x INT, y STRING) ROW FORMAT DELIMITED FIELDS TERMINATED BY '`';
    -- 手工构造数据进test表
    INSERT OVERWRITE TABLE parquet SELECT x,y FROM test;
    INSERT OVERWRITE TABLE parquet2 SELECT x,y FROM test;</p></div>
    ";i:2;s:1140:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">SET mapred.job.tracker=<span style="color: #7a0874; font-weight: bold;">local</span>;
    SET hive.exec.mode.local.auto=<span style="color: #c20cb9; font-weight: bold;">true</span>;
    SET fs.defaultFS=file:<span style="color: #000000; font-weight: bold;">///</span>; 
    <span style="color: #660033;">--</span> 避免转成mapjoin
    SET hive.auto.convert.join=<span style="color: #c20cb9; font-weight: bold;">false</span>; 
    <span style="color: #000000; font-weight: bold;">select</span> a.x, b.y from parquet a left <span style="color: #c20cb9; font-weight: bold;">join</span> parquet2 b on <span style="color: #7a0874; font-weight: bold;">&#40;</span>a.x = b.x<span style="color: #7a0874; font-weight: bold;">&#41;</span>;</pre></td></tr></table><p class="theCode" style="display:none;">SET mapred.job.tracker=local;
    SET hive.exec.mode.local.auto=true;
    SET fs.defaultFS=file:///; 
    -- 避免转成mapjoin
    SET hive.auto.convert.join=false; 
    select a.x, b.y from parquet a left join parquet2 b on (a.x = b.x);</p></div>
    ";i:3;s:1747:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000066; font-weight: bold;">void</span> pushFilters<span style="color: #009900;">&#40;</span>JobConf jobConf, TableScanOperator tableScan<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
        <span style="color: #666666; font-style: italic;">// construct column name list and types for reference by filter push down</span>
        <span style="color: #003399;">Utilities</span>.<span style="color: #006633;">setColumnNameList</span><span style="color: #009900;">&#40;</span>jobConf, tableScan<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">// 在conf里设置columns</span>
        <span style="color: #003399;">Utilities</span>.<span style="color: #006633;">setColumnTypeList</span><span style="color: #009900;">&#40;</span>jobConf, tableScan<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">// 在conf里设置columns.types</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">public static void pushFilters(JobConf jobConf, TableScanOperator tableScan) {
        // construct column name list and types for reference by filter push down
        Utilities.setColumnNameList(jobConf, tableScan); // 在conf里设置columns
        Utilities.setColumnTypeList(jobConf, tableScan); // 在conf里设置columns.types
    }</p></div>
    ";i:4;s:12301:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"> <span style="color: #000000; font-weight: bold;">protected</span> <span style="color: #000066; font-weight: bold;">void</span> pushProjectionsAndFilters<span style="color: #009900;">&#40;</span>JobConf jobConf, <span style="color: #000000; font-weight: bold;">Class</span> inputFormatClass,
          <span style="color: #003399;">String</span> splitPath, <span style="color: #003399;">String</span> splitPathWithNoSchema, <span style="color: #000066; font-weight: bold;">boolean</span> nonNative<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
        <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">mrwork</span> <span style="color: #339933;">==</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          init<span style="color: #009900;">&#40;</span>job<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">if</span><span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">mrwork</span>.<span style="color: #006633;">getPathToAliases</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">==</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #000000; font-weight: bold;">return</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        ArrayList<span style="color: #339933;">&lt;</span>String<span style="color: #339933;">&gt;</span> aliases <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> ArrayList<span style="color: #339933;">&lt;</span>String<span style="color: #339933;">&gt;</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        Iterator<span style="color: #339933;">&lt;</span>Entry<span style="color: #339933;">&lt;</span><span style="color: #003399;">String</span>, ArrayList<span style="color: #339933;">&lt;</span>String<span style="color: #339933;">&gt;&gt;&gt;</span> iterator <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">mrwork</span>
            .<span style="color: #006633;">getPathToAliases</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">entrySet</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">iterator</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">while</span> <span style="color: #009900;">&#40;</span>iterator.<span style="color: #006633;">hasNext</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          Entry<span style="color: #339933;">&lt;</span><span style="color: #003399;">String</span>, ArrayList<span style="color: #339933;">&lt;</span>String<span style="color: #339933;">&gt;&gt;</span> entry <span style="color: #339933;">=</span> iterator.<span style="color: #006633;">next</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #003399;">String</span> key <span style="color: #339933;">=</span> entry.<span style="color: #006633;">getKey</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #000066; font-weight: bold;">boolean</span> match<span style="color: #339933;">;</span>
          <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>nonNative<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #666666; font-style: italic;">// For non-native tables, we need to do an exact match to avoid</span>
            <span style="color: #666666; font-style: italic;">// HIVE-1903.  (The table location contains no files, and the string</span>
            <span style="color: #666666; font-style: italic;">// representation of its path does not have a trailing slash.)</span>
            match <span style="color: #339933;">=</span>
              splitPath.<span style="color: #006633;">equals</span><span style="color: #009900;">&#40;</span>key<span style="color: #009900;">&#41;</span> <span style="color: #339933;">||</span> splitPathWithNoSchema.<span style="color: #006633;">equals</span><span style="color: #009900;">&#40;</span>key<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">else</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #666666; font-style: italic;">// But for native tables, we need to do a prefix match for</span>
            <span style="color: #666666; font-style: italic;">// subdirectories.  (Unlike non-native tables, prefix mixups don't seem</span>
            <span style="color: #666666; font-style: italic;">// to be a potential problem here since we are always dealing with the</span>
            <span style="color: #666666; font-style: italic;">// path to something deeper than the table location.)</span>
            match <span style="color: #339933;">=</span>
              splitPath.<span style="color: #006633;">startsWith</span><span style="color: #009900;">&#40;</span>key<span style="color: #009900;">&#41;</span> <span style="color: #339933;">||</span> splitPathWithNoSchema.<span style="color: #006633;">startsWith</span><span style="color: #009900;">&#40;</span>key<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #009900;">&#125;</span>
          <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>match<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            ArrayList<span style="color: #339933;">&lt;</span>String<span style="color: #339933;">&gt;</span> list <span style="color: #339933;">=</span> entry.<span style="color: #006633;">getValue</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> val <span style="color: #339933;">:</span> list<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
              aliases.<span style="color: #006633;">add</span><span style="color: #009900;">&#40;</span>val<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
          <span style="color: #009900;">&#125;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> alias <span style="color: #339933;">:</span> aliases<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          Operator<span style="color: #339933;">&lt;?</span> <span style="color: #000000; font-weight: bold;">extends</span> OperatorDesc<span style="color: #339933;">&gt;</span> op <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">mrwork</span>.<span style="color: #006633;">getAliasToWork</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">get</span><span style="color: #009900;">&#40;</span>
            alias<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>op <span style="color: #000000; font-weight: bold;">instanceof</span> TableScanOperator<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            TableScanOperator ts <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span>TableScanOperator<span style="color: #009900;">&#41;</span> op<span style="color: #339933;">;</span>
            <span style="color: #666666; font-style: italic;">// push down projections.</span>
            ColumnProjectionUtils.<span style="color: #006633;">appendReadColumns</span><span style="color: #009900;">&#40;</span>
                jobConf, ts.<span style="color: #006633;">getNeededColumnIDs</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, ts.<span style="color: #006633;">getNeededColumns</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #666666; font-style: italic;">// push down filters</span>
            pushFilters<span style="color: #009900;">&#40;</span>jobConf, ts<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #009900;">&#125;</span>
        <span style="color: #009900;">&#125;</span>
      <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;"> protected void pushProjectionsAndFilters(JobConf jobConf, Class inputFormatClass,
          String splitPath, String splitPathWithNoSchema, boolean nonNative) {
        if (this.mrwork == null) {
          init(job);
        }
    
        if(this.mrwork.getPathToAliases() == null) {
          return;
        }
    
        ArrayList&lt;String&gt; aliases = new ArrayList&lt;String&gt;();
        Iterator&lt;Entry&lt;String, ArrayList&lt;String&gt;&gt;&gt; iterator = this.mrwork
            .getPathToAliases().entrySet().iterator();
    
        while (iterator.hasNext()) {
          Entry&lt;String, ArrayList&lt;String&gt;&gt; entry = iterator.next();
          String key = entry.getKey();
          boolean match;
          if (nonNative) {
            // For non-native tables, we need to do an exact match to avoid
            // HIVE-1903.  (The table location contains no files, and the string
            // representation of its path does not have a trailing slash.)
            match =
              splitPath.equals(key) || splitPathWithNoSchema.equals(key);
          } else {
            // But for native tables, we need to do a prefix match for
            // subdirectories.  (Unlike non-native tables, prefix mixups don't seem
            // to be a potential problem here since we are always dealing with the
            // path to something deeper than the table location.)
            match =
              splitPath.startsWith(key) || splitPathWithNoSchema.startsWith(key);
          }
          if (match) {
            ArrayList&lt;String&gt; list = entry.getValue();
            for (String val : list) {
              aliases.add(val);
            }
          }
        }
    
        for (String alias : aliases) {
          Operator&lt;? extends OperatorDesc&gt; op = this.mrwork.getAliasToWork().get(
            alias);
          if (op instanceof TableScanOperator) {
            TableScanOperator ts = (TableScanOperator) op;
            // push down projections.
            ColumnProjectionUtils.appendReadColumns(
                jobConf, ts.getNeededColumnIDs(), ts.getNeededColumns());
            // push down filters
            pushFilters(jobConf, ts);
          }
        }
      }</p></div>
    ";}
categories:
  - hadoop
tags:
  - parquet

---
一直好奇parquet和hive是怎样做列裁剪（跳过某些列）的，今天跟踪了一下代码。
parquet和hive交接的代码已经在合并在hive里面了，直接看hive的代码
<pre>input format在：org.apache.hadoop.hive.ql.io.parquet.MapredParquetInputFormat</pre>
## 数据准备

<pre lang="sql" escaped="true">CREATE TABLE parquet (x INT, y STRING) STORED AS PARQUET;
CREATE TABLE parquet2 (x INT, y STRING) STORED AS PARQUET;
CREATE TABLE test (x INT, y STRING) ROW FORMAT DELIMITED FIELDS TERMINATED BY '`';
-- 手工构造数据进test表
INSERT OVERWRITE TABLE parquet SELECT x,y FROM test;
INSERT OVERWRITE TABLE parquet2 SELECT x,y FROM test;</pre>
&nbsp;
## 测试语句

<pre escaped="true" lang="bash">SET mapred.job.tracker=local;
SET hive.exec.mode.local.auto=true;
SET fs.defaultFS=file:///; 
-- 避免转成mapjoin
SET hive.auto.convert.join=false; 
select a.x, b.y from parquet a left join parquet2 b on (a.x = b.x);</pre>
## 代码分析

maptask读取数据的时候，需要先获取一个reader  
MapTask(job.getInputFormat().getRecordReader)-> CombineHiveInputFormat.getRecordReader -> HiveInputFormat.pushFilters
<pre escaped="true" lang="java">public static void pushFilters(JobConf jobConf, TableScanOperator tableScan) {
    // construct column name list and types for reference by filter push down
    Utilities.setColumnNameList(jobConf, tableScan); // 在conf里设置columns
    Utilities.setColumnTypeList(jobConf, tableScan); // 在conf里设置columns.types
}</pre>
从this.mrwork.getPathToAliases里面拿到table alias，然后再从this.mrwork.getAliasToWork拿到TableScanOperator，  
ts.getNeededColumnIDs(), ts.getNeededColumns() 可以拿个这个表扫描需要的字段。
<pre escaped="true" lang="java">protected void pushProjectionsAndFilters(JobConf jobConf, Class inputFormatClass,
      String splitPath, String splitPathWithNoSchema, boolean nonNative) {
    if (this.mrwork == null) {
      init(job);
    }

    if(this.mrwork.getPathToAliases() == null) {
      return;
    }

    ArrayList&lt;String&gt; aliases = new ArrayList&lt;String&gt;();
    Iterator&lt;Entry&lt;String, ArrayList&lt;String&gt;&gt;&gt; iterator = this.mrwork
        .getPathToAliases().entrySet().iterator();

    while (iterator.hasNext()) {
      Entry&lt;String, ArrayList&lt;String&gt;&gt; entry = iterator.next();
      String key = entry.getKey();
      boolean match;
      if (nonNative) {
        // For non-native tables, we need to do an exact match to avoid
        // HIVE-1903.  (The table location contains no files, and the string
        // representation of its path does not have a trailing slash.)
        match =
          splitPath.equals(key) || splitPathWithNoSchema.equals(key);
      } else {
        // But for native tables, we need to do a prefix match for
        // subdirectories.  (Unlike non-native tables, prefix mixups don't seem
        // to be a potential problem here since we are always dealing with the
        // path to something deeper than the table location.)
        match =
          splitPath.startsWith(key) || splitPathWithNoSchema.startsWith(key);
      }
      if (match) {
        ArrayList&lt;String&gt; list = entry.getValue();
        for (String val : list) {
          aliases.add(val);
        }
      }
    }

    for (String alias : aliases) {
      Operator&lt;? extends OperatorDesc&gt; op = this.mrwork.getAliasToWork().get(
        alias);
      if (op instanceof TableScanOperator) {
        TableScanOperator ts = (TableScanOperator) op;
        // push down projections.
        ColumnProjectionUtils.appendReadColumns(
            jobConf, ts.getNeededColumnIDs(), ts.getNeededColumns());
        // push down filters
        pushFilters(jobConf, ts);
      }
    }
  }</pre>
注意这个方法:ColumnProjectionUtils.appendReadColumns，收集这个数据用到的字段。存储到的参数是  
hive.io.file.readcolumn.ids 记录需要获取的字段ID  
hive.io.file.readcolumn.names 记录需要获取的字段名称
在ParquetRecordReaderWrapper.getSplit里也有一个  
jobConf = projectionPusher.pushProjectionsAndFilters(conf, finalPath.getParent());
感觉和上面的HiveInputFormat的功能重叠，代码基本一样，可能为了兼容旧版本？不过重复添加也没有影响。
使用这个字段是在DataWritableReadSupport.init里面，从final String columns = configuration.get(IOConstants.COLUMNS);拿出所有字段，然后构造一个schema，然后结合上面的hive.io.file.readcolumn.ids，从而构造出新的schema
过滤条件的下放也是类似的情况。