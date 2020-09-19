---
title: Hive的Lateral View
author: fatkun
type: post
date: 2013-06-11T18:10:14+00:00
url: /2013/06/hive的lateral-view.html
duoshuo_thread_id:
  - 6300410024170619650
wp-syntax-cache-content:
  - |
    a:6:{i:1;s:1256:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;"><span style="color: #993333; font-weight: bold;">CREATE</span> <span style="color: #993333; font-weight: bold;">TABLE</span> test_array <span style="color: #66cc66;">&#40;</span>a array<span style="color: #66cc66;">&lt;</span>int<span style="color: #66cc66;">&gt;,</span> b array<span style="color: #66cc66;">&lt;</span>string<span style="color: #66cc66;">&gt;</span><span style="color: #66cc66;">&#41;</span>
    <span style="color: #993333; font-weight: bold;">ROW</span> FORMAT DELIMITED
    <span style="color: #993333; font-weight: bold;">FIELDS</span> <span style="color: #993333; font-weight: bold;">TERMINATED</span> <span style="color: #993333; font-weight: bold;">BY</span> <span style="color: #ff0000;">'`'</span>
    COLLECTION ITEMS <span style="color: #993333; font-weight: bold;">TERMINATED</span> <span style="color: #993333; font-weight: bold;">BY</span> <span style="color: #ff0000;">','</span>;</pre></td></tr></table><p class="theCode" style="display:none;">create table test_array (a array&lt;int&gt;, b array&lt;string&gt;)
    ROW FORMAT DELIMITED
    FIELDS TERMINATED BY '`'
    COLLECTION ITEMS TERMINATED BY ',';</p></div>
    ";i:2;s:447:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;"><span style="color: #cc66cc;">10</span><span style="color: #66cc66;">,</span><span style="color: #cc66cc;">11</span><span style="color: #ff0000;">`tom,mary
    20,21`</span>kate<span style="color: #66cc66;">,</span>tim</pre></td></tr></table><p class="theCode" style="display:none;">10,11`tom,mary
    20,21`kate,tim</p></div>
    ";i:3;s:654:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;"><span style="color: #993333; font-weight: bold;">LOAD</span> <span style="color: #993333; font-weight: bold;">DATA</span> <span style="color: #993333; font-weight: bold;">LOCAL</span> inpath <span style="color: #ff0000;">'/tmp/test'</span> overwrite <span style="color: #993333; font-weight: bold;">INTO</span> <span style="color: #993333; font-weight: bold;">TABLE</span> test_array;</pre></td></tr></table><p class="theCode" style="display:none;">load data local inpath '/tmp/test' overwrite into table test_array;</p></div>
    ";i:4;s:1336:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;">hive<span style="color: #66cc66;">&gt;</span> <span style="color: #993333; font-weight: bold;">SELECT</span> explode<span style="color: #66cc66;">&#40;</span>b<span style="color: #66cc66;">&#41;</span> <span style="color: #993333; font-weight: bold;">AS</span> name<span style="color: #66cc66;">,</span> a <span style="color: #993333; font-weight: bold;">FROM</span> test_array;
    FAILED: SemanticException <span style="color: #cc66cc;">1</span>:<span style="color: #cc66cc;">27</span> <span style="color: #993333; font-weight: bold;">ONLY</span> a single expression <span style="color: #993333; font-weight: bold;">IN</span> the <span style="color: #993333; font-weight: bold;">SELECT</span> clause <span style="color: #993333; font-weight: bold;">IS</span> supported <span style="color: #993333; font-weight: bold;">WITH</span> UDTF<span style="color: #ff0000;">'s. Error encountered near token '</span>a<span style="color: #ff0000;">'</span></pre></td></tr></table><p class="theCode" style="display:none;">hive&gt; select explode(b) as name, a from test_array;
    FAILED: SemanticException 1:27 Only a single expression in the SELECT clause is supported with UDTF's. Error encountered near token 'a'</p></div>
    ";i:5;s:1609:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;">hive<span style="color: #66cc66;">&gt;</span> <span style="color: #993333; font-weight: bold;">SELECT</span> a<span style="color: #66cc66;">,</span> name <span style="color: #993333; font-weight: bold;">FROM</span> test_array LATERAL <span style="color: #993333; font-weight: bold;">VIEW</span> explode<span style="color: #66cc66;">&#40;</span>b<span style="color: #66cc66;">&#41;</span> r1 <span style="color: #993333; font-weight: bold;">AS</span> name;
    <span style="color: #66cc66;">&#91;</span><span style="color: #cc66cc;">10</span><span style="color: #66cc66;">,</span><span style="color: #cc66cc;">11</span><span style="color: #66cc66;">&#93;</span>	tom
    <span style="color: #66cc66;">&#91;</span><span style="color: #cc66cc;">10</span><span style="color: #66cc66;">,</span><span style="color: #cc66cc;">11</span><span style="color: #66cc66;">&#93;</span>	mary
    <span style="color: #66cc66;">&#91;</span><span style="color: #cc66cc;">20</span><span style="color: #66cc66;">,</span><span style="color: #cc66cc;">21</span><span style="color: #66cc66;">&#93;</span>	kate
    <span style="color: #66cc66;">&#91;</span><span style="color: #cc66cc;">20</span><span style="color: #66cc66;">,</span><span style="color: #cc66cc;">21</span><span style="color: #66cc66;">&#93;</span>	tim</pre></td></tr></table><p class="theCode" style="display:none;">hive&gt; SELECT a, name FROM test_array LATERAL VIEW explode(b) r1 AS name;
    [10,11]	tom
    [10,11]	mary
    [20,21]	kate
    [20,21]	tim</p></div>
    ";i:6;s:1419:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;">hive<span style="color: #66cc66;">&gt;</span> <span style="color: #993333; font-weight: bold;">SELECT</span> id<span style="color: #66cc66;">,</span> name <span style="color: #993333; font-weight: bold;">FROM</span> test_array LATERAL <span style="color: #993333; font-weight: bold;">VIEW</span> explode<span style="color: #66cc66;">&#40;</span>b<span style="color: #66cc66;">&#41;</span> r1 <span style="color: #993333; font-weight: bold;">AS</span> name LATERAL <span style="color: #993333; font-weight: bold;">VIEW</span> explode<span style="color: #66cc66;">&#40;</span>A<span style="color: #66cc66;">&#41;</span> r2 <span style="color: #993333; font-weight: bold;">AS</span> id;
    <span style="color: #cc66cc;">10</span>	tom
    <span style="color: #cc66cc;">11</span>	tom
    <span style="color: #cc66cc;">10</span>	mary
    <span style="color: #cc66cc;">11</span>	mary
    <span style="color: #cc66cc;">20</span>	kate
    <span style="color: #cc66cc;">21</span>	kate
    <span style="color: #cc66cc;">20</span>	tim
    <span style="color: #cc66cc;">21</span>	tim</pre></td></tr></table><p class="theCode" style="display:none;">hive&gt; SELECT id, name FROM test_array LATERAL VIEW explode(b) r1 AS name LATERAL VIEW explode(A) r2 AS id;
    10	tom
    11	tom
    10	mary
    11	mary
    20	kate
    21	kate
    20	tim
    21	tim</p></div>
    ";}
categories:
  - 未分类
tags:
  - hive
  - Lateral View

---
Lateral View用于把UDTF的行转列结果集合在一起提供服务。Lateral View可以返回多列数据，前提是UDTF注册的输出个数。
UDTF代码参考：hive/src/ql/src/java/org/apache/hadoop/hive/ql/udf/generic/GenericUDTFExplode.java
## 准备数据

<pre escaped="true" lang="sql">create table test_array (a array&lt;int>, b array&lt;string>)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY '`'
COLLECTION ITEMS TERMINATED BY ',';</pre>
测试数据，保存文件为/tmp/test
<pre escaped="true" lang="sql">10,11`tom,mary
20,21`kate,tim
</pre>
导入数据
<pre escaped="true" lang="sql">load data local inpath '/tmp/test' overwrite into table test_array;</pre>
## 测试

<pre escaped="true" lang="sql">hive&gt; select explode(b) as name, a from test_array;
FAILED: SemanticException 1:27 Only a single expression in the SELECT clause is supported with UDTF's. Error encountered near token 'a'
</pre>
UDTF只能select单列
使用LATERAL VIEW
<pre escaped="true" lang="sql">hive&gt; SELECT a, name FROM test_array LATERAL VIEW explode(b) r1 AS name;
[10,11]	tom
[10,11]	mary
[20,21]	kate
[20,21]	tim
</pre>
可以有多个lateral view
<pre escaped="true" lang="sql">hive&gt; SELECT id, name FROM test_array LATERAL VIEW explode(b) r1 AS name LATERAL VIEW explode(A) r2 AS id;
10	tom
11	tom
10	mary
11	mary
20	kate
21	kate
20	tim
21	tim
</pre>
## 参考

<a href="http://www.oratea.net/?p=650" target="_blank">hive中的Lateral View</a>