---
title: try finally中return的执行顺序
author: fatkun
type: post
date: 2010-11-26T14:25:40+00:00
url: /2010/11/try-catch-finally-return.html
duoshuo_thread_id:
  - 6300408787870155522
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:5363:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> <span style="color: #000000; font-weight: bold;">Try</span> <span style="color: #009900;">&#123;</span>
    	<span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000066; font-weight: bold;">void</span> main<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> args<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;最终结果:&quot;</span> <span style="color: #339933;">+</span> aa<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span>
    &nbsp;
    	<span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000066; font-weight: bold;">int</span> aa<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    		<span style="color: #000066; font-weight: bold;">int</span> a <span style="color: #339933;">=</span> <span style="color: #cc66cc;">1</span><span style="color: #339933;">;</span>
    		<span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#123;</span>
    			<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;try:&quot;</span> <span style="color: #339933;">+</span> a<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
    			<span style="color: #000000; font-weight: bold;">throw</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">Exception</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    			<span style="color: #666666; font-style: italic;">//return a;</span>
    		<span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">Exception</span> e<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    			a <span style="color: #339933;">=</span> <span style="color: #cc66cc;">2</span><span style="color: #339933;">;</span>
    			<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;catch:&quot;</span> <span style="color: #339933;">+</span> a<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    			<span style="color: #000000; font-weight: bold;">return</span> a<span style="color: #339933;">;</span>
    		<span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">finally</span> <span style="color: #009900;">&#123;</span>
    			a <span style="color: #339933;">=</span> <span style="color: #cc66cc;">3</span><span style="color: #339933;">;</span>
    			<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;finally:&quot;</span> <span style="color: #339933;">+</span> a<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    			<span style="color: #666666; font-style: italic;">//return编辑器会提示finally block does not complete normally</span>
    			<span style="color: #000000; font-weight: bold;">return</span> a<span style="color: #339933;">;</span>
    		<span style="color: #009900;">&#125;</span>
    	<span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #666666; font-style: italic;">//运行结果:</span>
    <span style="color: #666666; font-style: italic;">/*
    try:1
    catch:2
    finally:3
    最终结果:3
    */</span></pre></td></tr></table><p class="theCode" style="display:none;">public class Try {
    	public static void main(String[] args) {
    		System.out.println(&quot;最终结果:&quot; + aa());
    	}
    
    	public static int aa() {
    		int a = 1;
    		try {
    			System.out.println(&quot;try:&quot; + a);
    
    			throw new Exception();
    			//return a;
    		} catch (Exception e) {
    			a = 2;
    			System.out.println(&quot;catch:&quot; + a);
    			return a;
    		} finally {
    			a = 3;
    			System.out.println(&quot;finally:&quot; + a);
    			//return编辑器会提示finally block does not complete normally
    			return a;
    		}
    	}
    
    }
    
    //运行结果:
    /*
    try:1
    catch:2
    finally:3
    最终结果:3
    */</p></div>
    ";}
categories:
  - J2EE
tags:
  - finally
  - return

---
看代码吧，容易懂点。
<pre escaped="true" lang="java">public class Try {
	public static void main(String[] args) {
		System.out.println("最终结果:" + aa());
	}

	public static int aa() {
		int a = 1;
		try {
			System.out.println("try:" + a);

			throw new Exception();
			//return a;
		} catch (Exception e) {
			a = 2;
			System.out.println("catch:" + a);
			return a;
		} finally {
			a = 3;
			System.out.println("finally:" + a);
			//return编辑器会提示finally block does not complete normally
			return a;
		}
	}

}

//运行结果:
/*
try:1
catch:2
finally:3
最终结果:3
*/</pre>
可以把上面的代码注释一部分。试试注释掉抛出的错误。以及各个return。
## 结论

  1. finally始终执行，如果在finally中有return，始终返回这个值
  2. 当不抛错和在try中return a ，finally中没有return语句时， try 的 return 方法会先执行，finally的方法最后执行，然后再返回到主方法。此时最终结果是1
  3. finally中的return优先级最高，最终结果是3
  4. return的值会保存下来，不受到后面finally的影响