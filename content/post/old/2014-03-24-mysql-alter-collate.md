---
title: mysql 排序规则 COLLATE 修改
author: fatkun
type: post
date: 2014-03-24T07:23:59+00:00
url: /2014/03/mysql-alter-collate.html
duoshuo_thread_id:
  - 6300410318308770562
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:839:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;"><span style="color: #993333; font-weight: bold;">ALTER</span> <span style="color: #993333; font-weight: bold;">TABLE</span> <span style="color: #66cc66;">&lt;</span>some_table<span style="color: #66cc66;">&gt;</span> <span style="color: #993333; font-weight: bold;">CONVERT</span> <span style="color: #993333; font-weight: bold;">TO</span> <span style="color: #993333; font-weight: bold;">CHARACTER</span> <span style="color: #993333; font-weight: bold;">SET</span> utf8 <span style="color: #993333; font-weight: bold;">COLLATE</span> utf8_unicode_ci;</pre></td></tr></table><p class="theCode" style="display:none;">alter table &lt;some_table&gt; convert to character set utf8 collate utf8_unicode_ci;</p></div>
    ";}
categories:
  - 数据库
tags:
  - COLLATE
  - mysql
  - 排序规则

---
使用以下语句转换。
<pre lang="sql" escaped="true">alter table &lt;some_table&gt; convert to character set utf8 collate utf8_unicode_ci;</pre>
来源：http://stackoverflow.com/questions/742205/mysql-alter-table-collation