---
title: mysql修改表、字段、库的字符集
author: fatkun
type: post
date: 2011-05-02T08:20:27+00:00
url: /2011/05/mysql-alter-charset.html
duoshuo_thread_id:
  - 6300408813702873858
wp-syntax-cache-content:
  - |
    a:7:{i:1;s:806:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;"><span style="color: #993333; font-weight: bold;">ALTER</span> <span style="color: #993333; font-weight: bold;">DATABASE</span> db_name <span style="color: #993333; font-weight: bold;">DEFAULT</span> <span style="color: #993333; font-weight: bold;">CHARACTER</span> <span style="color: #993333; font-weight: bold;">SET</span> character_name <span style="color: #66cc66;">&#91;</span><span style="color: #993333; font-weight: bold;">COLLATE</span> <span style="color: #66cc66;">...</span><span style="color: #66cc66;">&#93;</span>;</pre></td></tr></table><p class="theCode" style="display:none;">ALTER DATABASE db_name DEFAULT CHARACTER SET character_name [COLLATE ...];</p></div>
    ";i:2;s:1417:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;"><span style="color: #993333; font-weight: bold;">ALTER</span> <span style="color: #993333; font-weight: bold;">TABLE</span> tbl_name <span style="color: #993333; font-weight: bold;">CONVERT</span> <span style="color: #993333; font-weight: bold;">TO</span> <span style="color: #993333; font-weight: bold;">CHARACTER</span> <span style="color: #993333; font-weight: bold;">SET</span> character_name <span style="color: #66cc66;">&#91;</span><span style="color: #993333; font-weight: bold;">COLLATE</span> <span style="color: #66cc66;">...</span><span style="color: #66cc66;">&#93;</span>
    如：<span style="color: #993333; font-weight: bold;">ALTER</span> <span style="color: #993333; font-weight: bold;">TABLE</span> logtest <span style="color: #993333; font-weight: bold;">CONVERT</span> <span style="color: #993333; font-weight: bold;">TO</span> <span style="color: #993333; font-weight: bold;">CHARACTER</span> <span style="color: #993333; font-weight: bold;">SET</span> utf8 <span style="color: #993333; font-weight: bold;">COLLATE</span> utf8_general_ci;</pre></td></tr></table><p class="theCode" style="display:none;">ALTER TABLE tbl_name CONVERT TO CHARACTER SET character_name [COLLATE ...]
    如：ALTER TABLE logtest CONVERT TO CHARACTER SET utf8 COLLATE utf8_general_ci;</p></div>
    ";i:3;s:1293:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;"><span style="color: #993333; font-weight: bold;">ALTER</span> <span style="color: #993333; font-weight: bold;">TABLE</span> tbl_name <span style="color: #993333; font-weight: bold;">DEFAULT</span> <span style="color: #993333; font-weight: bold;">CHARACTER</span> <span style="color: #993333; font-weight: bold;">SET</span> character_name <span style="color: #66cc66;">&#91;</span><span style="color: #993333; font-weight: bold;">COLLATE</span><span style="color: #66cc66;">...</span><span style="color: #66cc66;">&#93;</span>;
    如：<span style="color: #993333; font-weight: bold;">ALTER</span> <span style="color: #993333; font-weight: bold;">TABLE</span> logtest <span style="color: #993333; font-weight: bold;">DEFAULT</span> <span style="color: #993333; font-weight: bold;">CHARACTER</span> <span style="color: #993333; font-weight: bold;">SET</span> utf8 <span style="color: #993333; font-weight: bold;">COLLATE</span> utf8_general_ci;</pre></td></tr></table><p class="theCode" style="display:none;">ALTER TABLE tbl_name DEFAULT CHARACTER SET character_name [COLLATE...];
    如：ALTER TABLE logtest DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;</p></div>
    ";i:4;s:1544:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;"><span style="color: #993333; font-weight: bold;">ALTER</span> <span style="color: #993333; font-weight: bold;">TABLE</span> tbl_name <span style="color: #993333; font-weight: bold;">CHANGE</span> c_name c_name <span style="color: #993333; font-weight: bold;">CHARACTER</span> <span style="color: #993333; font-weight: bold;">SET</span> character_name <span style="color: #66cc66;">&#91;</span><span style="color: #993333; font-weight: bold;">COLLATE</span> <span style="color: #66cc66;">...</span><span style="color: #66cc66;">&#93;</span>;
    如：<span style="color: #993333; font-weight: bold;">ALTER</span> <span style="color: #993333; font-weight: bold;">TABLE</span> logtest <span style="color: #993333; font-weight: bold;">CHANGE</span> title title <span style="color: #993333; font-weight: bold;">VARCHAR</span><span style="color: #66cc66;">&#40;</span><span style="color: #cc66cc;">100</span><span style="color: #66cc66;">&#41;</span> <span style="color: #993333; font-weight: bold;">CHARACTER</span> <span style="color: #993333; font-weight: bold;">SET</span> utf8 <span style="color: #993333; font-weight: bold;">COLLATE</span> utf8_general_ci;</pre></td></tr></table><p class="theCode" style="display:none;">ALTER TABLE tbl_name CHANGE c_name c_name CHARACTER SET character_name [COLLATE ...];
    如：ALTER TABLE logtest CHANGE title title VARCHAR(100) CHARACTER SET utf8 COLLATE utf8_general_ci;</p></div>
    ";i:5;s:429:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;"><span style="color: #993333; font-weight: bold;">SHOW</span> <span style="color: #993333; font-weight: bold;">CREATE</span> <span style="color: #993333; font-weight: bold;">DATABASE</span> db_name;</pre></td></tr></table><p class="theCode" style="display:none;">show create database db_name;</p></div>
    ";i:6;s:425:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;"><span style="color: #993333; font-weight: bold;">SHOW</span> <span style="color: #993333; font-weight: bold;">CREATE</span> <span style="color: #993333; font-weight: bold;">TABLE</span> tbl_name;</pre></td></tr></table><p class="theCode" style="display:none;">show create table tbl_name;</p></div>
    ";i:7;s:491:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;"><span style="color: #993333; font-weight: bold;">SHOW</span> <span style="color: #993333; font-weight: bold;">FULL</span> <span style="color: #993333; font-weight: bold;">COLUMNS</span> <span style="color: #993333; font-weight: bold;">FROM</span> tbl_name;</pre></td></tr></table><p class="theCode" style="display:none;">show full columns from tbl_name;</p></div>
    ";}
categories:
  - 数据库
tags:
  - charset
  - mysql
  - 字符集

---
修改数据库字符集：
<pre escaped="true" lang="sql">ALTER DATABASE db_name DEFAULT CHARACTER SET character_name [COLLATE ...];</pre>
把表默认的字符集和所有字符列（CHAR,VARCHAR,TEXT）改为新的字符集：
<pre escaped="true" lang="sql">ALTER TABLE tbl_name CONVERT TO CHARACTER SET character_name [COLLATE ...]
如：ALTER TABLE logtest CONVERT TO CHARACTER SET utf8 COLLATE utf8_general_ci;</pre>
只是修改表的默认字符集：
<pre escaped="true" lang="sql">ALTER TABLE tbl_name DEFAULT CHARACTER SET character_name [COLLATE...];
如：ALTER TABLE logtest DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;</pre>
修改字段的字符集：
<pre escaped="true" lang="sql">ALTER TABLE tbl_name CHANGE c_name c_name CHARACTER SET character_name [COLLATE ...];
如：ALTER TABLE logtest CHANGE title title VARCHAR(100) CHARACTER SET utf8 COLLATE utf8_general_ci;</pre>
查看数据库编码：
<pre escaped="true" lang="sql">show create database db_name;</pre>
查看表编码：
<pre escaped="true" lang="sql">show create table tbl_name;</pre>
查看字段编码：
<pre escaped="true" lang="sql">show full columns from tbl_name;</pre>
来源：<http://www.diannaowa.com/index.php/archives/233>