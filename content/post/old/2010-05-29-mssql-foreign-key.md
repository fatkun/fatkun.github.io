---
title: MSSQL多个外键对应同一个表时查询外键的内容
author: fatkun
type: post
date: 2010-05-29T04:11:05+00:00
url: /2010/05/mssql-foreign-key.html
duoshuo_thread_id:
  - 6300408725643461377
wp-syntax-cache-content:
  - |
    a:4:{i:1;s:569:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;">CityID	CityName
    <span style="color: #cc66cc;">1</span>	广州
    <span style="color: #cc66cc;">2</span>	湛江
    <span style="color: #cc66cc;">3</span>	江门
    <span style="color: #cc66cc;">4</span>	肇庆
    <span style="color: #cc66cc;">5</span>	惠州
    <span style="color: #cc66cc;">6</span>	汕头</pre></td></tr></table><p class="theCode" style="display:none;">CityID	CityName
    1	广州
    2	湛江
    3	江门
    4	肇庆
    5	惠州
    6	汕头</p></div>
    ";i:2;s:541:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;">CarID	CarName	StartCityID	EndCityID
    <span style="color: #cc66cc;">1</span>	G001	<span style="color: #cc66cc;">1</span>	<span style="color: #cc66cc;">2</span>
    <span style="color: #cc66cc;">2</span>	G002	<span style="color: #cc66cc;">1</span>	<span style="color: #cc66cc;">3</span></pre></td></tr></table><p class="theCode" style="display:none;">CarID	CarName	StartCityID	EndCityID
    1	G001	1	2
    2	G002	1	3</p></div>
    ";i:3;s:1098:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;"><span style="color: #993333; font-weight: bold;">SELECT</span> 始发站<span style="color: #66cc66;">=</span>c1<span style="color: #66cc66;">.</span>CityName<span style="color: #66cc66;">,</span>终点站<span style="color: #66cc66;">=</span>c2<span style="color: #66cc66;">.</span>CityName
    <span style="color: #993333; font-weight: bold;">FROM</span> car<span style="color: #66cc66;">,</span>City c1<span style="color: #66cc66;">,</span>City c2
    <span style="color: #993333; font-weight: bold;">WHERE</span> StartCityID <span style="color: #66cc66;">=</span> c1<span style="color: #66cc66;">.</span>CityID <span style="color: #993333; font-weight: bold;">AND</span> EndCityID <span style="color: #66cc66;">=</span> c2<span style="color: #66cc66;">.</span>CityID</pre></td></tr></table><p class="theCode" style="display:none;">SELECT 始发站=c1.CityName,终点站=c2.CityName
    FROM car,City c1,City c2
    WHERE StartCityID = c1.CityID AND EndCityID = c2.CityID</p></div>
    ";i:4;s:1149:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;"><span style="color: #993333; font-weight: bold;">SELECT</span> 始发站<span style="color: #66cc66;">=</span>c1<span style="color: #66cc66;">.</span>CityName<span style="color: #66cc66;">,</span>终点站<span style="color: #66cc66;">=</span>c2<span style="color: #66cc66;">.</span>CityName
    <span style="color: #993333; font-weight: bold;">FROM</span> car
    <span style="color: #993333; font-weight: bold;">JOIN</span> City c1 <span style="color: #993333; font-weight: bold;">ON</span> StartCityID <span style="color: #66cc66;">=</span> c1<span style="color: #66cc66;">.</span>CityID
    <span style="color: #993333; font-weight: bold;">JOIN</span> City c2 <span style="color: #993333; font-weight: bold;">ON</span> EndCityID <span style="color: #66cc66;">=</span> c2<span style="color: #66cc66;">.</span>CityID</pre></td></tr></table><p class="theCode" style="display:none;">SELECT 始发站=c1.CityName,终点站=c2.CityName
    FROM car
    join City c1 on StartCityID = c1.CityID
    join City c2 on EndCityID = c2.CityID</p></div>
    ";}
categories:
  - 数据库
tags:
  - join
  - sqlserver
  - 外键

---
当有一个表同时有多个外键同时指向某一个表时，需要通过外键来查询到相应的信息。
举个例子：这是一个订车票的
城市表
<pre escaped="true" lang="sql">CityID	CityName
1	广州
2	湛江
3	江门
4	肇庆
5	惠州
6	汕头
</pre>
车次表
<pre escaped="true" lang="sql">CarID	CarName	StartCityID	EndCityID
1	G001	1	2
2	G002	1	3</pre>
这里的StartCityID和EndCityID分别是城市表的外键
## 解决方法

现在要把对应的始发城市和终点城市的名称取到，mssql语句可以这样  
方法一：
<pre escaped="true" lang="sql">SELECT 始发站=c1.CityName,终点站=c2.CityName
FROM car,City c1,City c2
WHERE StartCityID = c1.CityID AND EndCityID = c2.CityID</pre>
方法二：
<pre escaped="true" lang="sql">SELECT 始发站=c1.CityName,终点站=c2.CityName
FROM car
join City c1 on StartCityID = c1.CityID
join City c2 on EndCityID = c2.CityID</pre>