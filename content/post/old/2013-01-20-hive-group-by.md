---
title: Hive – Group By 的实现
author: fatkun
type: post
date: 2013-01-20T14:53:23+00:00
url: /2013/01/hive-group-by.html
duoshuo_thread_id:
  - 6300409441887978242
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:750:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;"><span style="color: #993333; font-weight: bold;">SELECT</span> uid<span style="color: #66cc66;">,</span> <span style="color: #993333; font-weight: bold;">SUM</span><span style="color: #66cc66;">&#40;</span><span style="color: #993333; font-weight: bold;">COUNT</span><span style="color: #66cc66;">&#41;</span> <span style="color: #993333; font-weight: bold;">FROM</span> logs <span style="color: #993333; font-weight: bold;">GROUP</span> <span style="color: #993333; font-weight: bold;">BY</span> uid;</pre></td></tr></table><p class="theCode" style="display:none;">SELECT uid, sum(count) FROM logs group by uid;</p></div>
    ";i:2;s:1407:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;">hive<span style="color: #66cc66;">&gt;</span> <span style="color: #993333; font-weight: bold;">SELECT</span> <span style="color: #66cc66;">*</span> <span style="color: #993333; font-weight: bold;">FROM</span> logs;
    a	苹果	<span style="color: #cc66cc;">5</span>
    a	橙子	<span style="color: #cc66cc;">3</span>
    a      苹果   <span style="color: #cc66cc;">2</span>
    b	烧鸡	<span style="color: #cc66cc;">1</span>
    &nbsp;
    hive<span style="color: #66cc66;">&gt;</span> <span style="color: #993333; font-weight: bold;">SELECT</span> uid<span style="color: #66cc66;">,</span> <span style="color: #993333; font-weight: bold;">SUM</span><span style="color: #66cc66;">&#40;</span><span style="color: #993333; font-weight: bold;">COUNT</span><span style="color: #66cc66;">&#41;</span> <span style="color: #993333; font-weight: bold;">FROM</span> logs <span style="color: #993333; font-weight: bold;">GROUP</span> <span style="color: #993333; font-weight: bold;">BY</span> uid;
    a	<span style="color: #cc66cc;">10</span>
    b	<span style="color: #cc66cc;">1</span></pre></td></tr></table><p class="theCode" style="display:none;">hive&gt; select * from logs;
    a	苹果	5
    a	橙子	3
    a      苹果   2
    b	烧鸡	1
    
    hive&gt; SELECT uid, sum(count) FROM logs group by uid;
    a	10
    b	1</p></div>
    ";i:3;s:11168:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">hive<span style="color: #339933;">&gt;</span> explain SELECT uid, sum<span style="color: #009900;">&#40;</span>count<span style="color: #009900;">&#41;</span> FROM logs group by uid<span style="color: #339933;">;</span>
    OK
    <span style="color: #000000; font-weight: bold;">ABSTRACT</span> SYNTAX TREE<span style="color: #339933;">:</span>
      <span style="color: #009900;">&#40;</span>TOK_QUERY <span style="color: #009900;">&#40;</span>TOK_FROM <span style="color: #009900;">&#40;</span>TOK_TABREF <span style="color: #009900;">&#40;</span>TOK_TABNAME logs<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#40;</span>TOK_INSERT <span style="color: #009900;">&#40;</span>TOK_DESTINATION <span style="color: #009900;">&#40;</span>TOK_DIR TOK_TMP_FILE<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#40;</span>TOK_SELECT <span style="color: #009900;">&#40;</span>TOK_SELEXPR <span style="color: #009900;">&#40;</span>TOK_TABLE_OR_COL uid<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#40;</span>TOK_SELEXPR <span style="color: #009900;">&#40;</span>TOK_FUNCTION sum <span style="color: #009900;">&#40;</span>TOK_TABLE_OR_COL count<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#40;</span>TOK_GROUPBY <span style="color: #009900;">&#40;</span>TOK_TABLE_OR_COL uid<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span>
    &nbsp;
    STAGE DEPENDENCIES<span style="color: #339933;">:</span>
      Stage<span style="color: #339933;">-</span><span style="color: #cc66cc;">1</span> is a root stage
      Stage<span style="color: #339933;">-</span><span style="color: #cc66cc;">0</span> is a root stage
    &nbsp;
    STAGE PLANS<span style="color: #339933;">:</span>
      Stage<span style="color: #339933;">:</span> Stage<span style="color: #339933;">-</span><span style="color: #cc66cc;">1</span>
        <span style="color: #003399;">Map</span> Reduce
          Alias <span style="color: #339933;">-&gt;</span> <span style="color: #003399;">Map</span> Operator Tree<span style="color: #339933;">:</span>
            logs 
              TableScan <span style="color: #666666; font-style: italic;">// 扫描表</span>
                alias<span style="color: #339933;">:</span> logs
                Select Operator <span style="color: #666666; font-style: italic;">//选择字段</span>
                  expressions<span style="color: #339933;">:</span>
                        expr<span style="color: #339933;">:</span> uid
                        type<span style="color: #339933;">:</span> string
                        expr<span style="color: #339933;">:</span> count
                        type<span style="color: #339933;">:</span> <span style="color: #000066; font-weight: bold;">int</span>
                  outputColumnNames<span style="color: #339933;">:</span> uid, count
                  <span style="color: #003399;">Group</span> By Operator <span style="color: #666666; font-style: italic;">//这里是因为默认设置了hive.map.aggr=true，会在mapper先做一次聚合，减少reduce需要处理的数据</span>
                    aggregations<span style="color: #339933;">:</span>
                          expr<span style="color: #339933;">:</span> sum<span style="color: #009900;">&#40;</span>count<span style="color: #009900;">&#41;</span> <span style="color: #666666; font-style: italic;">//聚集函数</span>
                    bucketGroup<span style="color: #339933;">:</span> <span style="color: #000066; font-weight: bold;">false</span>
                    keys<span style="color: #339933;">:</span> <span style="color: #666666; font-style: italic;">//键</span>
                          expr<span style="color: #339933;">:</span> uid
                          type<span style="color: #339933;">:</span> string
                    mode<span style="color: #339933;">:</span> hash <span style="color: #666666; font-style: italic;">//hash方式，processHashAggr()</span>
                    outputColumnNames<span style="color: #339933;">:</span> _col0, _col1
                    Reduce Output Operator <span style="color: #666666; font-style: italic;">//输出key，value给reducer</span>
                      key expressions<span style="color: #339933;">:</span>
                            expr<span style="color: #339933;">:</span> _col0
                            type<span style="color: #339933;">:</span> string
                      sort order<span style="color: #339933;">:</span> <span style="color: #339933;">+</span>
                      Map<span style="color: #339933;">-</span>reduce partition columns<span style="color: #339933;">:</span>
                            expr<span style="color: #339933;">:</span> _col0
                            type<span style="color: #339933;">:</span> string
                      tag<span style="color: #339933;">:</span> <span style="color: #339933;">-</span><span style="color: #cc66cc;">1</span>
                      value expressions<span style="color: #339933;">:</span>
                            expr<span style="color: #339933;">:</span> _col1
                            type<span style="color: #339933;">:</span> bigint
          Reduce Operator Tree<span style="color: #339933;">:</span>
            <span style="color: #003399;">Group</span> By Operator
    &nbsp;
              aggregations<span style="color: #339933;">:</span>
                    expr<span style="color: #339933;">:</span> sum<span style="color: #009900;">&#40;</span>VALUE._col0<span style="color: #009900;">&#41;</span>
    <span style="color: #666666; font-style: italic;">//聚合</span>
              bucketGroup<span style="color: #339933;">:</span> <span style="color: #000066; font-weight: bold;">false</span>
              keys<span style="color: #339933;">:</span>
                    expr<span style="color: #339933;">:</span> KEY._col0
                    type<span style="color: #339933;">:</span> string
              mode<span style="color: #339933;">:</span> mergepartial <span style="color: #666666; font-style: italic;">//合并值</span>
              outputColumnNames<span style="color: #339933;">:</span> _col0, _col1
              Select Operator <span style="color: #666666; font-style: italic;">//选择字段</span>
                expressions<span style="color: #339933;">:</span>
                      expr<span style="color: #339933;">:</span> _col0
                      type<span style="color: #339933;">:</span> string
                      expr<span style="color: #339933;">:</span> _col1
                      type<span style="color: #339933;">:</span> bigint
                outputColumnNames<span style="color: #339933;">:</span> _col0, _col1
                <span style="color: #003399;">File</span> Output Operator <span style="color: #666666; font-style: italic;">//输出到文件</span>
                  compressed<span style="color: #339933;">:</span> <span style="color: #000066; font-weight: bold;">false</span>
                  GlobalTableId<span style="color: #339933;">:</span> <span style="color: #cc66cc;">0</span>
                  table<span style="color: #339933;">:</span>
                      input format<span style="color: #339933;">:</span> org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">hadoop</span>.<span style="color: #006633;">mapred</span>.<span style="color: #006633;">TextInputFormat</span>
                      output format<span style="color: #339933;">:</span> org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">hadoop</span>.<span style="color: #006633;">hive</span>.<span style="color: #006633;">ql</span>.<span style="color: #006633;">io</span>.<span style="color: #006633;">HiveIgnoreKeyTextOutputFormat</span>
    &nbsp;
      Stage<span style="color: #339933;">:</span> Stage<span style="color: #339933;">-</span><span style="color: #cc66cc;">0</span>
        Fetch Operator
          limit<span style="color: #339933;">:</span> <span style="color: #339933;">-</span><span style="color: #cc66cc;">1</span></pre></td></tr></table><p class="theCode" style="display:none;">hive&gt; explain SELECT uid, sum(count) FROM logs group by uid;
    OK
    ABSTRACT SYNTAX TREE:
      (TOK_QUERY (TOK_FROM (TOK_TABREF (TOK_TABNAME logs))) (TOK_INSERT (TOK_DESTINATION (TOK_DIR TOK_TMP_FILE)) (TOK_SELECT (TOK_SELEXPR (TOK_TABLE_OR_COL uid)) (TOK_SELEXPR (TOK_FUNCTION sum (TOK_TABLE_OR_COL count)))) (TOK_GROUPBY (TOK_TABLE_OR_COL uid))))
    
    STAGE DEPENDENCIES:
      Stage-1 is a root stage
      Stage-0 is a root stage
    
    STAGE PLANS:
      Stage: Stage-1
        Map Reduce
          Alias -&gt; Map Operator Tree:
            logs 
              TableScan // 扫描表
                alias: logs
                Select Operator //选择字段
                  expressions:
                        expr: uid
                        type: string
                        expr: count
                        type: int
                  outputColumnNames: uid, count
                  Group By Operator //这里是因为默认设置了hive.map.aggr=true，会在mapper先做一次聚合，减少reduce需要处理的数据
                    aggregations:
                          expr: sum(count) //聚集函数
                    bucketGroup: false
                    keys: //键
                          expr: uid
                          type: string
                    mode: hash //hash方式，processHashAggr()
                    outputColumnNames: _col0, _col1
                    Reduce Output Operator //输出key，value给reducer
                      key expressions:
                            expr: _col0
                            type: string
                      sort order: +
                      Map-reduce partition columns:
                            expr: _col0
                            type: string
                      tag: -1
                      value expressions:
                            expr: _col1
                            type: bigint
          Reduce Operator Tree:
            Group By Operator
     
              aggregations:
                    expr: sum(VALUE._col0)
    //聚合
              bucketGroup: false
              keys:
                    expr: KEY._col0
                    type: string
              mode: mergepartial //合并值
              outputColumnNames: _col0, _col1
              Select Operator //选择字段
                expressions:
                      expr: _col0
                      type: string
                      expr: _col1
                      type: bigint
                outputColumnNames: _col0, _col1
                File Output Operator //输出到文件
                  compressed: false
                  GlobalTableId: 0
                  table:
                      input format: org.apache.hadoop.mapred.TextInputFormat
                      output format: org.apache.hadoop.hive.ql.io.HiveIgnoreKeyTextOutputFormat
    
      Stage: Stage-0
        Fetch Operator
          limit: -1</p></div>
    ";}
categories:
  - hive
tags:
  - group by
  - hive
  - mapreduce
  - 计算过程

---
## 准备数据

<pre escaped="true" lang="sql">SELECT uid, sum(count) FROM logs group by uid;</pre>
<pre escaped="true" lang="sql">hive&gt; select * from logs;
a	苹果	5
a	橙子	3
a      苹果   2
b	烧鸡	1

hive&gt; SELECT uid, sum(count) FROM logs group by uid;
a	10
b	1</pre>
## 计算过程

<a href="http://fatkun.com/2013/01/hive-group-by.html/hive-groupby-cal" rel="attachment wp-att-1333"><img src="http://fatkun.com/wp-content/uploads/hive-groupby-cal.jpg" alt="hive-groupby-cal" width="643" height="227" class="alignnone size-full wp-image-1333" srcset="http://fatkun.com/wp-content/uploads/hive-groupby-cal.jpg 643w, http://fatkun.com/wp-content/uploads/hive-groupby-cal-300x105.jpg 300w" sizes="(max-width: 643px) 100vw, 643px" /></a>  
默认设置了hive.map.aggr=true，所以会在mapper端先group by一次，最后再把结果merge起来，为了减少reducer处理的数据量。注意看explain的mode是不一样的。mapper是hash，reducer是mergepartial。如果把hive.map.aggr=false，那将groupby放到reducer才做，他的mode是complete.
## Operator

<a href="http://fatkun.com/2013/01/hive-group-by.html/hive-groupby-op" rel="attachment wp-att-1334"><img src="http://fatkun.com/wp-content/uploads/hive-groupby-op.png" alt="hive-groupby-op" width="439" height="555" class="alignnone size-full wp-image-1334" srcset="http://fatkun.com/wp-content/uploads/hive-groupby-op.png 439w, http://fatkun.com/wp-content/uploads/hive-groupby-op-237x300.png 237w" sizes="(max-width: 439px) 100vw, 439px" /></a>
## Explain

<pre escaped="true" lang="java">hive&gt; explain SELECT uid, sum(count) FROM logs group by uid;
OK
ABSTRACT SYNTAX TREE:
  (TOK_QUERY (TOK_FROM (TOK_TABREF (TOK_TABNAME logs))) (TOK_INSERT (TOK_DESTINATION (TOK_DIR TOK_TMP_FILE)) (TOK_SELECT (TOK_SELEXPR (TOK_TABLE_OR_COL uid)) (TOK_SELEXPR (TOK_FUNCTION sum (TOK_TABLE_OR_COL count)))) (TOK_GROUPBY (TOK_TABLE_OR_COL uid))))

STAGE DEPENDENCIES:
  Stage-1 is a root stage
  Stage-0 is a root stage

STAGE PLANS:
  Stage: Stage-1
    Map Reduce
      Alias -&gt; Map Operator Tree:
        logs 
          TableScan // 扫描表
            alias: logs
            Select Operator //选择字段
              expressions:
                    expr: uid
                    type: string
                    expr: count
                    type: int
              outputColumnNames: uid, count
              Group By Operator //这里是因为默认设置了hive.map.aggr=true，会在mapper先做一次聚合，减少reduce需要处理的数据
                aggregations:
                      expr: sum(count) //聚集函数
                bucketGroup: false
                keys: //键
                      expr: uid
                      type: string
                mode: hash //hash方式，processHashAggr()
                outputColumnNames: _col0, _col1
                Reduce Output Operator //输出key，value给reducer
                  key expressions:
                        expr: _col0
                        type: string
                  sort order: +
                  Map-reduce partition columns:
                        expr: _col0
                        type: string
                  tag: -1
                  value expressions:
                        expr: _col1
                        type: bigint
      Reduce Operator Tree:
        Group By Operator
 
          aggregations:
                expr: sum(VALUE._col0)
//聚合
          bucketGroup: false
          keys:
                expr: KEY._col0
                type: string
          mode: mergepartial //合并值
          outputColumnNames: _col0, _col1
          Select Operator //选择字段
            expressions:
                  expr: _col0
                  type: string
                  expr: _col1
                  type: bigint
            outputColumnNames: _col0, _col1
            File Output Operator //输出到文件
              compressed: false
              GlobalTableId: 0
              table:
                  input format: org.apache.hadoop.mapred.TextInputFormat
                  output format: org.apache.hadoop.hive.ql.io.HiveIgnoreKeyTextOutputFormat

  Stage: Stage-0
    Fetch Operator
      limit: -1
</pre>