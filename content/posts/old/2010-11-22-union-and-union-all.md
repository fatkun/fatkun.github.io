---
title: 数据库UNION和UNION ALL比较
author: fatkun
type: post
date: 2010-11-22T05:22:08+00:00
url: /2010/11/union-and-union-all.html
duoshuo_thread_id:
  - 6300408777304703746
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:631:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;"><span style="color: #993333; font-weight: bold;">SELECT</span> <span style="color: #66cc66;">*</span> <span style="color: #993333; font-weight: bold;">FROM</span> A <span style="color: #993333; font-weight: bold;">UNION</span> <span style="color: #993333; font-weight: bold;">SELECT</span> <span style="color: #66cc66;">*</span> <span style="color: #993333; font-weight: bold;">FROM</span> B</pre></td></tr></table><p class="theCode" style="display:none;">select * from A union select * from B</p></div>
    ";}
categories:
  - 数据库
tags:
  - UNION
  - UNION ALL

---
UNION能够把结果集合并
<pre escaped="true" lang="sql">select * from A union select * from B</pre>
如果能确定没有重复行，建议使用UNION ALL，不用排序。
  1. order by子句必须写在最后一个结果集里，并且其排序规则将改变操作后的排序结果。对于Union、Union All、Intersect、Minus都有效。
  2. Union可以对字段名不同但数据类型相同的结果集进行合并；
  3. 如果字段名不同的结果集进行Union，那么对此字段的Order by子句将失效。
  4. Union，对两个结果集进行并集操作，不包括重复行，同时进行默认规则的排序；
  5. Union All，对两个结果集进行并集操作，包括重复行，不进行排序；
  6. Intersect，对两个结果集进行交集操作，不包括重复行，同时进行默认规则的排序；
  7. Minus，对两个结果集进行差操作，不包括重复行，同时进行默认规则的排序。
  8. 可以在最后一个结果集中指定Order by子句改变排序方式。