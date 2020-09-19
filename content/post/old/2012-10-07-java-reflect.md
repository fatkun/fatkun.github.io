---
title: JAVA反射(Reflect)的使用
author: fatkun
type: post
date: 2012-10-07T15:59:52+00:00
url: /2012/10/java-reflect.html
duoshuo_thread_id:
  - 6300408866374943489
wp-syntax-cache-content:
  - |
    a:4:{i:1;s:396:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="html" style="font-family:monospace;">LogFactory.class.getDeclaredMethod(&quot;functionName&quot;,new Class[]{String.class,int.class})</pre></td></tr></table><p class="theCode" style="display:none;">LogFactory.class.getDeclaredMethod(&quot;functionName&quot;,new Class[]{String.class,int.class})</p></div>
    ";i:2;s:1663:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #003399;">Method</span> method <span style="color: #339933;">=</span> LogFactory.<span style="color: #000000; font-weight: bold;">class</span>.<span style="color: #006633;">getDeclaredMethod</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;getContextClassLoader&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    method.<span style="color: #006633;">setAccessible</span><span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">true</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">// 如果是private的方法，要把它设为可访问</span>
    <span style="color: #003399;">ClassLoader</span> classLoader <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">ClassLoader</span><span style="color: #009900;">&#41;</span>method.<span style="color: #006633;">invoke</span><span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span></pre></td></tr></table><p class="theCode" style="display:none;">Method method = LogFactory.class.getDeclaredMethod(&quot;getContextClassLoader&quot;);
    method.setAccessible(true); // 如果是private的方法，要把它设为可访问
    ClassLoader classLoader = (ClassLoader)method.invoke(null);</p></div>
    ";i:3;s:1430:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #003399;">Field</span> field <span style="color: #339933;">=</span> LogFactory.<span style="color: #000000; font-weight: bold;">class</span>.<span style="color: #006633;">getDeclaredField</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;factories&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    field.<span style="color: #006633;">setAccessible</span><span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">true</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #003399;">Hashtable</span> obj <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">Hashtable</span><span style="color: #009900;">&#41;</span>field.<span style="color: #006633;">get</span><span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span></pre></td></tr></table><p class="theCode" style="display:none;">Field field = LogFactory.class.getDeclaredField(&quot;factories&quot;);
    field.setAccessible(true);
    Hashtable obj = (Hashtable)field.get(null);</p></div>
    ";i:4;s:2355:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #666666; font-style: italic;">// SessionState里有一个private static的tss局部变量</span>
    <span style="color: #000000; font-weight: bold;">Class</span> clazz <span style="color: #339933;">=</span> SessionState.<span style="color: #000000; font-weight: bold;">class</span><span style="color: #339933;">;</span>
    <span style="color: #003399;">Field</span> field <span style="color: #339933;">=</span> clazz.<span style="color: #006633;">getDeclaredField</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;tss&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">// 由于是private的，不能通过getField获取</span>
    field.<span style="color: #006633;">setAccessible</span><span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">true</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">// 设为可访问</span>
    <span style="color: #003399;">ThreadLocal</span> threadLocal <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">ThreadLocal</span><span style="color: #009900;">&#41;</span>field.<span style="color: #006633;">get</span><span style="color: #009900;">&#40;</span>sessionState<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">// 通过field.get(对象) 获取它的值</span>
    threadLocal.<span style="color: #006633;">remove</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span></pre></td></tr></table><p class="theCode" style="display:none;">// SessionState里有一个private static的tss局部变量
    Class clazz = SessionState.class;
    Field field = clazz.getDeclaredField(&quot;tss&quot;); // 由于是private的，不能通过getField获取
    field.setAccessible(true); // 设为可访问
    ThreadLocal threadLocal = (ThreadLocal)field.get(sessionState);// 通过field.get(对象) 获取它的值
    threadLocal.remove();</p></div>
    ";}
categories:
  - J2EE
tags:
  - JAVA
  - reflect
  - ThreadLocal

---
## 反射方法Method

getDeclaredMethod是获取该类声明的方法，不包括继承的。
> Method getDeclaredMethod(String name, Class&#8230; parameterTypes)  
> 返回一个 Method 对象，该对象反映此 Class 对象所表示的类或接口的指定已声明方法。
还有一个getMethod是只能获取public的方法
> getMethod(String name, Class&#8230; parameterTypes)  
> 返回一个 Method 对象，它反映此 Class 对象所表示的类或接口的指定公共成员方法。
name参数是方法名；parameterTypes 参数是按声明顺序标识该方法形参类型的 Class 对象的一个数组  
如：
<pre lang="html" escaped="true">LogFactory.class.getDeclaredMethod("functionName",new Class[]{String.class,int.class})</pre>
如果方法没有参数，提供null或者省略都可以。  
method.invoke中，invoke(Object obj, Object&#8230; args) ，obj是对象，如果是静态方法，填入null；args参数是一个Object对象数组，如 new Object[] {&#8220;test&#8221;, new Integer(10)}
下面的例子是想要反射common logging 包里的LogFactory getContextClassLoader方法。这是一个private static方法
<pre lang="java" escaped="true">Method method = LogFactory.class.getDeclaredMethod("getContextClassLoader");
method.setAccessible(true); // 如果是private的方法，要把它设为可访问
ClassLoader classLoader = (ClassLoader)method.invoke(null);</pre>
## 反射属性Field

和method差不多，也有getDeclaredField和getField方法。  
可以通过field.get来获取值，参数是你要获取的是哪个对象的属性。如果是静态变量，填入null  
另外可以通过field.set来赋值。
<pre lang="java" escaped="true">Field field = LogFactory.class.getDeclaredField("factories");
field.setAccessible(true);
Hashtable obj = (Hashtable)field.get(null);</pre>
## 例子

在SesstionState里有一个ThreadLocal的pravate tss变量，我们要取到这个变量，并且调用它的remove方法。注意：ThreadLocal的对象是在每个线程都存有一个map，把值存在那里，所以，必须和原线程一致才能取到他的值。
<pre lang="java" escaped="true">// SessionState里有一个private static的tss局部变量
Class clazz = SessionState.class;
Field field = clazz.getDeclaredField("tss"); // 由于是private的，不能通过getField获取
field.setAccessible(true); // 设为可访问
ThreadLocal threadLocal = (ThreadLocal)field.get(sessionState);// 通过field.get(对象) 获取它的值
threadLocal.remove();</pre>