---
title: java变量的作用域
author: fatkun
type: post
date: 2010-07-27T06:37:38+00:00
url: /2010/07/the-scope-of-variables.html
views:
  - 8
duoshuo_thread_id:
  - 6300408751350350593
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:3213:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="line_numbers"><pre>1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13
    </pre></td><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> OneClass <span style="color: #009900;">&#123;</span>
    	<span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000066; font-weight: bold;">int</span> x<span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//会赋值默认值0</span>
    	<span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000066; font-weight: bold;">void</span> main<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> args<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#123;</span>
    		<span style="color: #666666; font-style: italic;">//int x = 2;</span>
    		<span style="color: #666666; font-style: italic;">//不能在同一个方法内定义同一个变量，不然会报错 Duplicate local variable x</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;第一个x:&quot;</span><span style="color: #339933;">+</span>x<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #009900;">&#123;</span>
    			<span style="color: #000066; font-weight: bold;">int</span> x <span style="color: #339933;">=</span> <span style="color: #cc66cc;">5</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//在方法内的变量必须初始化，否则x会是随机值而不是0</span>
    			<span style="color: #666666; font-style: italic;">//如果不赋值会报错The local variable x may not have been initialized</span>
    			<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;第二个x:&quot;</span><span style="color: #339933;">+</span>x<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #009900;">&#125;</span>
    	<span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">public class OneClass {
    	static int x;//会赋值默认值0
    	public static void main(String[] args){
    		//int x = 2;
    		//不能在同一个方法内定义同一个变量，不然会报错 Duplicate local variable x
    		System.out.println(&quot;第一个x:&quot;+x);
    		{
    			int x = 5;//在方法内的变量必须初始化，否则x会是随机值而不是0
    			//如果不赋值会报错The local variable x may not have been initialized
    			System.out.println(&quot;第二个x:&quot;+x);
    		}
    	}
    }</p></div>
    ";}
categories:
  - J2EE
tags:
  - java基础

---
<pre escaped="true" lang="java" line="1">public class OneClass {
	static int x;//会赋值默认值0
	public static void main(String[] args){
		//int x = 2;
		//不能在同一个方法内定义同一个变量，不然会报错 Duplicate local variable x
		System.out.println("第一个x:"+x);
		{
			int x = 5;//在方法内的变量必须初始化，否则x会是随机值而不是0
			//如果不赋值会报错The local variable x may not have been initialized
			System.out.println("第二个x:"+x);
		}
	}
}
</pre>