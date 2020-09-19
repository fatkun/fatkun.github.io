---
title: Ubuntu中配置Mysql编码
author: fatkun
type: post
date: 2011-05-03T08:42:34+00:00
url: /2011/05/ubuntu-mysql-charset.html
duoshuo_thread_id:
  - 6300408813749011201
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:312:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #c20cb9; font-weight: bold;">sudo</span> service mysql restart</pre></td></tr></table><p class="theCode" style="display:none;">sudo service mysql restart</p></div>
    ";i:2;s:3878:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;">mysql<span style="color: #66cc66;">&gt;</span> <span style="color: #993333; font-weight: bold;">SHOW</span> <span style="color: #993333; font-weight: bold;">VARIABLES</span> <span style="color: #993333; font-weight: bold;">LIKE</span> <span style="color: #ff0000;">'char%'</span>;
    <span style="color: #66cc66;">+</span><span style="color: #808080; font-style: italic;">--------------------------+----------------------------+</span>
    <span style="color: #66cc66;">|</span> Variable_name            <span style="color: #66cc66;">|</span> <span style="color: #993333; font-weight: bold;">VALUE</span>                      <span style="color: #66cc66;">|</span>
    <span style="color: #66cc66;">+</span><span style="color: #808080; font-style: italic;">--------------------------+----------------------------+</span>
    <span style="color: #66cc66;">|</span> character_set_client     <span style="color: #66cc66;">|</span> utf8                       <span style="color: #66cc66;">|</span>
    <span style="color: #66cc66;">|</span> character_set_connection <span style="color: #66cc66;">|</span> utf8                       <span style="color: #66cc66;">|</span>
    <span style="color: #66cc66;">|</span> character_set_database   <span style="color: #66cc66;">|</span> utf8                       <span style="color: #66cc66;">|</span>
    <span style="color: #66cc66;">|</span> character_set_filesystem <span style="color: #66cc66;">|</span> <span style="color: #993333; font-weight: bold;">BINARY</span>                     <span style="color: #66cc66;">|</span>
    <span style="color: #66cc66;">|</span> character_set_results    <span style="color: #66cc66;">|</span> utf8                       <span style="color: #66cc66;">|</span>
    <span style="color: #66cc66;">|</span> character_set_server     <span style="color: #66cc66;">|</span> utf8                       <span style="color: #66cc66;">|</span>
    <span style="color: #66cc66;">|</span> character_set_system     <span style="color: #66cc66;">|</span> utf8                       <span style="color: #66cc66;">|</span>
    <span style="color: #66cc66;">|</span> character_sets_dir       <span style="color: #66cc66;">|</span> <span style="color: #66cc66;">/</span>usr<span style="color: #66cc66;">/</span>share<span style="color: #66cc66;">/</span>mysql<span style="color: #66cc66;">/</span>charsets<span style="color: #66cc66;">/</span> <span style="color: #66cc66;">|</span>
    <span style="color: #66cc66;">+</span><span style="color: #808080; font-style: italic;">--------------------------+----------------------------+</span>
    <span style="color: #cc66cc;">8</span> <span style="color: #993333; font-weight: bold;">ROWS</span> <span style="color: #993333; font-weight: bold;">IN</span> <span style="color: #993333; font-weight: bold;">SET</span> <span style="color: #66cc66;">&#40;</span><span style="color: #cc66cc;">0.00</span> sec<span style="color: #66cc66;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">mysql&gt; show variables like 'char%';
    +--------------------------+----------------------------+
    | Variable_name            | Value                      |
    +--------------------------+----------------------------+
    | character_set_client     | utf8                       |
    | character_set_connection | utf8                       |
    | character_set_database   | utf8                       |
    | character_set_filesystem | binary                     |
    | character_set_results    | utf8                       |
    | character_set_server     | utf8                       |
    | character_set_system     | utf8                       |
    | character_sets_dir       | /usr/share/mysql/charsets/ |
    +--------------------------+----------------------------+
    8 rows in set (0.00 sec)</p></div>
    ";}
categories:
  - Linux
tags:
  - mysql
  - Ubuntu
  - 编码

---
## 找到配置文件

我是通过sudo apt-get install mysql来安装的。mysql的配置文件在/etc/mysql/my.cnf  
如果找不到这个文件，可以运行sudo find / -iname &#8216;*.cnf&#8217;查找所有的cnf文件
## 修改配置文件

在[mysqld]下添加  
default-character-set=utf8  
在[client]下添加  
default-character-set=utf8
## 重启mysql

<pre escaped="true" lang="bash">sudo service mysql restart</pre>
## 登录mysql查看是否成功

\# mysql -u root
<pre escaped="true" lang="sql">mysql> show variables like 'char%';
+--------------------------+----------------------------+
| Variable_name            | Value                      |
+--------------------------+----------------------------+
| character_set_client     | utf8                       |
| character_set_connection | utf8                       |
| character_set_database   | utf8                       |
| character_set_filesystem | binary                     |
| character_set_results    | utf8                       |
| character_set_server     | utf8                       |
| character_set_system     | utf8                       |
| character_sets_dir       | /usr/share/mysql/charsets/ |
+--------------------------+----------------------------+
8 rows in set (0.00 sec)
</pre>
## 修改已经部署的数据库编码

感觉还是挺麻烦的，注意要修改数据库、表、字段的编码。  
具体的命令请参考[mysql修改表、字段、库的字符集][1]
参考文章：  
[Linux平台下修正MySQL中文乱码问题][2]

 [1]: http://fatkun.com/2011/05/mysql-alter-charset.html
 [2]: http://www.linuxidc.com/Linux/2008-05/13128.htm