---
title: 使用json-lib遍历数组与对象（JSONArray与JSONObject）
author: fatkun
type: post
date: 2010-07-18T06:55:31+00:00
url: /2010/07/jsonarray-jsonobject-array.html
views:
  - 40
duoshuo_thread_id:
  - 6300408751060943617
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:5023:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #666666; font-style: italic;">//遍历json数组</span>
    <span style="color: #003399;">String</span> json1 <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;{data:[{name:'Wallace'},{name:'Grommit'}]}&quot;</span><span style="color: #339933;">;</span>
    jsonObjSplit <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> JSONObject<span style="color: #009900;">&#40;</span>json1<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    JSONArray ja <span style="color: #339933;">=</span> jsonObjSplit.<span style="color: #006633;">getJSONArray</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;data&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> i <span style="color: #339933;">=</span> <span style="color: #cc66cc;">0</span><span style="color: #339933;">;</span> i <span style="color: #339933;">&lt;</span> ja.<span style="color: #006633;">length</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> i<span style="color: #339933;">++</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    JSONObject jo <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span>JSONObject<span style="color: #009900;">&#41;</span> ja.<span style="color: #006633;">get</span><span style="color: #009900;">&#40;</span>i<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>jo.<span style="color: #006633;">get</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;name&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #666666; font-style: italic;">//JSONObject遍历json对象</span>
    <span style="color: #003399;">String</span> json2 <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;{name:'Wallace',age:15}&quot;</span><span style="color: #339933;">;</span>
    jsonObj <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> JSONObject<span style="color: #009900;">&#40;</span>json2<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">Iterator</span> iter <span style="color: #339933;">=</span> jsonObj.<span style="color: #006633;">keys</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> iter.<span style="color: #006633;">hasNext</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #003399;">String</span> key <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span><span style="color: #009900;">&#41;</span>iter.<span style="color: #006633;">next</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>jsonObj .<span style="color: #006633;">getString</span><span style="color: #009900;">&#40;</span><span style="color: #003399;">Key</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    ｝</pre></td></tr></table><p class="theCode" style="display:none;">//遍历json数组
    String json1 = &quot;{data:[{name:'Wallace'},{name:'Grommit'}]}&quot;;
    jsonObjSplit = new JSONObject(json1);
    JSONArray ja = jsonObjSplit.getJSONArray(&quot;data&quot;);
    for (int i = 0; i &lt; ja.length(); i++) {
    JSONObject jo = (JSONObject) ja.get(i);
    System.out.println(jo.get(&quot;name&quot;));
    }
    
    //JSONObject遍历json对象
    String json2 = &quot;{name:'Wallace',age:15}&quot;;
    jsonObj = new JSONObject(json2);
    
    for (Iterator iter = jsonObj.keys(); iter.hasNext();) {
    String key = (String)iter.next();
    System.out.println(jsonObj .getString(Key));
    ｝</p></div>
    ";}
categories:
  - J2EE
tags:
  - JSONArray
  - JSONObject
  - 遍历数组

---
<p style="padding: 0px; margin: 0px;">  使用json-lib遍历数组与对象</p>
<pre escaped="true" lang="java">//遍历json数组
String json1 = "{data:[{name:'Wallace'},{name:'Grommit'}]}";
jsonObjSplit = new JSONObject(json1);
JSONArray ja = jsonObjSplit.getJSONArray("data");
for (int i = 0; i &lt; ja.length(); i++) {
JSONObject jo = (JSONObject) ja.get(i);
System.out.println(jo.get("name"));
}

//JSONObject遍历json对象
String json2 = "{name:'Wallace',age:15}";
jsonObj = new JSONObject(json2);

for (Iterator iter = jsonObj.keys(); iter.hasNext();) {
String key = (String)iter.next();
System.out.println(jsonObj .getString(Key));
｝</pre>
<p style="padding: 0px; margin: 0px;">