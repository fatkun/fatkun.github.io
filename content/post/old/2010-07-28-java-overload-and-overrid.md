---
title: Java的重载(Overload)与重写(Override)
author: fatkun
type: post
date: 2010-07-28T14:10:25+00:00
url: /2010/07/java-overload-and-overrid.html
views:
  - 22
duoshuo_thread_id:
  - 6300408757952185090
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:7445:"
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
    14
    15
    16
    17
    18
    19
    20
    21
    22
    23
    24
    25
    26
    27
    28
    29
    30
    31
    32
    33
    34
    35
    36
    37
    38
    </pre></td><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">package</span> <span style="color: #006699;">com.fatkun</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #008000; font-style: italic; font-weight: bold;">/**
     * Overloading（重载，过载）
     * 方法名相同，参数类型不同或者参数类型顺序不同
     * 返回值，访问修饰符，异常可以不一样
     * @author fatkun
     *
     */</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> Overloading <span style="color: #009900;">&#123;</span>
    &nbsp;
    	<span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">int</span> test<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#123;</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;test1&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #000000; font-weight: bold;">return</span> <span style="color: #cc66cc;">1</span><span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span>
    &nbsp;
    	<span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> test<span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> a<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#123;</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;test2&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span>	
    &nbsp;
    	<span style="color: #666666; font-style: italic;">//以下两个参数类型顺序不同</span>
    	<span style="color: #000000; font-weight: bold;">public</span> <span style="color: #003399;">String</span> test<span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> a,<span style="color: #003399;">String</span> s<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#123;</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;test3&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #000000; font-weight: bold;">return</span> <span style="color: #0000ff;">&quot;returntest3&quot;</span><span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span>	
    &nbsp;
    	<span style="color: #000000; font-weight: bold;">public</span> <span style="color: #003399;">String</span> test<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> s,<span style="color: #000066; font-weight: bold;">int</span> a<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#123;</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;test4&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #000000; font-weight: bold;">return</span> <span style="color: #0000ff;">&quot;returntest4&quot;</span><span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span>	
    &nbsp;
    	<span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000066; font-weight: bold;">void</span> main<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> args<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#123;</span>
    		Overloading o <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> Overloading<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>o.<span style="color: #006633;">test</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		o.<span style="color: #006633;">test</span><span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">1</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>o.<span style="color: #006633;">test</span><span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">1</span>,<span style="color: #0000ff;">&quot;test3&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>o.<span style="color: #006633;">test</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;test4&quot;</span>,<span style="color: #cc66cc;">1</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">package com.fatkun;
    
    /**
     * Overloading（重载，过载）
     * 方法名相同，参数类型不同或者参数类型顺序不同
     * 返回值，访问修饰符，异常可以不一样
     * @author fatkun
     *
     */
    public class Overloading {
    
    	public int test(){
    		System.out.println(&quot;test1&quot;);
    		return 1;
    	}
    
    	public void test(int a){
    		System.out.println(&quot;test2&quot;);
    	}	
    
    	//以下两个参数类型顺序不同
    	public String test(int a,String s){
    		System.out.println(&quot;test3&quot;);
    		return &quot;returntest3&quot;;
    	}	
    
    	public String test(String s,int a){
    		System.out.println(&quot;test4&quot;);
    		return &quot;returntest4&quot;;
    	}	
    
    	public static void main(String[] args){
    		Overloading o = new Overloading();
    		System.out.println(o.test());
    		o.test(1);
    		System.out.println(o.test(1,&quot;test3&quot;));
    		System.out.println(o.test(&quot;test4&quot;,1));
    	}</p></div>
    ";i:2;s:4036:"
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
    14
    15
    16
    17
    18
    19
    20
    21
    22
    23
    24
    25
    26
    </pre></td><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">package</span> <span style="color: #006699;">com.fatkun</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #008000; font-style: italic; font-weight: bold;">/**
     * Overriding(重写，覆盖)
     * 重写是子类继承父类对父类的方法进行修改。方法名，参数，返回值必须一样。
     * 访问级别的限制性和异常不能比被重写的方法强
     * @author fatkun
     *
     */</span>
    <span style="color: #000000; font-weight: bold;">class</span> TestClass <span style="color: #009900;">&#123;</span>
    	<span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> test<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#123;</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;这是TestClass的test方法&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> Overriding <span style="color: #000000; font-weight: bold;">extends</span> TestClass <span style="color: #009900;">&#123;</span>
    &nbsp;
    	<span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000066; font-weight: bold;">void</span> main<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> args<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    		<span style="color: #000000; font-weight: bold;">new</span> Overriding<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">test</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span>
    &nbsp;
    	@Override
    	<span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> test<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;这是Overriding的test方法，重写了TestClass中的方法&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">package com.fatkun;
    
    /**
     * Overriding(重写，覆盖)
     * 重写是子类继承父类对父类的方法进行修改。方法名，参数，返回值必须一样。
     * 访问级别的限制性和异常不能比被重写的方法强
     * @author fatkun
     *
     */
    class TestClass {
    	public void test(){
    		System.out.println(&quot;这是TestClass的test方法&quot;);
    	}
    }
    
    public class Overriding extends TestClass {
    
    	public static void main(String[] args) {
    		new Overriding().test();
    	}
    
    	@Override
    	public void test() {
    		System.out.println(&quot;这是Overriding的test方法，重写了TestClass中的方法&quot;);
    	}
    }</p></div>
    ";}
categories:
  - 未分类
tags:
  - java基础
  - Thinking in Java 读书笔记

---
## 重载与重写之间的差别

<table border="0" cellspacing="0" cellpadding="0" width="492">  <tr>    <td width="72">      <p align="left">        <strong>区别点</strong>      </p>    </td>
    <td width="80">      <p align="left">        <strong>重载方法</strong> <strong> </strong>      </p>    </td>
    <td width="340">      <p align="left">        <strong>重写方法</strong>      </p>    </td>  </tr>
  <tr>    <td width="72">      <p align="left">        参数列表      </p>    </td>
    <td width="80">      <p align="left">        必须修改      </p>    </td>
    <td width="340">      <p align="left">        一定不能修改      </p>    </td>  </tr>
  <tr>    <td width="72">      <p align="left">        返回类型      </p>    </td>
    <td width="80">      <p align="left">        可以修改      </p>    </td>
    <td width="340">      <p align="left">        一定不能修改      </p>    </td>  </tr>
  <tr>    <td width="72">      <p align="left">        异常      </p>    </td>
    <td width="80">      <p align="left">        可以修改      </p>    </td>
    <td width="340">      <p align="left">        可以减少或删除，一定不能抛出新的或者更广的异常      </p>    </td>  </tr>
  <tr>    <td width="72">      <p align="left">        访问      </p>    </td>
    <td width="80">      <p align="left">        可以修改      </p>    </td>
    <td width="340">      <p align="left">        一定不能做更严格的限制（可以降低限制）      </p>    </td>  </tr></table>
## 重载（Overload）

<p align="left">  每个重载的方法（或者构造函数）都必须有一个独一无二的参数类型列表。<br /> 只能重载构造函数<br /> 规则</p>
  * 被重载的方法**<span style="text-decoration: underline;">必须</span>**改变参数列表；
  * 被重载的方法**可以**改变返回类型；
  * 被重载的方法**可以**改变访问修饰符；
  * 被重载的方法**可以**声明新的或更广的检查异常；
  * 方法能够在同一个类中或者在一个子类中被重载。
<pre escaped="true" lang="java" line="1">package com.fatkun;

/**
 * Overloading（重载，过载）
 * 方法名相同，参数类型不同或者参数类型顺序不同
 * 返回值，访问修饰符，异常可以不一样
 * @author fatkun
 *
 */
public class Overloading {

	public int test(){
		System.out.println("test1");
		return 1;
	}

	public void test(int a){
		System.out.println("test2");
	}	

	//以下两个参数类型顺序不同
	public String test(int a,String s){
		System.out.println("test3");
		return "returntest3";
	}	

	public String test(String s,int a){
		System.out.println("test4");
		return "returntest4";
	}	

	public static void main(String[] args){
		Overloading o = new Overloading();
		System.out.println(o.test());
		o.test(1);
		System.out.println(o.test(1,"test3"));
		System.out.println(o.test("test4",1));
	}</pre>
## 重写（Override）

<p align="left">  能够在需要新的子类特有行为时重新在子类中定义方法。<br /> 规则</p>
  * 参数列表**<span style="text-decoration: underline;">必须完全</span>**与被重写方法的相同；
  * 返回类型**<span style="text-decoration: underline;">必须完全</span>**与被重写方法的返回类型相同；
  * 访问级别的限制性**一定不能**比被重写方法的强；
  * 访问级别的限制性可以比被重写方法的弱；
  * 重写方法**一定不能抛出新的检查异常或比被重写的方法声明的检查异常更广泛**的检查异常
  * 重写的方法能够抛出更少或更有限的异常（也就是说，被重写的方法声明了异常，但重写的方法可以什么也不声明）
  * **不能重写被标示为****final****的方法**；
  * 如果不能继承一个方法，则不能重写这个方法。
<pre escaped="true" lang="java" line="1">package com.fatkun;

/**
 * Overriding(重写，覆盖)
 * 重写是子类继承父类对父类的方法进行修改。方法名，参数，返回值必须一样。
 * 访问级别的限制性和异常不能比被重写的方法强
 * @author fatkun
 *
 */
class TestClass {
	public void test(){
		System.out.println("这是TestClass的test方法");
	}
}

public class Overriding extends TestClass {

	public static void main(String[] args) {
		new Overriding().test();
	}

	@Override
	public void test() {
		System.out.println("这是Overriding的test方法，重写了TestClass中的方法");
	}
}</pre>
## 调用

重载方法：  
参数类型决定选择哪个重载版本（根据声明的参数类型），这发生在编译时。被调用的实际方法仍是发生在运行时期的虚拟方法调用。但是编译器已经知道所调用的方法的签名。因此，在运行时期，参数匹配已经明确，只是还不知道该方法所在的实际类。  
重写方法：  
对象类型（即：堆上实际实例的类型决定调用选择哪个方法，这发生在运行时期）
文章来源:<http://chen1984.javaeye.com/blog/353342> 代码来源:fatkun