---
title: Java的访问控制
author: fatkun
type: post
date: 2010-07-30T09:00:55+00:00
url: /2010/07/java-access.html
views:
  - 47
duoshuo_thread_id:
  - 6300408758015099650
wp-syntax-cache-content:
  - |
    a:4:{i:1;s:4402:"
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
    </pre></td><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #666666; font-style: italic;">//PackageClass.java</span>
    <span style="color: #000000; font-weight: bold;">package</span> <span style="color: #006699;">com.fatkun.util</span><span style="color: #339933;">;</span>
    <span style="color: #008000; font-style: italic; font-weight: bold;">/**
     * 在包com.fatkun.util内，分别有a,b,c,d四个变量，它们的修饰符都不一样。
     * @author fatkun
     *
     */</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> PackageClass <span style="color: #009900;">&#123;</span>
    	<span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000066; font-weight: bold;">int</span> a<span style="color: #339933;">;</span>
    	<span style="color: #000066; font-weight: bold;">int</span> b<span style="color: #339933;">;</span>
    	<span style="color: #000000; font-weight: bold;">protected</span> <span style="color: #000066; font-weight: bold;">int</span> c<span style="color: #339933;">;</span>
    	<span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">int</span> d<span style="color: #339933;">;</span>
    &nbsp;
    	<span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000066; font-weight: bold;">void</span> main<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> args<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    		PackageClass p <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> PackageClass<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>p.<span style="color: #006633;">a</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>p.<span style="color: #006633;">b</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>p.<span style="color: #006633;">c</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>p.<span style="color: #006633;">d</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
    		<span style="color: #000000; font-weight: bold;">new</span> InsideClass<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #009900;">&#125;</span>
    <span style="color: #000000; font-weight: bold;">class</span> InsideClass <span style="color: #009900;">&#123;</span>
    &nbsp;
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">//PackageClass.java
    package com.fatkun.util;
    /**
     * 在包com.fatkun.util内，分别有a,b,c,d四个变量，它们的修饰符都不一样。
     * @author fatkun
     *
     */
    public class PackageClass {
    	private int a;
    	int b;
    	protected int c;
    	public int d;
    
    	public static void main(String[] args) {
    		PackageClass p = new PackageClass();
    		System.out.println(p.a);
    		System.out.println(p.b);
    		System.out.println(p.c);
    		System.out.println(p.d);
    
    		new InsideClass();
    	}
    
    }
    class InsideClass {
    
    }</p></div>
    ";i:2;s:3748:"
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
    </pre></td><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #666666; font-style: italic;">//AnotherPackageClass.java</span>
    <span style="color: #000000; font-weight: bold;">package</span> <span style="color: #006699;">com.fatkun.util</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #008000; font-style: italic; font-weight: bold;">/**
     * 同一个包内的类，private的不能访问
     * @author fatkun
     *
     */</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> AnotherPackageClass <span style="color: #009900;">&#123;</span>
    &nbsp;
    	<span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000066; font-weight: bold;">void</span> main<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> args<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#123;</span>
    		PackageClass p <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> PackageClass<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>p.<span style="color: #006633;">a</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//private只能在类内部访问</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>p.<span style="color: #006633;">b</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>p.<span style="color: #006633;">c</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>p.<span style="color: #006633;">d</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
    		<span style="color: #666666; font-style: italic;">//内部类在同一个包内可以访问</span>
    		<span style="color: #000000; font-weight: bold;">new</span> InsideClass<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">//AnotherPackageClass.java
    package com.fatkun.util;
    
    /**
     * 同一个包内的类，private的不能访问
     * @author fatkun
     *
     */
    public class AnotherPackageClass {
    
    	public static void main(String[] args){
    		PackageClass p = new PackageClass();
    		System.out.println(p.a);//private只能在类内部访问
    		System.out.println(p.b);
    		System.out.println(p.c);
    		System.out.println(p.d);
    
    		//内部类在同一个包内可以访问
    		new InsideClass();
    	}
    
    }</p></div>
    ";i:3;s:3998:"
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
    </pre></td><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #666666; font-style: italic;">//ExtendClass.java</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">com.fatkun.util.*</span><span style="color: #339933;">;</span>
    <span style="color: #008000; font-style: italic; font-weight: bold;">/**
     * PackageClass的子类
     * @author fatkun
     *
     */</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> ExtendClass <span style="color: #000000; font-weight: bold;">extends</span> PackageClass <span style="color: #009900;">&#123;</span>
    &nbsp;
    	<span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000066; font-weight: bold;">void</span> main<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> args<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    		ExtendClass e <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> ExtendClass<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>e.<span style="color: #006633;">a</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//private只能在类内部访问</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>e.<span style="color: #006633;">b</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//default只能在类内部和同一个包内访问</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>e.<span style="color: #006633;">c</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//protect能在子类访问</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>e.<span style="color: #006633;">d</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
    		<span style="color: #666666; font-style: italic;">//内部类在子类不可以访问</span>
    		<span style="color: #000000; font-weight: bold;">new</span> InsideClass<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">//ExtendClass.java
    import com.fatkun.util.*;
    /**
     * PackageClass的子类
     * @author fatkun
     *
     */
    public class ExtendClass extends PackageClass {
    
    	public static void main(String[] args) {
    		ExtendClass e = new ExtendClass();
    		System.out.println(e.a);//private只能在类内部访问
    		System.out.println(e.b);//default只能在类内部和同一个包内访问
    		System.out.println(e.c);//protect能在子类访问
    		System.out.println(e.d);
    
    		//内部类在子类不可以访问
    		new InsideClass();
    	}
    }</p></div>
    ";i:4;s:4095:"
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
    </pre></td><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #666666; font-style: italic;">//DefaultClass.java</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">com.fatkun.util.*</span><span style="color: #339933;">;</span>
    <span style="color: #008000; font-style: italic; font-weight: bold;">/**
     * 不同包内
     * @author fatkun
     *
     */</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> DefaultClass <span style="color: #009900;">&#123;</span>
    &nbsp;
    	<span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000066; font-weight: bold;">void</span> main<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> args<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    		PackageClass p <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> PackageClass<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>p.<span style="color: #006633;">a</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//private只能在类内部访问</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>p.<span style="color: #006633;">b</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//default只能在类内部和同一个包内访问</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>p.<span style="color: #006633;">c</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//protect只能在类内部、同一个包、子类访问</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>p.<span style="color: #006633;">d</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//public能在任何地方访问</span>
    &nbsp;
    		<span style="color: #666666; font-style: italic;">//内部类在不同包内不可以访问</span>
    		<span style="color: #000000; font-weight: bold;">new</span> InsideClass<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">//DefaultClass.java
    import com.fatkun.util.*;
    /**
     * 不同包内
     * @author fatkun
     *
     */
    public class DefaultClass {
    
    	public static void main(String[] args) {
    		PackageClass p = new PackageClass();
    		System.out.println(p.a);//private只能在类内部访问
    		System.out.println(p.b);//default只能在类内部和同一个包内访问
    		System.out.println(p.c);//protect只能在类内部、同一个包、子类访问
    		System.out.println(p.d);//public能在任何地方访问
    
    		//内部类在不同包内不可以访问
    		new InsideClass();
    	}
    
    }</p></div>
    ";}
categories:
  - J2EE
tags:
  - java基础
  - Thinking in Java 读书笔记
  - 权限

---
## 包（Package）

  1. 创建自己的包时，要求 package语句必须是文件中的第一个“非注释”代码。
  2. 如果类名冲突时，可这样写java.util.Vector v = new java.util.Vector();
  3. 可能（但并常见）有一个编译单元根本没有任何公共类。此时，可按自己的意愿任意指定文件名。
## 访问控制

<table border="0" cellspacing="0" cellpadding="0" width="584">  <tr>    <td width="105">      <p align="center">        <strong>修饰符</strong>      </p>    </td>
    <td width="139">      <p align="center">        <strong>类内部</strong>      </p>    </td>
    <td width="87">      <p align="center">        <strong>同一个包</strong>      </p>    </td>
    <td width="104">      <p align="center">        <strong>子类</strong>      </p>    </td>
    <td width="149">      <p align="center">        <strong>任何地方</strong>      </p>    </td>  </tr>
  <tr>    <td width="105">      <p align="center">        private      </p>    </td>
    <td width="139">      <p align="center">        √      </p>    </td>
    <td width="87">    </td>
    <td width="104">    </td>
    <td width="149">    </td>  </tr>
  <tr>    <td width="105">      <p align="center">        default      </p>    </td>
    <td width="139">      <p align="center">        √      </p>    </td>
    <td width="87">      <p align="center">        √      </p>    </td>
    <td width="104">    </td>
    <td width="149">    </td>  </tr>
  <tr>    <td width="105">      <p align="center">        protected      </p>    </td>
    <td width="139">      <p align="center">        √      </p>    </td>
    <td width="87">      <p align="center">        √      </p>    </td>
    <td width="104">      <p align="center">        √      </p>    </td>
    <td width="149">    </td>  </tr>
  <tr>    <td width="105">      <p align="center">        public      </p>    </td>
    <td width="139">      <p align="center">        √      </p>    </td>
    <td width="87">      <p align="center">        √      </p>    </td>
    <td width="104">      <p align="center">        √      </p>    </td>
    <td width="149">      <p align="center">        √      </p>    </td>  </tr></table>
类的修饰符只有public 和 default，默认时只能被同一个文件或包内访问。
<!--more-->

**下面是代码解释**
<pre escaped="true" lang="java" line="1">//PackageClass.java
package com.fatkun.util;
/**
 * 在包com.fatkun.util内，分别有a,b,c,d四个变量，它们的修饰符都不一样。
 * @author fatkun
 *
 */
public class PackageClass {
	private int a;
	int b;
	protected int c;
	public int d;

	public static void main(String[] args) {
		PackageClass p = new PackageClass();
		System.out.println(p.a);
		System.out.println(p.b);
		System.out.println(p.c);
		System.out.println(p.d);

		new InsideClass();
	}

}
class InsideClass {

}</pre>
<pre escaped="true" lang="java" line="1">//AnotherPackageClass.java
package com.fatkun.util;

/**
 * 同一个包内的类，private的不能访问
 * @author fatkun
 *
 */
public class AnotherPackageClass {

	public static void main(String[] args){
		PackageClass p = new PackageClass();
		System.out.println(p.a);//private只能在类内部访问
		System.out.println(p.b);
		System.out.println(p.c);
		System.out.println(p.d);

		//内部类在同一个包内可以访问
		new InsideClass();
	}

}</pre>
<pre escaped="true" lang="java" line="1">//ExtendClass.java
import com.fatkun.util.*;
/**
 * PackageClass的子类
 * @author fatkun
 *
 */
public class ExtendClass extends PackageClass {

	public static void main(String[] args) {
		ExtendClass e = new ExtendClass();
		System.out.println(e.a);//private只能在类内部访问
		System.out.println(e.b);//default只能在类内部和同一个包内访问
		System.out.println(e.c);//protect能在子类访问
		System.out.println(e.d);

		//内部类在子类不可以访问
		new InsideClass();
	}
}</pre>
<pre escaped="true" lang="java" line="1">//DefaultClass.java
import com.fatkun.util.*;
/**
 * 不同包内
 * @author fatkun
 *
 */
public class DefaultClass {

	public static void main(String[] args) {
		PackageClass p = new PackageClass();
		System.out.println(p.a);//private只能在类内部访问
		System.out.println(p.b);//default只能在类内部和同一个包内访问
		System.out.println(p.c);//protect只能在类内部、同一个包、子类访问
		System.out.println(p.d);//public能在任何地方访问

		//内部类在不同包内不可以访问
		new InsideClass();
	}

}</pre>