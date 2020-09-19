---
title: Hive改表名后查询不了数据(DataNucleus缓存问题)
author: fatkun
type: post
date: 2013-05-29T17:21:15+00:00
url: /2013/05/hive-rename.html
duoshuo_thread_id:
  - 6300410023910572801
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:1048:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> getMetaData<span style="color: #009900;">&#40;</span>QB qb<span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">throws</span> SemanticException <span style="color: #009900;">&#123;</span>
        tab <span style="color: #339933;">=</span> db.<span style="color: #006633;">getTable</span><span style="color: #009900;">&#40;</span>tab_name<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">// 这里返回了上一次的结果</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">public void getMetaData(QB qb) throws SemanticException {
        tab = db.getTable(tab_name); // 这里返回了上一次的结果
    }</p></div>
    ";i:2;s:1350:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>datanucleus.cache.level2.type<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>none<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">&lt;property&gt;
      &lt;name&gt;datanucleus.cache.level2.type&lt;/name&gt;
      &lt;value&gt;none&lt;/value&gt;
    &lt;/property&gt;</p></div>
    ";}
categories:
  - hive
tags:
  - cache
  - datanucleus
  - hive
  - 缓存

---
## 现象

改了Hive表名后查询不了任何数据。
## 重现方式

开启两个hive命令行，  
先在第一个hive查询一条语句：select * from logs1;  
然后在第二个hive把表名更改：alter table logs1 rename to logs2;  
再在第一个hive查询：select * from logs2;//这时查询成功，但没有数据
## 调试

想到可能是缓存或者事务的原因。。虽然发现查询条件没有错，但返回结果的预期不一样
<pre lang="java" escaped="true">public void getMetaData(QB qb) throws SemanticException {
    tab = db.getTable(tab_name); // 这里返回了上一次的结果
}</pre>
代码太多了。。最终还是没搞懂哪里缓存了。。实际上跟踪调试是经过了mysql-connector的查询，中间结果返回了JDBCResult，但是二进制的结果，看不出什么东西，不知道为什么最后返回的结果却是缓存的。只能随便试试看DataNucleus有那些缓存的参数了，死马当活马医。
找到有以下参数：
datanucleus.query.compilation.cached  
datanucleus.query.results.cached  
datanucleus.cache.level2.type
最终试了datanucleus.cache.level2.type可行。。
##  解决方法

在hive-site.xml加上这个参数
<pre lang="xml" escaped="true">&lt;property&gt;
  &lt;name&gt;datanucleus.cache.level2.type&lt;/name&gt;
  &lt;value&gt;none&lt;/value&gt;
&lt;/property&gt;</pre>