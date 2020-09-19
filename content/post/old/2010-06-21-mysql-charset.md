---
title: Mysql指定编码创建数据库
author: fatkun
type: post
date: 2010-06-21T06:42:23+00:00
url: /2010/06/mysql-charset.html
duoshuo_thread_id:
  - 6300408737504953090
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:724:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;"><span style="color: #993333; font-weight: bold;">CREATE</span> <span style="color: #993333; font-weight: bold;">DATABASE</span> <span style="color: #ff0000;">`test2`</span> <span style="color: #993333; font-weight: bold;">DEFAULT</span> <span style="color: #993333; font-weight: bold;">CHARACTER</span> <span style="color: #993333; font-weight: bold;">SET</span> utf8 <span style="color: #993333; font-weight: bold;">COLLATE</span> utf8_general_ci</pre></td></tr></table><p class="theCode" style="display:none;">CREATE DATABASE `test2` DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci</p></div>
    ";}
categories:
  - 数据库

---
mysql 创建数据库时指定编码很重要，一般都指定为统一的UTF-8编码，如果不指定编码，默认编码为lan1，插入中文时是会提示错误的，类似&#8221;\x22\x34&#8243;
<pre escaped="true" lang="sql">CREATE DATABASE `test2` DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci
</pre>