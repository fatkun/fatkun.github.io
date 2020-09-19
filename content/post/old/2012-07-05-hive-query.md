---
title: Hive查询用到的语句记录
author: fatkun
type: post
date: 2012-07-05T09:03:59+00:00
url: /2012/07/hive-query.html
duoshuo_thread_id:
  - 6300408859206877953
wp-syntax-cache-content:
  - |
    a:8:{i:1;s:679:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;"><span style="color: #993333; font-weight: bold;">SELECT</span> <span style="color: #66cc66;">*</span> <span style="color: #993333; font-weight: bold;">FROM</span> <span style="color: #66cc66;">&#40;</span><span style="color: #993333; font-weight: bold;">SELECT</span> A<span style="color: #66cc66;">,</span>B <span style="color: #993333; font-weight: bold;">FROM</span> atable<span style="color: #66cc66;">&#41;</span> alaisName</pre></td></tr></table><p class="theCode" style="display:none;">SELECT * FROM (SELECT A,B FROM atable) alaisName</p></div>
    ";i:2;s:678:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;"><span style="color: #993333; font-weight: bold;">SELECT</span> a<span style="color: #66cc66;">,</span><span style="color: #993333; font-weight: bold;">SUM</span><span style="color: #66cc66;">&#40;</span>b<span style="color: #66cc66;">&#41;</span> <span style="color: #993333; font-weight: bold;">FROM</span> atable <span style="color: #993333; font-weight: bold;">GROUP</span> <span style="color: #993333; font-weight: bold;">BY</span> b</pre></td></tr></table><p class="theCode" style="display:none;">select a,sum(b) from atable group by b</p></div>
    ";i:3;s:826:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;"><span style="color: #993333; font-weight: bold;">SELECT</span> <span style="color: #993333; font-weight: bold;">MAX</span><span style="color: #66cc66;">&#40;</span>a<span style="color: #66cc66;">&#41;</span><span style="color: #66cc66;">,</span><span style="color: #993333; font-weight: bold;">SUM</span><span style="color: #66cc66;">&#40;</span>b<span style="color: #66cc66;">&#41;</span> <span style="color: #993333; font-weight: bold;">FROM</span> atable <span style="color: #993333; font-weight: bold;">GROUP</span> <span style="color: #993333; font-weight: bold;">BY</span> b</pre></td></tr></table><p class="theCode" style="display:none;">select max(a),sum(b) from atable group by b</p></div>
    ";i:4;s:1061:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;"><span style="color: #993333; font-weight: bold;">SELECT</span> <span style="color: #66cc66;">*</span> <span style="color: #993333; font-weight: bold;">FROM</span> <span style="color: #66cc66;">&#40;</span><span style="color: #993333; font-weight: bold;">SELECT</span> <span style="color: #993333; font-weight: bold;">SUM</span><span style="color: #66cc66;">&#40;</span>A<span style="color: #66cc66;">&#41;</span> ASUM <span style="color: #993333; font-weight: bold;">FROM</span> ATABLE <span style="color: #993333; font-weight: bold;">GROUP</span> <span style="color: #993333; font-weight: bold;">BY</span> A<span style="color: #66cc66;">&#41;</span> SUBQ1 <span style="color: #993333; font-weight: bold;">WHERE</span> ASUM &amp;gt; <span style="color: #cc66cc;">10</span></pre></td></tr></table><p class="theCode" style="display:none;">SELECT * FROM (SELECT SUM(A) ASUM FROM ATABLE GROUP BY A) SUBQ1 WHERE ASUM &amp;gt; 10</p></div>
    ";i:5;s:1608:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;"><span style="color: #993333; font-weight: bold;">SELECT</span> <span style="color: #66cc66;">*</span>
      <span style="color: #993333; font-weight: bold;">FROM</span> log a
      <span style="color: #993333; font-weight: bold;">LEFT</span> <span style="color: #993333; font-weight: bold;">OUTER</span> <span style="color: #993333; font-weight: bold;">JOIN</span> users b
      <span style="color: #993333; font-weight: bold;">ON</span> <span style="color: #993333; font-weight: bold;">CASE</span> <span style="color: #993333; font-weight: bold;">WHEN</span> a<span style="color: #66cc66;">.</span>user_id <span style="color: #993333; font-weight: bold;">IS</span> <span style="color: #993333; font-weight: bold;">NULL</span> <span style="color: #993333; font-weight: bold;">THEN</span> concat<span style="color: #66cc66;">&#40;</span>‘hive’<span style="color: #66cc66;">,</span>rand<span style="color: #66cc66;">&#40;</span><span style="color: #66cc66;">&#41;</span> <span style="color: #66cc66;">&#41;</span> <span style="color: #993333; font-weight: bold;">ELSE</span> a<span style="color: #66cc66;">.</span>user_id <span style="color: #993333; font-weight: bold;">END</span> <span style="color: #66cc66;">=</span> b<span style="color: #66cc66;">.</span>user_id;</pre></td></tr></table><p class="theCode" style="display:none;">select *
      from log a
      left outer join users b
      on case when a.user_id is null then concat(‘hive’,rand() ) else a.user_id end = b.user_id;</p></div>
    ";i:6;s:209:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;">&nbsp;</pre></td></tr></table><p class="theCode" style="display:none;"></p></div>
    ";i:7;s:642:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="html" style="font-family:monospace;">-- 要实现这个，key不在B表
    select a.key from a where key not in(select key from b)
    -- 改写为 左连接key，找出B表key为null的
    select a.key from a left outer join b on a.key=b.key where b.key1 is null</pre></td></tr></table><p class="theCode" style="display:none;">-- 要实现这个，key不在B表
    select a.key from a where key not in(select key from b)
    -- 改写为 左连接key，找出B表key为null的
    select a.key from a left outer join b on a.key=b.key where b.key1 is null</p></div>
    ";i:8;s:209:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;">&nbsp;</pre></td></tr></table><p class="theCode" style="display:none;"></p></div>
    ";}
categories:
  - hive
tags:
  - hive
  - query

---
## 子查询

子查询需要一个别名
<pre lang="sql">SELECT * FROM (SELECT A,B FROM atable) alaisName</pre>
## group by

**这样的语句会报错，提示a不在group by里面**
<pre lang="sql">select a,sum(b) from atable group by b</pre>
hive Expression Not In Group By Key  
via:[来源][1]  
解决方法是，使用 max、min、或者collect_set，如：
<pre lang="sql">select max(a),sum(b) from atable group by b</pre>
**group by 之后字段可以作为条件再继续查找**
<pre lang="sql">SELECT * FROM (SELECT SUM(A) ASUM FROM ATABLE GROUP BY A) SUBQ1 WHERE ASUM &gt; 10</pre>
## Join

默认join是内连接，还有left outer join 、right outer join和 full outer join
## 可以用case when &#8230; then &#8230; else &#8230;

语法: CASE a WHEN b THEN c [WHEN d THEN e]* [ELSE f] END via:[HIVE UDF整理（九）][2]
via:[数据倾斜总结][3]
<pre lang="sql">select *
  from log a
  left outer join users b
  on case when a.user_id is null then concat(‘hive’,rand() ) else a.user_id end = b.user_id;</pre>
<pre lang="sql"></pre>
<h2 lang="sql">  Not in</h2>
not in 在Hive0.8才支持，在之前的版本可以用left outer join代替
<a href="http://chiyx.iteye.com/blog/1530981" target="_blank">Hive使用LEFT OUTER JOIN 实现not in </a>
<pre lang="html">-- 要实现这个，key不在B表
select a.key from a where key not in(select key from b)
-- 改写为 左连接key，找出B表key为null的
select a.key from a left outer join b on a.key=b.key where b.key1 is null</pre>
&nbsp;
<pre lang="sql"></pre>

 [1]: http://stackoverflow.com/questions/5746687/hive-expression-not-in-group-by-key
 [2]: http://www.oratea.net/?p=948
 [3]: http://www.tbdata.org/archives/2109