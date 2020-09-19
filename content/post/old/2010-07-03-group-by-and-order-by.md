---
title: 如何在SQL中先排序后分组
author: fatkun
type: post
date: 2010-07-03T13:50:44+00:00
url: /2010/07/group-by-and-order-by.html
views:
  - 17
duoshuo_thread_id:
  - 6300408743964181249
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:728:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;"><span style="color: #993333; font-weight: bold;">SELECT</span> <span style="color: #66cc66;">*</span> <span style="color: #993333; font-weight: bold;">FROM</span> feed <span style="color: #993333; font-weight: bold;">GROUP</span> <span style="color: #993333; font-weight: bold;">BY</span> userid <span style="color: #993333; font-weight: bold;">ORDER</span> <span style="color: #993333; font-weight: bold;">BY</span> <span style="color: #993333; font-weight: bold;">TIME</span></pre></td></tr></table><p class="theCode" style="display:none;">select * from feed group by userid order by time</p></div>
    ";i:2;s:1283:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;"><span style="color: #993333; font-weight: bold;">SELECT</span> <span style="color: #66cc66;">*</span> <span style="color: #993333; font-weight: bold;">FROM</span>
    <span style="color: #66cc66;">&#40;</span><span style="color: #993333; font-weight: bold;">SELECT</span> <span style="color: #66cc66;">*</span> <span style="color: #993333; font-weight: bold;">FROM</span> feed <span style="color: #993333; font-weight: bold;">ORDER</span> <span style="color: #993333; font-weight: bold;">BY</span> <span style="color: #993333; font-weight: bold;">TIME</span><span style="color: #66cc66;">&#41;</span> <span style="color: #993333; font-weight: bold;">AS</span> T 
    <span style="color: #993333; font-weight: bold;">GROUP</span> <span style="color: #993333; font-weight: bold;">BY</span> T<span style="color: #66cc66;">.</span>userid <span style="color: #993333; font-weight: bold;">ORDER</span> <span style="color: #993333; font-weight: bold;">BY</span> T<span style="color: #66cc66;">.</span>time</pre></td></tr></table><p class="theCode" style="display:none;">select * from
    (select * from feed order by time) as T 
    group by T.userid order by T.time</p></div>
    ";i:3;s:876:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;"><span style="color: #993333; font-weight: bold;">SELECT</span> <span style="color: #66cc66;">*</span> <span style="color: #993333; font-weight: bold;">FROM</span> feed <span style="color: #993333; font-weight: bold;">GROUP</span> <span style="color: #993333; font-weight: bold;">BY</span> userid <span style="color: #993333; font-weight: bold;">ORDER</span> <span style="color: #993333; font-weight: bold;">BY</span> <span style="color: #993333; font-weight: bold;">MAX</span><span style="color: #66cc66;">&#40;</span><span style="color: #993333; font-weight: bold;">TIME</span><span style="color: #66cc66;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">select * from feed group by userid order by max(time)</p></div>
    ";}
categories:
  - 数据库
tags:
  - group by
  - hibernate子查询
  - order by

---
标题说的有点奇怪，换句话说是让order by比group by先执行。还不明白对吧？  
举个例子：实现场景，要实现QQ空间的动态消息，首先要按最新的消息查到QQ好友排序，然后再按好友分别查询他们的动态消息
有如下的Feed表
<pre>id	userid	type		msg	who	time
1	2	add_twitter		hahah	1	2010-04-27 19:12:38
2	2	add_twitter		怎么啦	2	2010-04-27 19:12:44
3	4	add_twitter		asddas	3	2010-04-27 19:20:26
4	2	reply_twitter		放大法	4	2010-04-27 19:24:09
5	5	reply_twitter		噶	5	2010-04-27 19:24:13
6	3	add_twitter		saf	6	2010-04-27 19:35:48
7	2	add_twitter		先谢谢谢谢谢谢	7	2010-04-27 19:54:44</pre>
现在想要，按时间先后，把用户的id查询出来，每个id只出现一次。
当然，第一时间就想到用group by语句来分组嘛
<pre escaped="true" lang="sql">select * from feed group by userid order by time</pre>
可是，得到的结果并不是自己想要的，group by比order by先解析了，结果就是得到最旧的那一条。
## 正确的方法

使用子查询
<pre escaped="true" lang="sql">select * from
(select * from feed order by time) as T 
group by T.userid order by T.time</pre>
上面这句在mysql可以正常取值，但是在hibernate不能使用from 后面的子查询，杯具。。  
换个折中的方法，以下方法只是为了取得userid而已
<pre escaped="true" lang="sql">select * from feed group by userid order by max(time)</pre>