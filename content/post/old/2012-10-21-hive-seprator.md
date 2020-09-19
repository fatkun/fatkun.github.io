---
title: Hive内容包含有\001会当成分割符
author: fatkun
type: post
date: 2012-10-21T14:45:54+00:00
url: /2012/10/hive-seprator.html
duoshuo_thread_id:
  - 6300409441405633281
wp-syntax-cache-content:
  - |
    a:5:{i:1;s:1948:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;"># 建表语句
    <span style="color: #993333; font-weight: bold;">CREATE</span> <span style="color: #993333; font-weight: bold;">TABLE</span> test <span style="color: #66cc66;">&#40;</span> sn string<span style="color: #66cc66;">,</span> pv <span style="color: #993333; font-weight: bold;">INT</span><span style="color: #66cc66;">&#41;</span> <span style="color: #993333; font-weight: bold;">ROW</span> FORMAT DELIMITED <span style="color: #993333; font-weight: bold;">FIELDS</span> <span style="color: #993333; font-weight: bold;">TERMINATED</span> <span style="color: #993333; font-weight: bold;">BY</span> <span style="color: #ff0000;">'`'</span>;
    # 在另一个窗口构造一个错误数据文件
    printf <span style="color: #ff0000;">&quot;a<span style="color: #000099; font-weight: bold;">\0</span>01`12&quot;</span> <span style="color: #66cc66;">&gt;</span> <span style="color: #66cc66;">/</span>tmp<span style="color: #66cc66;">/</span>test<span style="color: #66cc66;">.</span>txt
    # 把数据<span style="color: #993333; font-weight: bold;">LOAD</span>进表里
    <span style="color: #993333; font-weight: bold;">LOAD</span> <span style="color: #993333; font-weight: bold;">DATA</span> <span style="color: #993333; font-weight: bold;">LOCAL</span> INPATH <span style="color: #ff0000;">'/tmp/test.txt'</span> OVERWRITE <span style="color: #993333; font-weight: bold;">INTO</span> <span style="color: #993333; font-weight: bold;">TABLE</span> test;</pre></td></tr></table><p class="theCode" style="display:none;"># 建表语句
    create table test ( sn string, pv int) ROW FORMAT DELIMITED FIELDS TERMINATED BY '`';
    # 在另一个窗口构造一个错误数据文件
    printf &quot;a\001`12&quot; &gt; /tmp/test.txt
    # 把数据load进表里
    LOAD DATA LOCAL INPATH '/tmp/test.txt' OVERWRITE INTO TABLE test;</p></div>
    ";i:2;s:398:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;"><span style="color: #993333; font-weight: bold;">SELECT</span> sn<span style="color: #66cc66;">,</span>pv <span style="color: #993333; font-weight: bold;">FROM</span> test;</pre></td></tr></table><p class="theCode" style="display:none;">select sn,pv from test;</p></div>
    ";i:3;s:1558:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #666666; font-style: italic;">//FileSinkOperator.java文件</span>
      @Override
      <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> processOp<span style="color: #009900;">&#40;</span><span style="color: #003399;">Object</span> row, <span style="color: #000066; font-weight: bold;">int</span> tag<span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">throws</span> HiveException <span style="color: #009900;">&#123;</span>
    ...
            <span style="color: #666666; font-style: italic;">// use SerDe to serialize r, and write it out</span>
            recordValue <span style="color: #339933;">=</span> serializer.<span style="color: #006633;">serialize</span><span style="color: #009900;">&#40;</span>row, inputObjInspectors<span style="color: #009900;">&#91;</span><span style="color: #cc66cc;">0</span><span style="color: #009900;">&#93;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    ...
      <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">//FileSinkOperator.java文件
      @Override
      public void processOp(Object row, int tag) throws HiveException {
    ...
            // use SerDe to serialize r, and write it out
            recordValue = serializer.serialize(row, inputObjInspectors[0]);
    ...
      }</p></div>
    ";i:4;s:1620:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #666666; font-style: italic;">//FileSinkOperator.java文件</span>
          serializer       <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span>Serializer<span style="color: #009900;">&#41;</span> conf.<span style="color: #006633;">getTableInfo</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getDeserializerClass</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">newInstance</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          serializer.<span style="color: #006633;">initialize</span><span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">null</span>, conf.<span style="color: #006633;">getTableInfo</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getProperties</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span></pre></td></tr></table><p class="theCode" style="display:none;">//FileSinkOperator.java文件
          serializer       = (Serializer) conf.getTableInfo().getDeserializerClass().newInstance();
          serializer.initialize(null, conf.getTableInfo().getProperties());</p></div>
    ";i:5;s:4418:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #666666; font-style: italic;">// SemanticAnalyzer.java</span>
      <span style="color: #000000; font-weight: bold;">private</span> Operator genFileSinkPlan<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> dest, QB qb, Operator input<span style="color: #009900;">&#41;</span>
          <span style="color: #000000; font-weight: bold;">throws</span> SemanticException <span style="color: #009900;">&#123;</span>
    ...
    <span style="color: #006633;">CreateTableDesc</span> tblDesc <span style="color: #339933;">=</span> qb.<span style="color: #006633;">getTableDesc</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">//到qb里面找</span>
    ...
    &nbsp;
          <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>tblDesc <span style="color: #339933;">==</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>qb.<span style="color: #006633;">getIsQuery</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
              <span style="color: #003399;">String</span> fileFormat <span style="color: #339933;">=</span> HiveConf.<span style="color: #006633;">getVar</span><span style="color: #009900;">&#40;</span>conf, HiveConf.<span style="color: #006633;">ConfVars</span>.<span style="color: #006633;">HIVEQUERYRESULTFILEFORMAT</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
              table_desc <span style="color: #339933;">=</span> PlanUtils.<span style="color: #006633;">getDefaultQueryOutputTableDesc</span><span style="color: #009900;">&#40;</span>cols, colTypes, fileFormat<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">else</span> <span style="color: #009900;">&#123;</span>
              table_desc <span style="color: #339933;">=</span> PlanUtils.<span style="color: #006633;">getDefaultTableDesc</span><span style="color: #009900;">&#40;</span><span style="color: #003399;">Integer</span>
                  .<span style="color: #006633;">toString</span><span style="color: #009900;">&#40;</span><span style="color: #003399;">Utilities</span>.<span style="color: #006633;">ctrlaCode</span><span style="color: #009900;">&#41;</span>, cols, colTypes, <span style="color: #000066; font-weight: bold;">false</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
          <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">else</span> <span style="color: #009900;">&#123;</span>
            table_desc <span style="color: #339933;">=</span> PlanUtils.<span style="color: #006633;">getTableDesc</span><span style="color: #009900;">&#40;</span>tblDesc, cols, colTypes<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #009900;">&#125;</span>
    &nbsp;
    ...
     <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">// SemanticAnalyzer.java
      private Operator genFileSinkPlan(String dest, QB qb, Operator input)
          throws SemanticException {
    ...
    CreateTableDesc tblDesc = qb.getTableDesc(); //到qb里面找
    ...
    
          if (tblDesc == null) {
            if (qb.getIsQuery()) {
              String fileFormat = HiveConf.getVar(conf, HiveConf.ConfVars.HIVEQUERYRESULTFILEFORMAT);
              table_desc = PlanUtils.getDefaultQueryOutputTableDesc(cols, colTypes, fileFormat);
            } else {
              table_desc = PlanUtils.getDefaultTableDesc(Integer
                  .toString(Utilities.ctrlaCode), cols, colTypes, false);
            }
          } else {
            table_desc = PlanUtils.getTableDesc(tblDesc, cols, colTypes);
          }
    
    ...
     }</p></div>
    ";}
categories:
  - hive
tags:
  - hive
  - seprator
  - 分割符

---
## 起因

发现某一行一列数据多了一个\001字符，导致select的时候在这一列后面的结果都不正确。
## 重现

hive版本：0.7.1cdh3u4
<pre lang="sql" escaped="true"># 建表语句
create table test ( sn string, pv int) ROW FORMAT DELIMITED FIELDS TERMINATED BY '`';
# 在另一个窗口构造一个错误数据文件
printf "a\001`12" &gt; /tmp/test.txt
# 把数据load进表里
LOAD DATA LOCAL INPATH '/tmp/test.txt' OVERWRITE INTO TABLE test;</pre>
这里指定了字段的分割符为反引号（\`），后来发现中途并不是全部用这个分割字段。  
这时如果查询
<pre lang="sql" escaped="true">select sn,pv from test;</pre>
返回的值居然是a NULL，而不是 a 12
## 原因

这条语句（select sn,pv from test;）会有三个Opertor，分别是TableScanOperator, SelectOperator, FileSinkOperator。FileSinkOperator是负责把结果输出到文件，输出前需要把对象做一次序列化存储到文件里。
<pre escaped="true" lang="java">//FileSinkOperator.java文件
  @Override
  public void processOp(Object row, int tag) throws HiveException {
...
        // use SerDe to serialize r, and write it out
        recordValue = serializer.serialize(row, inputObjInspectors[0]);
...
  }</pre>
这里的row是由它的父Operator（SelectOperator）传入的，值是一个数组，暂且用row = [a\001, 12]表示(实际上这里面还包裹一些对象，但不妨碍分析)。  
单步跟进后，发现recordValue返回的值是a\001\00112，这里的serializer用的分割符号是\001，所以现在变成了两个\001。  
那么，这个serializer哪里来的？
<pre escaped="true" lang="java">//FileSinkOperator.java文件
      serializer       = (Serializer) conf.getTableInfo().getDeserializerClass().newInstance();
      serializer.initialize(null, conf.getTableInfo().getProperties());</pre>
conf.getTableInfo()返回的是一个TableDesc，这个是在编译阶段genFileSinkPlan()构造的。
<pre escaped="true" lang="java">// SemanticAnalyzer.java
  private Operator genFileSinkPlan(String dest, QB qb, Operator input)
      throws SemanticException {
...
CreateTableDesc tblDesc = qb.getTableDesc(); //到qb里面找
...

      if (tblDesc == null) {
        if (qb.getIsQuery()) {
          String fileFormat = HiveConf.getVar(conf, HiveConf.ConfVars.HIVEQUERYRESULTFILEFORMAT);
          table_desc = PlanUtils.getDefaultQueryOutputTableDesc(cols, colTypes, fileFormat);
        } else {
          table_desc = PlanUtils.getDefaultTableDesc(Integer
              .toString(Utilities.ctrlaCode), cols, colTypes, false);
        }
      } else {
        table_desc = PlanUtils.getTableDesc(tblDesc, cols, colTypes);
      }

...
 }</pre>
发现在SemanticAnalyzer.java文件里，只有在CTAS的语句才会调用qb.setTableDesc()，所以这里tblDesc没有值，它自己用默认值创建了一个。PlanUtils.getDefaultQueryOutputTableDesc(cols, colTypes, fileFormat);分割符是Utilities.ctrlaCode，也就是\001
目前还没搞明白为什么分割符这么混乱。但可以知道为什么第二列本来应该返回数字却返回了null，是这里的分割符号是\001，那么就多了一列出来。
## 结论

就算你指定了分割符（FIELDS TERMINATED BY），但hive在中间交换数据时仍然使用它默认的分割符号\001-\009，暂时只想到在数据中过滤这些字符了，还不了解hive的序列化\反序列化。