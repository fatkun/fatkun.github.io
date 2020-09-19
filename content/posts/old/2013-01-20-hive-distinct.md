---
title: Hive – Distinct 的实现
author: fatkun
type: post
date: 2013-01-20T14:34:13+00:00
url: /2013/01/hive-distinct.html
duoshuo_thread_id:
  - 6300409441816675074
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:888:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;"><span style="color: #993333; font-weight: bold;">SELECT</span> <span style="color: #993333; font-weight: bold;">COUNT</span><span style="color: #66cc66;">,</span> <span style="color: #993333; font-weight: bold;">COUNT</span><span style="color: #66cc66;">&#40;</span><span style="color: #993333; font-weight: bold;">DISTINCT</span> uid<span style="color: #66cc66;">&#41;</span> <span style="color: #993333; font-weight: bold;">FROM</span> logs <span style="color: #993333; font-weight: bold;">GROUP</span> <span style="color: #993333; font-weight: bold;">BY</span> <span style="color: #993333; font-weight: bold;">COUNT</span>;</pre></td></tr></table><p class="theCode" style="display:none;">select count, count(distinct uid) from logs group by count;</p></div>
    ";i:2;s:1610:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;">hive<span style="color: #66cc66;">&gt;</span> <span style="color: #993333; font-weight: bold;">SELECT</span> <span style="color: #66cc66;">*</span> <span style="color: #993333; font-weight: bold;">FROM</span> logs;
    OK
    a	苹果	<span style="color: #cc66cc;">3</span>
    a	橙子	<span style="color: #cc66cc;">3</span>
    a	烧鸡	<span style="color: #cc66cc;">1</span>
    b	烧鸡	<span style="color: #cc66cc;">3</span>
    &nbsp;
    hive<span style="color: #66cc66;">&gt;</span> <span style="color: #993333; font-weight: bold;">SELECT</span> <span style="color: #993333; font-weight: bold;">COUNT</span><span style="color: #66cc66;">,</span> <span style="color: #993333; font-weight: bold;">COUNT</span><span style="color: #66cc66;">&#40;</span><span style="color: #993333; font-weight: bold;">DISTINCT</span> uid<span style="color: #66cc66;">&#41;</span> <span style="color: #993333; font-weight: bold;">FROM</span> logs <span style="color: #993333; font-weight: bold;">GROUP</span> <span style="color: #993333; font-weight: bold;">BY</span> <span style="color: #993333; font-weight: bold;">COUNT</span>;
    <span style="color: #cc66cc;">1</span>	<span style="color: #cc66cc;">1</span>
    <span style="color: #cc66cc;">3</span>	<span style="color: #cc66cc;">2</span></pre></td></tr></table><p class="theCode" style="display:none;">hive&gt; select * from logs;
    OK
    a	苹果	3
    a	橙子	3
    a	烧鸡	1
    b	烧鸡	3
    
    hive&gt; select count, count(distinct uid) from logs group by count;
    1	1
    3	2</p></div>
    ";i:3;s:12296:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">hive<span style="color: #339933;">&gt;</span> explain select count, count<span style="color: #009900;">&#40;</span>distinct uid<span style="color: #009900;">&#41;</span> from logs group by count<span style="color: #339933;">;</span>
    OK
    <span style="color: #000000; font-weight: bold;">ABSTRACT</span> SYNTAX TREE<span style="color: #339933;">:</span>
      <span style="color: #009900;">&#40;</span>TOK_QUERY <span style="color: #009900;">&#40;</span>TOK_FROM <span style="color: #009900;">&#40;</span>TOK_TABREF <span style="color: #009900;">&#40;</span>TOK_TABNAME logs<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#40;</span>TOK_INSERT <span style="color: #009900;">&#40;</span>TOK_DESTINATION <span style="color: #009900;">&#40;</span>TOK_DIR TOK_TMP_FILE<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#40;</span>TOK_SELECT <span style="color: #009900;">&#40;</span>TOK_SELEXPR <span style="color: #009900;">&#40;</span>TOK_TABLE_OR_COL count<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#40;</span>TOK_SELEXPR <span style="color: #009900;">&#40;</span>TOK_FUNCTIONDI count <span style="color: #009900;">&#40;</span>TOK_TABLE_OR_COL uid<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#40;</span>TOK_GROUPBY <span style="color: #009900;">&#40;</span>TOK_TABLE_OR_COL count<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span>
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
              TableScan <span style="color: #666666; font-style: italic;">//表扫描</span>
                alias<span style="color: #339933;">:</span> logs
                Select Operator<span style="color: #666666; font-style: italic;">//列裁剪，取出uid，count字段就够了</span>
                  expressions<span style="color: #339933;">:</span>
                        expr<span style="color: #339933;">:</span> count
                        type<span style="color: #339933;">:</span> <span style="color: #000066; font-weight: bold;">int</span>
                        expr<span style="color: #339933;">:</span> uid
                        type<span style="color: #339933;">:</span> string
                  outputColumnNames<span style="color: #339933;">:</span> count, uid
                  <span style="color: #003399;">Group</span> By Operator <span style="color: #666666; font-style: italic;">//先来map聚集</span>
                    aggregations<span style="color: #339933;">:</span>
                          expr<span style="color: #339933;">:</span> count<span style="color: #009900;">&#40;</span>DISTINCT uid<span style="color: #009900;">&#41;</span> <span style="color: #666666; font-style: italic;">//聚集表达式</span>
                    bucketGroup<span style="color: #339933;">:</span> <span style="color: #000066; font-weight: bold;">false</span>
                    keys<span style="color: #339933;">:</span>
                          expr<span style="color: #339933;">:</span> count
                          type<span style="color: #339933;">:</span> <span style="color: #000066; font-weight: bold;">int</span>
                          expr<span style="color: #339933;">:</span> uid
                          type<span style="color: #339933;">:</span> string
                    mode<span style="color: #339933;">:</span> hash <span style="color: #666666; font-style: italic;">//hash方式</span>
                    outputColumnNames<span style="color: #339933;">:</span> _col0, _col1, _col2
                    Reduce Output Operator
                      key expressions<span style="color: #339933;">:</span> <span style="color: #666666; font-style: italic;">//输出的键</span>
                            expr<span style="color: #339933;">:</span> _col0 <span style="color: #666666; font-style: italic;">//count</span>
                            type<span style="color: #339933;">:</span> <span style="color: #000066; font-weight: bold;">int</span>
                            expr<span style="color: #339933;">:</span> _col1 <span style="color: #666666; font-style: italic;">//uid</span>
                            type<span style="color: #339933;">:</span> string
                      sort order<span style="color: #339933;">:</span> <span style="color: #339933;">++</span>
                      Map<span style="color: #339933;">-</span>reduce partition columns<span style="color: #339933;">:</span> <span style="color: #666666; font-style: italic;">//这里是按group by的字段分区的</span>
                            expr<span style="color: #339933;">:</span> _col0 <span style="color: #666666; font-style: italic;">//这里表示count</span>
                            type<span style="color: #339933;">:</span> <span style="color: #000066; font-weight: bold;">int</span>
                      tag<span style="color: #339933;">:</span> <span style="color: #339933;">-</span><span style="color: #cc66cc;">1</span>
                      value expressions<span style="color: #339933;">:</span>
                            expr<span style="color: #339933;">:</span> _col2
                            type<span style="color: #339933;">:</span> bigint
          Reduce Operator Tree<span style="color: #339933;">:</span>
            <span style="color: #003399;">Group</span> By Operator <span style="color: #666666; font-style: italic;">//第二次聚集</span>
              aggregations<span style="color: #339933;">:</span>
                    expr<span style="color: #339933;">:</span> count<span style="color: #009900;">&#40;</span>DISTINCT KEY._col1<span style="color: #339933;">:</span><span style="color: #cc66cc;">0</span>._col0<span style="color: #009900;">&#41;</span> <span style="color: #666666; font-style: italic;">//uid:count</span>
              bucketGroup<span style="color: #339933;">:</span> <span style="color: #000066; font-weight: bold;">false</span>
              keys<span style="color: #339933;">:</span>
                    expr<span style="color: #339933;">:</span> KEY._col0 <span style="color: #666666; font-style: italic;">//count</span>
                    type<span style="color: #339933;">:</span> <span style="color: #000066; font-weight: bold;">int</span>
              mode<span style="color: #339933;">:</span> mergepartial <span style="color: #666666; font-style: italic;">//合并</span>
              outputColumnNames<span style="color: #339933;">:</span> _col0, _col1
              Select Operator <span style="color: #666666; font-style: italic;">//列裁剪</span>
                expressions<span style="color: #339933;">:</span>
                      expr<span style="color: #339933;">:</span> _col0
                      type<span style="color: #339933;">:</span> <span style="color: #000066; font-weight: bold;">int</span>
                      expr<span style="color: #339933;">:</span> _col1
                      type<span style="color: #339933;">:</span> bigint
                outputColumnNames<span style="color: #339933;">:</span> _col0, _col1
                <span style="color: #003399;">File</span> Output Operator <span style="color: #666666; font-style: italic;">//输出结果到文件</span>
                  compressed<span style="color: #339933;">:</span> <span style="color: #000066; font-weight: bold;">false</span>
                  GlobalTableId<span style="color: #339933;">:</span> <span style="color: #cc66cc;">0</span>
                  table<span style="color: #339933;">:</span>
                      input format<span style="color: #339933;">:</span> org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">hadoop</span>.<span style="color: #006633;">mapred</span>.<span style="color: #006633;">TextInputFormat</span>
                      output format<span style="color: #339933;">:</span> org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">hadoop</span>.<span style="color: #006633;">hive</span>.<span style="color: #006633;">ql</span>.<span style="color: #006633;">io</span>.<span style="color: #006633;">HiveIgnoreKeyTextOutputFormat</span>
    &nbsp;
      Stage<span style="color: #339933;">:</span> Stage<span style="color: #339933;">-</span><span style="color: #cc66cc;">0</span>
        Fetch Operator
          limit<span style="color: #339933;">:</span> <span style="color: #339933;">-</span><span style="color: #cc66cc;">1</span></pre></td></tr></table><p class="theCode" style="display:none;">hive&gt; explain select count, count(distinct uid) from logs group by count;
    OK
    ABSTRACT SYNTAX TREE:
      (TOK_QUERY (TOK_FROM (TOK_TABREF (TOK_TABNAME logs))) (TOK_INSERT (TOK_DESTINATION (TOK_DIR TOK_TMP_FILE)) (TOK_SELECT (TOK_SELEXPR (TOK_TABLE_OR_COL count)) (TOK_SELEXPR (TOK_FUNCTIONDI count (TOK_TABLE_OR_COL uid)))) (TOK_GROUPBY (TOK_TABLE_OR_COL count))))
    
    STAGE DEPENDENCIES:
      Stage-1 is a root stage
      Stage-0 is a root stage
    
    STAGE PLANS:
      Stage: Stage-1
        Map Reduce
          Alias -&gt; Map Operator Tree:
            logs 
              TableScan //表扫描
                alias: logs
                Select Operator//列裁剪，取出uid，count字段就够了
                  expressions:
                        expr: count
                        type: int
                        expr: uid
                        type: string
                  outputColumnNames: count, uid
                  Group By Operator //先来map聚集
                    aggregations:
                          expr: count(DISTINCT uid) //聚集表达式
                    bucketGroup: false
                    keys:
                          expr: count
                          type: int
                          expr: uid
                          type: string
                    mode: hash //hash方式
                    outputColumnNames: _col0, _col1, _col2
                    Reduce Output Operator
                      key expressions: //输出的键
                            expr: _col0 //count
                            type: int
                            expr: _col1 //uid
                            type: string
                      sort order: ++
                      Map-reduce partition columns: //这里是按group by的字段分区的
                            expr: _col0 //这里表示count
                            type: int
                      tag: -1
                      value expressions:
                            expr: _col2
                            type: bigint
          Reduce Operator Tree:
            Group By Operator //第二次聚集
              aggregations:
                    expr: count(DISTINCT KEY._col1:0._col0) //uid:count
              bucketGroup: false
              keys:
                    expr: KEY._col0 //count
                    type: int
              mode: mergepartial //合并
              outputColumnNames: _col0, _col1
              Select Operator //列裁剪
                expressions:
                      expr: _col0
                      type: int
                      expr: _col1
                      type: bigint
                outputColumnNames: _col0, _col1
                File Output Operator //输出结果到文件
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
  - distinct
  - hive

---
## 准备数据

语句
<pre escaped="true" lang="sql">select count, count(distinct uid) from logs group by count;</pre>
<pre escaped="true" lang="sql">hive&gt; select * from logs;
OK
a	苹果	3
a	橙子	3
a	烧鸡	1
b	烧鸡	3

hive&gt; select count, count(distinct uid) from logs group by count;
1	1
3	2</pre>
根据count分组，计算独立用户数。
## 计算过程

<a href="http://fatkun.com/2013/01/hive-distinct.html/hive-distinct-cal" rel="attachment wp-att-1324"><img src="http://fatkun.com/wp-content/uploads/hive-distinct-cal.jpg" alt="hive-distinct-cal" width="633" height="229" class="alignnone size-full wp-image-1324" srcset="http://fatkun.com/wp-content/uploads/hive-distinct-cal.jpg 633w, http://fatkun.com/wp-content/uploads/hive-distinct-cal-300x108.jpg 300w" sizes="(max-width: 633px) 100vw, 633px" /></a>
1. 第一步先在mapper计算部分值，会以count和uid作为key，如果是distinct并且之前已经出现过，则忽略这条计算。第一步是以<count, uid>组合为key，第二步是以count为key.  
2. ReduceSink是在mapper.close()时才执行的，在GroupByOperator.close()时，把结果输出。注意这里虽然key是count和uid，但是在reduce时分区是按count来的！  
3. 第一步的distinct计算的值没用，要留到reduce计算的才准确。这里只是减少了key组合相同的行。不过如果是普通的count，后面是会合并起来的。  
4. distinct通过比较lastInvoke判断要不要+1（因为在reduce是排序过了的，所以判断distict的字段变了没有，如果没变，则不+1）
## Operator

<a href="http://fatkun.com/2013/01/hive-distinct.html/hive-distinct-op" rel="attachment wp-att-1325"><img src="http://fatkun.com/wp-content/uploads/hive-distinct-op.png" alt="hive-distinct-op" width="347" height="467" class="alignnone size-full wp-image-1325" srcset="http://fatkun.com/wp-content/uploads/hive-distinct-op.png 347w, http://fatkun.com/wp-content/uploads/hive-distinct-op-222x300.png 222w" sizes="(max-width: 347px) 100vw, 347px" /></a>
## Explain

<pre escaped="true" lang="java">hive&gt; explain select count, count(distinct uid) from logs group by count;
OK
ABSTRACT SYNTAX TREE:
  (TOK_QUERY (TOK_FROM (TOK_TABREF (TOK_TABNAME logs))) (TOK_INSERT (TOK_DESTINATION (TOK_DIR TOK_TMP_FILE)) (TOK_SELECT (TOK_SELEXPR (TOK_TABLE_OR_COL count)) (TOK_SELEXPR (TOK_FUNCTIONDI count (TOK_TABLE_OR_COL uid)))) (TOK_GROUPBY (TOK_TABLE_OR_COL count))))

STAGE DEPENDENCIES:
  Stage-1 is a root stage
  Stage-0 is a root stage

STAGE PLANS:
  Stage: Stage-1
    Map Reduce
      Alias -&gt; Map Operator Tree:
        logs 
          TableScan //表扫描
            alias: logs
            Select Operator//列裁剪，取出uid，count字段就够了
              expressions:
                    expr: count
                    type: int
                    expr: uid
                    type: string
              outputColumnNames: count, uid
              Group By Operator //先来map聚集
                aggregations:
                      expr: count(DISTINCT uid) //聚集表达式
                bucketGroup: false
                keys:
                      expr: count
                      type: int
                      expr: uid
                      type: string
                mode: hash //hash方式
                outputColumnNames: _col0, _col1, _col2
                Reduce Output Operator
                  key expressions: //输出的键
                        expr: _col0 //count
                        type: int
                        expr: _col1 //uid
                        type: string
                  sort order: ++
                  Map-reduce partition columns: //这里是按group by的字段分区的
                        expr: _col0 //这里表示count
                        type: int
                  tag: -1
                  value expressions:
                        expr: _col2
                        type: bigint
      Reduce Operator Tree:
        Group By Operator //第二次聚集
          aggregations:
                expr: count(DISTINCT KEY._col1:0._col0) //uid:count
          bucketGroup: false
          keys:
                expr: KEY._col0 //count
                type: int
          mode: mergepartial //合并
          outputColumnNames: _col0, _col1
          Select Operator //列裁剪
            expressions:
                  expr: _col0
                  type: int
                  expr: _col1
                  type: bigint
            outputColumnNames: _col0, _col1
            File Output Operator //输出结果到文件
              compressed: false
              GlobalTableId: 0
              table:
                  input format: org.apache.hadoop.mapred.TextInputFormat
                  output format: org.apache.hadoop.hive.ql.io.HiveIgnoreKeyTextOutputFormat

  Stage: Stage-0
    Fetch Operator
      limit: -1
</pre>