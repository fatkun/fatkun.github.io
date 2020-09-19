---
title: Ext.encode与Ext.decode的JSON转换
author: fatkun
type: post
date: 2011-05-14T13:51:30+00:00
url: /2011/05/ext-encode-and-decode.html
duoshuo_thread_id:
  - 6300408813975503618
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:2969:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="javascript" style="font-family:monospace;"><span style="color: #000066; font-weight: bold;">var</span> arr <span style="color: #339933;">=</span> <span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span>
    <span style="color: #000066; font-weight: bold;">var</span> field1 <span style="color: #339933;">=</span> <span style="color: #009900;">&#123;</span><span style="color: #009900;">&#125;</span><span style="color: #339933;">;</span>
    field1<span style="color: #009900;">&#91;</span><span style="color: #3366CC;">'name'</span><span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> <span style="color: #3366CC;">'fatkun'</span><span style="color: #339933;">;</span>
    field1<span style="color: #009900;">&#91;</span><span style="color: #3366CC;">'age'</span><span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> <span style="color: #CC0000;">23</span><span style="color: #339933;">;</span>
    <span style="color: #000066; font-weight: bold;">var</span> field2 <span style="color: #339933;">=</span> <span style="color: #009900;">&#123;</span><span style="color: #009900;">&#125;</span><span style="color: #339933;">;</span>
    field2<span style="color: #009900;">&#91;</span><span style="color: #3366CC;">'name'</span><span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> <span style="color: #3366CC;">'test'</span><span style="color: #339933;">;</span>
    field2<span style="color: #009900;">&#91;</span><span style="color: #3366CC;">'age'</span><span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> <span style="color: #CC0000;">24</span><span style="color: #339933;">;</span>
    arr.<span style="color: #660066;">push</span><span style="color: #009900;">&#40;</span>field1<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    arr.<span style="color: #660066;">push</span><span style="color: #009900;">&#40;</span>field2<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    Ext.<span style="color: #660066;">encode</span><span style="color: #009900;">&#40;</span>arr<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #006600; font-style: italic;">//返回结果&quot;[{&quot;name&quot;:&quot;fatkun&quot;,&quot;age&quot;:23},{&quot;name&quot;:&quot;test&quot;,&quot;age&quot;:24}]&quot;</span></pre></td></tr></table><p class="theCode" style="display:none;">var arr = [];
    var field1 = {};
    field1['name'] = 'fatkun';
    field1['age'] = 23;
    var field2 = {};
    field2['name'] = 'test';
    field2['age'] = 24;
    arr.push(field1);
    arr.push(field2);
    Ext.encode(arr);
    //返回结果&quot;[{&quot;name&quot;:&quot;fatkun&quot;,&quot;age&quot;:23},{&quot;name&quot;:&quot;test&quot;,&quot;age&quot;:24}]&quot;</p></div>
    ";}
categories:
  - 网页前端
tags:
  - decode
  - encode
  - extjs

---
在Extjs中，我们可以通过json来交换数据，Extjs内置了两个方法来互相转换。
## Ext.decode( String json ) : Object

把json字符串转换为对象
## Ext.encode( Mixed o ) : String

把对象转换为字符串，用这个方法可以在ajax提交时返回数据
<pre escaped="true" lang="javascript">var arr = [];
var field1 = {};
field1['name'] = 'fatkun';
field1['age'] = 23;
var field2 = {};
field2['name'] = 'test';
field2['age'] = 24;
arr.push(field1);
arr.push(field2);
Ext.encode(arr);
//返回结果"[{"name":"fatkun","age":23},{"name":"test","age":24}]"</pre>