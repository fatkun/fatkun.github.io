---
title: Java的运算符号（逻辑与、或、非、移位运算）
author: fatkun
type: post
date: 2010-07-28T03:45:53+00:00
url: /2010/07/java-operator.html
views:
  - 26
duoshuo_thread_id:
  - 6300408751471985409
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:3625:"
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
    </pre></td><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> CalClass <span style="color: #009900;">&#123;</span>
    	<span style="color: #000000; font-weight: bold;">static</span> <span style="color: #003399;">Boolean</span> test<span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> num<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#123;</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>num<span style="color: #339933;">+</span><span style="color: #0000ff;">&quot;&gt;2&quot;</span><span style="color: #339933;">+</span><span style="color: #009900;">&#40;</span>num<span style="color: #339933;">&gt;</span><span style="color: #cc66cc;">2</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #000000; font-weight: bold;">return</span> num<span style="color: #339933;">&gt;</span><span style="color: #cc66cc;">2</span><span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span>
    	<span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000066; font-weight: bold;">void</span> main<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> args<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#123;</span>
    		<span style="color: #000066; font-weight: bold;">int</span> i <span style="color: #339933;">=</span> <span style="color: #cc66cc;">1</span>, j <span style="color: #339933;">=</span><span style="color: #cc66cc;">3</span> , k <span style="color: #339933;">=</span> <span style="color: #cc66cc;">4</span><span style="color: #339933;">;</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>test<span style="color: #009900;">&#40;</span>i<span style="color: #009900;">&#41;</span><span style="color: #339933;">||</span>test<span style="color: #009900;">&#40;</span>j<span style="color: #009900;">&#41;</span><span style="color: #339933;">||</span>test<span style="color: #009900;">&#40;</span>k<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;end&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">public class CalClass {
    	static Boolean test(int num){
    		System.out.println(num+&quot;&gt;2&quot;+(num&gt;2));
    		return num&gt;2;
    	}
    	public static void main(String[] args){
    		int i = 1, j =3 , k = 4;
    		System.out.println(test(i)||test(j)||test(k));
    		System.out.println(&quot;end&quot;);
    	}
    }</p></div>
    ";}
categories:
  - J2EE
tags:
  - java基础
  - Thinking in Java 读书笔记

---
1.只可将AND，OR 或NOT 应用于布尔值。与在C 及C++中不同，不可将一个非布尔值当作布尔值在逻辑表达式中使用。  
2.在AND（&&）运算中a()&&b()&&c()，当a为false时，b与c都不再执行，因为整个表达式都是false了，没必要再执行下去，OR（||）也是一样，当有一个为true时就结束。
<pre escaped="true" lang="java" line="1">public class CalClass {
	static Boolean test(int num){
		System.out.println(num+"&gt;2"+(num&gt;2));
		return num&gt;2;
	}
	public static void main(String[] args){
		int i = 1, j =3 , k = 4;
		System.out.println(test(i)||test(j)||test(k));
		System.out.println("end");
	}
}</pre>
3.对于布尔值，按位运算符（如&）具有与逻辑运算符(如&&)相同的效果，只是它们不会中途“短路”。
## 移位运算符

左移位运算符（<<）能将运算符左边的运算对象向左移动运算符右侧指定的位数（在低位补 0）。“有符号”右移位运算符（>>）则将运算符左边的运算对象向右移动运算符右侧指定的位数。“有符号”右移位运算符使用了“符号扩展”：若值为正，则在高位插入0；若值为负，则在高位插入1。Java 也添加了一种“无符号”右移位运算符（>>>），它使用了“零扩展”：无论正负，都在高位插入0。  
若对char，byte 或者short 进行移位处理，那么在移位进行之前，它们会自动转换成一个int。只有右侧的5个低位才会用到。这样可防止我们在一个 int数里移动不切实际的位数。若对一个long 值进行处理，最后得到的结果也是long。此时只会用到右侧的 6个低位，防止移动超过 long 值里现成的位数。但在进行“无符号”右移位时，也可能遇到一个问题。若对 byte 或short 值进行右移位运算，得到的可能不是正确的结果（Java 1.0 和Java 1.1 特别突出）。它们会自动转换成int 类型，并进行右移位。但“零扩展”不会发生。  
http://www.blogjava.net/rosen/archive/2005/08/12/9955.html  
“>> 右移”；“<< 左移”；“>>> 无符号右移”  
例子：
例子：  
-5>>3=-1  
1111 1111 1111 1111 1111 1111 1111 1011  
1111 1111 1111 1111 1111 1111 1111 1111  
其结果与 Math.floor((double)-5/(2\*2\*2)) 完全相同。
-5<<3=-40  
1111 1111 1111 1111 1111 1111 1111 1011  
1111 1111 1111 1111 1111 1111 1101 1000  
其结果与 -5\*2\*2*2 完全相同。
-5>>>3=536870911  
1111 1111 1111 1111 1111 1111 1111 1011  
0001 1111 1111 1111 1111 1111 1111 1111