---
title: hive1.1.0查询和旧版本不一致问题分析
author: fatkun
type: post
date: 2015-06-28T07:08:22+00:00
url: /2015/06/hive-join-failed.html
duoshuo_thread_id:
  - 6300410895981871873
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:2582:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;"><span style="color: #993333; font-weight: bold;">SELECT</span> tab1<span style="color: #66cc66;">.</span>ip<span style="color: #66cc66;">,</span> tab1<span style="color: #66cc66;">.</span>tm<span style="color: #66cc66;">,</span> tab2<span style="color: #66cc66;">.</span>hour
    <span style="color: #993333; font-weight: bold;">FROM</span> <span style="color: #66cc66;">&#40;</span>
        <span style="color: #993333; font-weight: bold;">SELECT</span> c<span style="color: #66cc66;">.</span>ip<span style="color: #66cc66;">,</span>c<span style="color: #66cc66;">.</span>lkid<span style="color: #66cc66;">,</span> c<span style="color: #66cc66;">.</span>hour<span style="color: #66cc66;">,</span><span style="color: #993333; font-weight: bold;">MIN</span><span style="color: #66cc66;">&#40;</span>s<span style="color: #66cc66;">.</span>hour<span style="color: #66cc66;">&#41;</span> <span style="color: #993333; font-weight: bold;">AS</span> tm <span style="color: #993333; font-weight: bold;">FROM</span> Tclick_iphone c <span style="color: #993333; font-weight: bold;">JOIN</span> Tsndata_iphone s 
        <span style="color: #993333; font-weight: bold;">ON</span> c<span style="color: #66cc66;">.</span>ip<span style="color: #66cc66;">=</span>s<span style="color: #66cc66;">.</span>ip <span style="color: #993333; font-weight: bold;">GROUP</span> <span style="color: #993333; font-weight: bold;">BY</span> c<span style="color: #66cc66;">.</span>ip<span style="color: #66cc66;">,</span>c<span style="color: #66cc66;">.</span>lkid<span style="color: #66cc66;">,</span>c<span style="color: #66cc66;">.</span>hour
    <span style="color: #66cc66;">&#41;</span> tab1 <span style="color: #993333; font-weight: bold;">JOIN</span> Tsndata_iphone tab2
    <span style="color: #993333; font-weight: bold;">ON</span> tab1<span style="color: #66cc66;">.</span>ip<span style="color: #66cc66;">=</span>tab2<span style="color: #66cc66;">.</span>ip <span style="color: #993333; font-weight: bold;">AND</span> tab1<span style="color: #66cc66;">.</span>tm<span style="color: #66cc66;">=</span>tab2<span style="color: #66cc66;">.</span>hour;</pre></td></tr></table><p class="theCode" style="display:none;">select tab1.ip, tab1.tm, tab2.hour
    from (
        select c.ip,c.lkid, c.hour,min(s.hour) as tm from Tclick_iphone c join Tsndata_iphone s 
        on c.ip=s.ip group by c.ip,c.lkid,c.hour
    ) tab1 join Tsndata_iphone tab2
    on tab1.ip=tab2.ip and tab1.tm=tab2.hour;</p></div>
    ";i:2;s:2494:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;"><span style="color: #993333; font-weight: bold;">SELECT</span> tab1<span style="color: #66cc66;">.</span>ip<span style="color: #66cc66;">,</span> tab1<span style="color: #66cc66;">.</span>tm<span style="color: #66cc66;">,</span> tab2<span style="color: #66cc66;">.</span>hour
    <span style="color: #993333; font-weight: bold;">FROM</span> <span style="color: #66cc66;">&#40;</span>
        <span style="color: #993333; font-weight: bold;">SELECT</span> c<span style="color: #66cc66;">.</span>ip<span style="color: #66cc66;">,</span>c<span style="color: #66cc66;">.</span>lkid<span style="color: #66cc66;">,</span> <span style="color: #993333; font-weight: bold;">MIN</span><span style="color: #66cc66;">&#40;</span>s<span style="color: #66cc66;">.</span>hour<span style="color: #66cc66;">&#41;</span> <span style="color: #993333; font-weight: bold;">AS</span> tm <span style="color: #993333; font-weight: bold;">FROM</span> Tclick_iphone c <span style="color: #993333; font-weight: bold;">JOIN</span> Tsndata_iphone s 
        <span style="color: #993333; font-weight: bold;">ON</span> c<span style="color: #66cc66;">.</span>ip<span style="color: #66cc66;">=</span>s<span style="color: #66cc66;">.</span>ip <span style="color: #993333; font-weight: bold;">GROUP</span> <span style="color: #993333; font-weight: bold;">BY</span> c<span style="color: #66cc66;">.</span>ip<span style="color: #66cc66;">,</span>c<span style="color: #66cc66;">.</span>lkid<span style="color: #66cc66;">,</span>c<span style="color: #66cc66;">.</span>hour
    <span style="color: #66cc66;">&#41;</span> tab1 <span style="color: #993333; font-weight: bold;">JOIN</span> Tsndata_iphone tab2
    <span style="color: #993333; font-weight: bold;">ON</span> tab1<span style="color: #66cc66;">.</span>ip<span style="color: #66cc66;">=</span>tab2<span style="color: #66cc66;">.</span>ip <span style="color: #993333; font-weight: bold;">AND</span> tab1<span style="color: #66cc66;">.</span>tm<span style="color: #66cc66;">=</span>tab2<span style="color: #66cc66;">.</span>hour;</pre></td></tr></table><p class="theCode" style="display:none;">select tab1.ip, tab1.tm, tab2.hour
    from (
        select c.ip,c.lkid, min(s.hour) as tm from Tclick_iphone c join Tsndata_iphone s 
        on c.ip=s.ip group by c.ip,c.lkid,c.hour
    ) tab1 join Tsndata_iphone tab2
    on tab1.ip=tab2.ip and tab1.tm=tab2.hour;</p></div>
    ";}
categories:
  - hadoop
  - hive
tags:
  - hive

---
<div>  <h2>    背景  </h2></div>
在查询以下语句的时候结果不正确，无法<span lang="EN-US">join tab1.tm=tab2.hour</span>。如果存在以下类似的语句，有子查询的<span lang="EN-US">group by</span>，外层有<span lang="EN-US">join</span>语句，返回的结果不正确，无法<span lang="EN-US">join</span>成功。
<pre lang="sql" escaped="true">select tab1.ip, tab1.tm, tab2.hour
from (
    select c.ip,c.lkid, c.hour,min(s.hour) as tm from Tclick_iphone c join Tsndata_iphone s 
    on c.ip=s.ip group by c.ip,c.lkid,c.hour
) tab1 join Tsndata_iphone tab2
on tab1.ip=tab2.ip and tab1.tm=tab2.hour;</pre>
<div></div>
<div>  <h2>    分析  </h2></div>
首先是构造可重复测试语句，减少所需要查询的数据，然后尝试替换其中的语句，检查语句是否正常。缩小错误范围。
测试中发现如果把子查询替换为表，能够正常查询。另外在随机测试的过程中，发现这样的语句也可以成功。
<pre lang="sql" escaped="true">select tab1.ip, tab1.tm, tab2.hour
from (
    select c.ip,c.lkid, min(s.hour) as tm from Tclick_iphone c join Tsndata_iphone s 
    on c.ip=s.ip group by c.ip,c.lkid,c.hour
) tab1 join Tsndata_iphone tab2
on tab1.ip=tab2.ip and tab1.tm=tab2.hour;</pre>
<div></div>
### 单步调试<span lang="EN-US">1</span>

反复单步调试对比错误、正确语句，发现第二步的输入和正确的语句不一样。
这是字节数组，还有个解析这个字节数组的描述信息（多少个字段，各个字段的类型） ，正确语句输入的内容为：
<span lang="EN-US">[3, 14, 49, 50, 49, 46, 50, 51, 54, 46, 49, 54, 52, 46, 50, 56, -114, 11, -82, 0, 0, 0, 0, 0, 0, 0, 0, 0]</span>
描述信息有两个字段
错误的语句输入内容为：
<span lang="EN-US">[15, 14, 49, 50, 49, 46, 50, 51, 54, 46, 49, 54, 52, 46, 50, 56, 4, 119, 105, 102, 105, -114, 10, -84, -114, 11, -82, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]</span>
描述信息有两个字段
这个字节第一位是判断符号，判断是否是<span lang="EN-US">null</span>，后面的字符如果是<span lang="EN-US">string</span>，第一位是字符长度。如果是数字，会有类似这样的<span lang="EN-US">bytes [-114, 10, -84]</span>
从这里看出输入的内容不一致，但字段描述信息却一样。那错误可能发生在输入的内容不正确或者字段描述解析不正确。
### 单步调试<span lang="EN-US">2 &#8211; </span>输入内容、字段描述从哪里来

从<span lang="EN-US">explain</span>知道第二步的输入来源于子查询的输出，也就是子查询的<span lang="EN-US">reduce</span>输出。单步调试发现字段描述是在编译语句阶段已经确定好，每个<span lang="EN-US">Operator</span>已经确定了输出的字段数和类型。
另外在对比<span lang="EN-US">explain</span>中，发现正确的语句比错误的语句多了个<span lang="EN-US">SELECT Operator</span>（列裁剪）。
### 单步调试<span lang="EN-US">3 &#8211; </span>为什么错误语句少了<span lang="EN-US">SELECT Operator</span>？

范围缩小到语句的语法编译。
发现代码中会打印一些日志出来，可以修改<span lang="EN-US">hive</span>的<span lang="EN-US">log4j</span>文件改为<span lang="EN-US">debug</span>模式，发现语句优化的过程中把<span lang="EN-US">SELECT Operator</span>去掉了。
优化前
<div>  <pre><code>&lt;span lang="EN-US">TS[0]-FIL[2]-RS[3]-JOIN[6]-SEL[7]-GBY[8]-RS[9]-GBY[10]-SEL[11]-FIL[13]-RS[14]-JOIN[17]-SEL[18]-FS[19]&lt;/span></code></pre>
  <pre><code>&lt;span lang="EN-US">ppd.PredicatePushDown: After PPD&lt;/span></code></pre>
  <pre><code>&lt;span lang="EN-US">TS[0]-FIL[21]-RS[3]-JOIN[6]-SEL[7]-GBY[8]-RS[9]-GBY[10]-FIL[20]-SEL[11]-RS[14]-JOIN[17]-SEL[18]-FS[19]&lt;/span></code></pre></div>
优化后
<div>  <pre><code>&lt;span lang="EN-US">TS[0]-FIL[21]-RS[3]-JOIN[6]-GBY[8]-RS[9]-GBY[10]-FIL[20]-RS[14]-JOIN[17]-SEL[18]-FS[19]&lt;/span></code></pre></div>
可以看到在<span lang="EN-US">GBY[10]-FIL[20]-SEL[11]-RS[14]</span>中，<span lang="EN-US">SEL[11]</span>被去掉了。
单步调试语句的优化过程，由于优化步骤有<span lang="EN-US">21</span>个，使用二分法检查到底是运行到哪一个优化器把<span lang="EN-US">SEL</span>去掉了。
最终发现是 <span lang="EN-US">IdentityProjectRemover </span>优化器。
这个优化器的功能是根据前后输入输出，去掉不必要的<span lang="EN-US">SELECT Operator</span>。检查到这里，没有继续往下查了，还有一些为什么<span lang="EN-US">FIL[20] row schema</span>为什么是两个字段，但实际输出内容却不是的问题。
### 搜索

使用关键词<span lang="EN-US">IdentityProjectRemover</span>搜索源代码，看看这个代码最新版本有没有修改过。搜索发现一些<span lang="EN-US">issue</span>，找到了关闭这个优化器的参数。`<span lang="EN-US">hive.optimize.remove.identity.project=false</span>`，另外发现在<span lang="EN-US">hive1.2.0</span>版本，增加了另一个参数，间接默认关闭了这个优化。
另外发现这个<span lang="EN-US">issue</span>和我们这次的错误类似，应该是同一个问题<span lang="EN-US"> <a href="https://issues.apache.org/jira/browse/HIVE-10996" target="_blank">HIVE-10996</a> </span>。这个<span lang="EN-US">issue</span>里面有说明更详细的错误原因，见<span lang="EN-US"><a href="https://issues.apache.org/jira/browse/HIVE-10996?focusedCommentId=14592859&page=com.atlassian.jira.plugin.system.issuetabpanels:comment-tabpanel#comment-14592859" target="_blank"><span lang="EN-US"><span lang="EN-US">评论</span></span></a></span>
这个<span lang="EN-US">issue</span>已经有补丁，但目前还没有合并到主干。它的解决的方法是在<span lang="EN-US">GBY-FIL-SEL</span>中插入一个<span lang="EN-US">SEL</span>，变成<span lang="EN-US">GBY-SEL-FIL-SEL</span>
<div>  <h2>    当前解决方案  </h2></div>
设置参数 <span lang="EN-US">hive.optimize.remove.identity.project=false </span>关闭这个优化器
这个优化是从<span lang="EN-US">1.1.0</span>版本引入（我们当前使用的版本）
<div>  <h2>    技巧  </h2></div>
刚开始<span lang="EN-US">debug</span>的时候很慢，而且越用越慢，后来发现限制<span lang="EN-US">hive</span>客户端使用内存有一定效果。可能<span lang="EN-US">debug</span>时需要<span lang="EN-US">dump</span>内存。
使用 <span lang="EN-US">hive &#8211;debug </span>可以远程<span lang="EN-US">debug</span>
使用 <span lang="EN-US">hive &#8211;hiveconf hive.root.logger=DEBUG,console </span>可以临时打印日志