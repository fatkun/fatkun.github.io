---
title: JAVA的==与Equals
author: fatkun
type: post
date: 2010-11-21T03:38:21+00:00
url: /2010/11/java-equals.html
duoshuo_thread_id:
  - 6300408777250177793
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:6690:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> TestEqual <span style="color: #009900;">&#123;</span>
    &nbsp;
    	<span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000066; font-weight: bold;">void</span> main<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> args<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    		<span style="color: #003399;">String</span> a <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;abc&quot;</span><span style="color: #339933;">;</span>
    		<span style="color: #003399;">String</span> b <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;abc&quot;</span><span style="color: #339933;">;</span>
    		<span style="color: #003399;">String</span> c <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">String</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;abc&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//新建了一个对象</span>
    		<span style="color: #003399;">String</span> d <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">String</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;abc&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #003399;">String</span> e <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;ab&quot;</span><span style="color: #339933;">+</span><span style="color: #0000ff;">&quot;c&quot;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//使用常量池中的对象</span>
    		<span style="color: #003399;">String</span> f <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;ab&quot;</span><span style="color: #339933;">;</span>
    		<span style="color: #003399;">String</span> g <span style="color: #339933;">=</span> f <span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot;c&quot;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//string是固定字符，需要新建对象</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>a <span style="color: #339933;">==</span> b<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//true，第一次a把字符串放在常量池，那b继续用这个常量，e也一样</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>a.<span style="color: #006633;">equals</span><span style="color: #009900;">&#40;</span>b<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//true</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;a == c?&quot;</span><span style="color: #339933;">+</span><span style="color: #009900;">&#40;</span>a <span style="color: #339933;">==</span> c<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//false</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>a.<span style="color: #006633;">equals</span><span style="color: #009900;">&#40;</span>c<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//true</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>c<span style="color: #339933;">==</span>d<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//false</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>a<span style="color: #339933;">==</span>e<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//true</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>a<span style="color: #339933;">==</span>g<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//false</span>
    	<span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">public class TestEqual {
    	
    	public static void main(String[] args) {
    		String a = &quot;abc&quot;;
    		String b = &quot;abc&quot;;
    		String c = new String(&quot;abc&quot;);//新建了一个对象
    		String d = new String(&quot;abc&quot;);
    		String e = &quot;ab&quot;+&quot;c&quot;;//使用常量池中的对象
    		String f = &quot;ab&quot;;
    		String g = f + &quot;c&quot;;//string是固定字符，需要新建对象
    		System.out.println(a == b);//true，第一次a把字符串放在常量池，那b继续用这个常量，e也一样
    		System.out.println(a.equals(b));//true
    		System.out.println(&quot;a == c?&quot;+(a == c));//false
    		System.out.println(a.equals(c));//true
    		System.out.println(c==d);//false
    		System.out.println(a==e);//true
    		System.out.println(a==g);//false
    	}
    }</p></div>
    ";i:2;s:8908:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> TestEqual <span style="color: #009900;">&#123;</span>
    &nbsp;
    	<span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000066; font-weight: bold;">void</span> main<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> args<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    		<span style="color: #003399;">Integer</span> i1 <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">Integer</span><span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">9</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> 
    		<span style="color: #003399;">Integer</span> i2 <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">Integer</span><span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">9</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> 
    		<span style="color: #000066; font-weight: bold;">int</span> i3 <span style="color: #339933;">=</span> <span style="color: #cc66cc;">9</span><span style="color: #339933;">;</span>
    		<span style="color: #000066; font-weight: bold;">int</span> i4 <span style="color: #339933;">=</span> <span style="color: #cc66cc;">9</span><span style="color: #339933;">;</span>
    		<span style="color: #003399;">Integer</span> i5 <span style="color: #339933;">=</span> <span style="color: #cc66cc;">9</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//自动装箱(box)操作，基本类型int 9可以自动box成对象Integer</span>
    		<span style="color: #003399;">Integer</span> i6 <span style="color: #339933;">=</span> <span style="color: #cc66cc;">9</span><span style="color: #339933;">;</span>
    		<span style="color: #003399;">Long</span> long1 <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">Long</span><span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">9</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>i1<span style="color: #339933;">==</span>i2<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//false</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>i1<span style="color: #339933;">==</span>i3<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//true</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;i3==i4?&quot;</span><span style="color: #339933;">+</span><span style="color: #009900;">&#40;</span>i3<span style="color: #339933;">==</span>i4<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//true，常量池</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;i1==i3?&quot;</span><span style="color: #339933;">+</span><span style="color: #009900;">&#40;</span>i1<span style="color: #339933;">==</span>i3<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//true</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;i5==i6?&quot;</span><span style="color: #339933;">+</span><span style="color: #009900;">&#40;</span>i5<span style="color: #339933;">==</span>i6<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//true，当-128&lt;i5&lt;127时为true，其他为false</span>
    		<span style="color: #666666; font-style: italic;">//http://blog.csdn.net/newsonglin/archive/2008/10/15/3079865.aspx</span>
    		<span style="color: #666666; font-style: italic;">// If the value p being boxed is true, false, a byte, a char in the range \u0000 to \u007f, or an int or short number between -128 and 127, then let r1 and r2 be the results of any two boxing conversions of p. It is always the case that r1 == r2.</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;i3==i5?&quot;</span><span style="color: #339933;">+</span><span style="color: #009900;">&#40;</span>i3<span style="color: #339933;">==</span>i5<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//false</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;i1==i5?&quot;</span><span style="color: #339933;">+</span><span style="color: #009900;">&#40;</span>i1<span style="color: #339933;">==</span>i5<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//false</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>i1.<span style="color: #006633;">equals</span><span style="color: #009900;">&#40;</span>i2<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//true，同类型比较值</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>i1.<span style="color: #006633;">equals</span><span style="color: #009900;">&#40;</span>long1<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//false，不同类型不进行比较</span>
    &nbsp;
    	<span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">public class TestEqual {
    	
    	public static void main(String[] args) {
    		Integer i1 = new Integer(9); 
    		Integer i2 = new Integer(9); 
    		int i3 = 9;
    		int i4 = 9;
    		Integer i5 = 9;//自动装箱(box)操作，基本类型int 9可以自动box成对象Integer
    		Integer i6 = 9;
    		Long long1 = new Long(9);
    		System.out.println(i1==i2);//false
    		System.out.println(i1==i3);//true
    		System.out.println(&quot;i3==i4?&quot;+(i3==i4));//true，常量池
    		System.out.println(&quot;i1==i3?&quot;+(i1==i3));//true
    		System.out.println(&quot;i5==i6?&quot;+(i5==i6));//true，当-128&lt;i5&lt;127时为true，其他为false
    		//http://blog.csdn.net/newsonglin/archive/2008/10/15/3079865.aspx
    		// If the value p being boxed is true, false, a byte, a char in the range \u0000 to \u007f, or an int or short number between -128 and 127, then let r1 and r2 be the results of any two boxing conversions of p. It is always the case that r1 == r2.
    		System.out.println(&quot;i3==i5?&quot;+(i3==i5));//false
    		System.out.println(&quot;i1==i5?&quot;+(i1==i5));//false
    		System.out.println(i1.equals(i2));//true，同类型比较值
    		System.out.println(i1.equals(long1));//false，不同类型不进行比较
    
    	}
    
    }</p></div>
    ";}
categories:
  - J2EE
tags:
  - equal
  - java基础

---
以下是我的理解，可能有误
Java中的“==”用来判断是否是同一个对象（对象的引用是不是一样），equals方法一般会被覆盖，主要是比较值，而且一般只和同一类对象比较。
## String的比较

<pre escaped="true" lang="java">public class TestEqual {
	
	public static void main(String[] args) {
		String a = "abc";
		String b = "abc";
		String c = new String("abc");//新建了一个对象
		String d = new String("abc");
		String e = "ab"+"c";//使用常量池中的对象
		String f = "ab";
		String g = f + "c";//string是固定字符，需要新建对象
		System.out.println(a == b);//true，第一次a把字符串放在常量池，那b继续用这个常量，e也一样
		System.out.println(a.equals(b));//true
		System.out.println("a == c?"+(a == c));//false
		System.out.println(a.equals(c));//true
		System.out.println(c==d);//false
		System.out.println(a==e);//true
		System.out.println(a==g);//false
	}
}
</pre>
还有个String.intern()不太理解  
更多的信息可以看这里：<http://developer.51cto.com/art/200602/21445.htm>
## 数字的比较

需要理解autoBoxing的概念！
<pre escaped="true" lang="java">public class TestEqual {
	
	public static void main(String[] args) {
		Integer i1 = new Integer(9); 
		Integer i2 = new Integer(9); 
		int i3 = 9;
		int i4 = 9;
		Integer i5 = 9;//自动装箱(box)操作，基本类型int 9可以自动box成对象Integer
		Integer i6 = 9;
		Long long1 = new Long(9);
		System.out.println(i1==i2);//false
		System.out.println(i1==i3);//true
		System.out.println("i3==i4?"+(i3==i4));//true，常量池
		System.out.println("i1==i3?"+(i1==i3));//true
		System.out.println("i5==i6?"+(i5==i6));//true，当-128&lt;i5&lt;127时为true，其他为false
		//http://blog.csdn.net/newsonglin/archive/2008/10/15/3079865.aspx
		// If the value p being boxed is true, false, a byte, a char in the range \u0000 to \u007f, or an int or short number between -128 and 127, then let r1 and r2 be the results of any two boxing conversions of p. It is always the case that r1 == r2.
		System.out.println("i3==i5?"+(i3==i5));//false
		System.out.println("i1==i5?"+(i1==i5));//false
		System.out.println(i1.equals(i2));//true，同类型比较值
		System.out.println(i1.equals(long1));//false，不同类型不进行比较

	}

}
</pre>
更多的信息可以参考这篇文章:<http://blog.csdn.net/newsonglin/archive/2008/10/15/3079865.aspx>