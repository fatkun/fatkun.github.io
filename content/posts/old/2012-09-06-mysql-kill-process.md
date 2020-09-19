---
title: mysql kill process解决死锁
author: fatkun
type: post
date: 2012-09-06T06:11:56+00:00
url: /2012/09/mysql-kill-process.html
duoshuo_thread_id:
  - 6300408866257502978
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:282:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="html" style="font-family:monospace;">show processlist;
    和 
    kill id,id...;</pre></td></tr></table><p class="theCode" style="display:none;">show processlist;
    和 
    kill id,id...;</p></div>
    ";i:2;s:5596:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;">mysql<span style="color: #66cc66;">&gt;</span> <span style="color: #993333; font-weight: bold;">SHOW</span> processlist;
    <span style="color: #66cc66;">+</span><span style="color: #808080; font-style: italic;">----+------+-----------+------+---------+------+-------+------------------+</span>
    &amp;brvbar; Id &amp;brvbar; <span style="color: #993333; font-weight: bold;">USER</span> &amp;brvbar; Host      &amp;brvbar; db   &amp;brvbar; Command &amp;brvbar; <span style="color: #993333; font-weight: bold;">TIME</span> &amp;brvbar; State &amp;brvbar; Info             &amp;brvbar;
    <span style="color: #66cc66;">+</span><span style="color: #808080; font-style: italic;">----+------+-----------+------+---------+------+-------+------------------+</span>
    &amp;brvbar;  <span style="color: #cc66cc;">7</span> &amp;brvbar; root &amp;brvbar; localhost &amp;brvbar; yy   &amp;brvbar; Sleep   &amp;brvbar;  <span style="color: #cc66cc;">154</span> &amp;brvbar;       &amp;brvbar; <span style="color: #993333; font-weight: bold;">NULL</span>             &amp;brvbar; 
    &amp;brvbar;  <span style="color: #cc66cc;">8</span> &amp;brvbar; root &amp;brvbar; localhost &amp;brvbar; <span style="color: #993333; font-weight: bold;">NULL</span> &amp;brvbar; Query   &amp;brvbar;    <span style="color: #cc66cc;">0</span> &amp;brvbar; <span style="color: #993333; font-weight: bold;">NULL</span>  &amp;brvbar; <span style="color: #993333; font-weight: bold;">SHOW</span> processlist &amp;brvbar; 
    <span style="color: #66cc66;">+</span><span style="color: #808080; font-style: italic;">----+------+-----------+------+---------+------+-------+------------------+</span>
    <span style="color: #cc66cc;">2</span> <span style="color: #993333; font-weight: bold;">ROWS</span> <span style="color: #993333; font-weight: bold;">IN</span> <span style="color: #993333; font-weight: bold;">SET</span> <span style="color: #66cc66;">&#40;</span><span style="color: #cc66cc;">0.00</span> sec<span style="color: #66cc66;">&#41;</span>
    &nbsp;
    mysql<span style="color: #66cc66;">&gt;</span> <span style="color: #993333; font-weight: bold;">KILL</span> <span style="color: #cc66cc;">7</span>
        <span style="color: #66cc66;">-&gt;</span> ;
    &nbsp;
    mysql<span style="color: #66cc66;">&gt;</span> <span style="color: #993333; font-weight: bold;">SHOW</span> processlist;
    <span style="color: #66cc66;">+</span><span style="color: #808080; font-style: italic;">----+------+-----------+------+---------+------+-------+------------------+</span>
    &amp;brvbar; Id &amp;brvbar; <span style="color: #993333; font-weight: bold;">USER</span> &amp;brvbar; Host      &amp;brvbar; db   &amp;brvbar; Command &amp;brvbar; <span style="color: #993333; font-weight: bold;">TIME</span> &amp;brvbar; State &amp;brvbar; Info             &amp;brvbar;
    <span style="color: #66cc66;">+</span><span style="color: #808080; font-style: italic;">----+------+-----------+------+---------+------+-------+------------------+</span>
    &amp;brvbar;  <span style="color: #cc66cc;">8</span> &amp;brvbar; root &amp;brvbar; localhost &amp;brvbar; <span style="color: #993333; font-weight: bold;">NULL</span> &amp;brvbar; Query   &amp;brvbar;    <span style="color: #cc66cc;">0</span> &amp;brvbar; <span style="color: #993333; font-weight: bold;">NULL</span>  &amp;brvbar; <span style="color: #993333; font-weight: bold;">SHOW</span> processlist &amp;brvbar; 
    <span style="color: #66cc66;">+</span><span style="color: #808080; font-style: italic;">----+------+-----------+------+---------+------+-------+------------------+</span>
    <span style="color: #cc66cc;">1</span> <span style="color: #993333; font-weight: bold;">ROW</span> <span style="color: #993333; font-weight: bold;">IN</span> <span style="color: #993333; font-weight: bold;">SET</span> <span style="color: #66cc66;">&#40;</span><span style="color: #cc66cc;">0.00</span> sec<span style="color: #66cc66;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">mysql&gt; show processlist;
    +----+------+-----------+------+---------+------+-------+------------------+
    &amp;brvbar; Id &amp;brvbar; User &amp;brvbar; Host      &amp;brvbar; db   &amp;brvbar; Command &amp;brvbar; Time &amp;brvbar; State &amp;brvbar; Info             &amp;brvbar;
    +----+------+-----------+------+---------+------+-------+------------------+
    &amp;brvbar;  7 &amp;brvbar; root &amp;brvbar; localhost &amp;brvbar; yy   &amp;brvbar; Sleep   &amp;brvbar;  154 &amp;brvbar;       &amp;brvbar; NULL             &amp;brvbar; 
    &amp;brvbar;  8 &amp;brvbar; root &amp;brvbar; localhost &amp;brvbar; NULL &amp;brvbar; Query   &amp;brvbar;    0 &amp;brvbar; NULL  &amp;brvbar; show processlist &amp;brvbar; 
    +----+------+-----------+------+---------+------+-------+------------------+
    2 rows in set (0.00 sec)
    
    mysql&gt; kill 7
        -&gt; ;
    
    mysql&gt; show processlist;
    +----+------+-----------+------+---------+------+-------+------------------+
    &amp;brvbar; Id &amp;brvbar; User &amp;brvbar; Host      &amp;brvbar; db   &amp;brvbar; Command &amp;brvbar; Time &amp;brvbar; State &amp;brvbar; Info             &amp;brvbar;
    +----+------+-----------+------+---------+------+-------+------------------+
    &amp;brvbar;  8 &amp;brvbar; root &amp;brvbar; localhost &amp;brvbar; NULL &amp;brvbar; Query   &amp;brvbar;    0 &amp;brvbar; NULL  &amp;brvbar; show processlist &amp;brvbar; 
    +----+------+-----------+------+---------+------+-------+------------------+
    1 row in set (0.00 sec)</p></div>
    ";}
categories:
  - 未分类

---
主要是两个命令：
<pre escaped="true" lang="html">show processlist;
和 
kill id,id...;</pre>
版权声明：转载时请以超链接形式标明文章原始出处和作者信息及本声明  
来源：http://ri0day.blogbus.com/logs/59186177.html
mysql使用myisam的时候锁表比较多，尤其有慢查询的时候，造成死锁.这时需要手动kill掉locked的process.使他释放.
(以前我都是重起服务)..惭愧啊..
演示:(id 7是我用python 来连过来的一个会话,虽然是状态是sleep,为了演示，干掉他)
<pre escaped="true" lang="sql">mysql&gt; show processlist;
+----+------+-----------+------+---------+------+-------+------------------+
&brvbar; Id &brvbar; User &brvbar; Host      &brvbar; db   &brvbar; Command &brvbar; Time &brvbar; State &brvbar; Info             &brvbar;
+----+------+-----------+------+---------+------+-------+------------------+
&brvbar;  7 &brvbar; root &brvbar; localhost &brvbar; yy   &brvbar; Sleep   &brvbar;  154 &brvbar;       &brvbar; NULL             &brvbar; 
&brvbar;  8 &brvbar; root &brvbar; localhost &brvbar; NULL &brvbar; Query   &brvbar;    0 &brvbar; NULL  &brvbar; show processlist &brvbar; 
+----+------+-----------+------+---------+------+-------+------------------+
2 rows in set (0.00 sec)

mysql&gt; kill 7
    -&gt; ;

mysql&gt; show processlist;
+----+------+-----------+------+---------+------+-------+------------------+
&brvbar; Id &brvbar; User &brvbar; Host      &brvbar; db   &brvbar; Command &brvbar; Time &brvbar; State &brvbar; Info             &brvbar;
+----+------+-----------+------+---------+------+-------+------------------+
&brvbar;  8 &brvbar; root &brvbar; localhost &brvbar; NULL &brvbar; Query   &brvbar;    0 &brvbar; NULL  &brvbar; show processlist &brvbar; 
+----+------+-----------+------+---------+------+-------+------------------+
1 row in set (0.00 sec)</pre>