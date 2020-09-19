---
title: MSSQL存储过程的用法：基础
author: fatkun
type: post
date: 2009-09-16T08:23:59+00:00
url: /2009/09/mssql-store-procedure.html
views:
  - 1
duoshuo_thread_id:
  - 6300408667711750913
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:1043:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;"><span style="color: #993333; font-weight: bold;">CREATE</span> <span style="color: #993333; font-weight: bold;">PROCEDURE</span> update_createtime
    @tbID <span style="color: #993333; font-weight: bold;">INT</span>
    <span style="color: #993333; font-weight: bold;">AS</span>
        <span style="color: #993333; font-weight: bold;">UPDATE</span> t_member <span style="color: #993333; font-weight: bold;">SET</span> createTime <span style="color: #66cc66;">=</span> GetDate<span style="color: #66cc66;">&#40;</span><span style="color: #66cc66;">&#41;</span> <span style="color: #993333; font-weight: bold;">WHERE</span> tbID <span style="color: #66cc66;">=</span> @tbID
    <span style="color: #993333; font-weight: bold;">GO</span></pre></td></tr></table><p class="theCode" style="display:none;">Create procedure update_createtime
    @tbID int
    as
        update t_member set createTime = GetDate() where tbID = @tbID
    go</p></div>
    ";i:2;s:2240:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;"><span style="color: #808080; font-style: italic;">--Developer:zhihui Zhou</span>
    <span style="color: #808080; font-style: italic;">--Date：New（）as 2008-10-18</span>
    <span style="color: #808080; font-style: italic;">--Email：zhou5791759@163.com</span>
    <span style="color: #808080; font-style: italic;">--QQ:297510342</span>
    &nbsp;
    <span style="color: #993333; font-weight: bold;">CREATE</span> <span style="color: #993333; font-weight: bold;">PROCEDURE</span> update_createtime
    @tbID <span style="color: #993333; font-weight: bold;">INT</span><span style="color: #66cc66;">,</span>
    @createTime nvarchar<span style="color: #66cc66;">&#40;</span><span style="color: #cc66cc;">50</span><span style="color: #66cc66;">&#41;</span> output
    <span style="color: #993333; font-weight: bold;">AS</span>
        <span style="color: #993333; font-weight: bold;">UPDATE</span> t_member <span style="color: #993333; font-weight: bold;">SET</span> createTime <span style="color: #66cc66;">=</span> GetDate<span style="color: #66cc66;">&#40;</span><span style="color: #66cc66;">&#41;</span> <span style="color: #993333; font-weight: bold;">WHERE</span> tbID <span style="color: #66cc66;">=</span> @tbID
        <span style="color: #993333; font-weight: bold;">SET</span> @createTime <span style="color: #66cc66;">=</span> <span style="color: #66cc66;">&#40;</span><span style="color: #993333; font-weight: bold;">SELECT</span> createTime <span style="color: #993333; font-weight: bold;">FROM</span> t_member <span style="color: #993333; font-weight: bold;">WHERE</span> tbID <span style="color: #66cc66;">=</span> @tbID<span style="color: #66cc66;">&#41;</span>
    <span style="color: #993333; font-weight: bold;">GO</span></pre></td></tr></table><p class="theCode" style="display:none;">--Developer:zhihui Zhou
    --Date：New（）as 2008-10-18
    --Email：zhou5791759@163.com
    --QQ:297510342
    
    Create procedure update_createtime
    @tbID int,
    @createTime nvarchar(50) output
    as
        update t_member set createTime = GetDate() where tbID = @tbID
        set @createTime = (select createTime from t_member where tbID = @tbID)
    go</p></div>
    ";i:3;s:921:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;"><span style="color: #808080; font-style: italic;">--Call SQL in the method for</span>
    <span style="color: #808080; font-style: italic;">--start</span>
    <span style="color: #993333; font-weight: bold;">DECLARE</span> @createTime nvarchar<span style="color: #66cc66;">&#40;</span><span style="color: #cc66cc;">50</span><span style="color: #66cc66;">&#41;</span>
    <span style="color: #993333; font-weight: bold;">EXEC</span> update_createTime <span style="color: #cc66cc;">1</span><span style="color: #66cc66;">,</span>@createTime output
    <span style="color: #808080; font-style: italic;">--end</span></pre></td></tr></table><p class="theCode" style="display:none;">--Call SQL in the method for
    --start
    declare @createTime nvarchar(50)
    exec update_createTime 1,@createTime output
    --end</p></div>
    ";}
categories:
  - 数据库

---
## 创建存储过程的基本格式：

<pre escaped="true" lang="sql">Create procedure update_createtime
@tbID int
as
    update t_member set createTime = GetDate() where tbID = @tbID
go</pre>
## 添加返回值时就可以这样做

<pre escaped="true" lang="sql">--Developer:zhihui Zhou
--Date：New（）as 2008-10-18
--Email：zhou5791759@163.com
--QQ:297510342

Create procedure update_createtime
@tbID int,
@createTime nvarchar(50) output
as
    update t_member set createTime = GetDate() where tbID = @tbID
    set @createTime = (select createTime from t_member where tbID = @tbID)
go</pre>
## 执行这个存储过程：

<pre escaped="true" lang="sql">--Call SQL in the method for
--start
declare @createTime nvarchar(50)
exec update_createTime 1,@createTime output
--end</pre>
来源：<http://www.cnblogs.com/zhou5791759/archive/2008/10/19/1314292.html>