---
title: GAE-Google App Engine网址抓取(java.net.UrlConnection)
author: fatkun
type: post
date: 2010-01-23T08:17:12+00:00
url: /2010/01/get-website-source-using-google-app-engine.html
views:
  - 143
duoshuo_thread_id:
  - 6300408713446425346
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:7060:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">package</span> <span style="color: #006699;">com.fatkun</span><span style="color: #339933;">;</span>
    <span style="color: #008000; font-style: italic; font-weight: bold;">/**
     * 在GAE上抓取网址
     * @author Fatkun
     * @site http://fatkun.com
     */</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">java.io.IOException</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">java.io.InputStreamReader</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">java.net.URL</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">javax.servlet.http.*</span><span style="color: #339933;">;</span>
    &nbsp;
    @SuppressWarnings<span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;serial&quot;</span><span style="color: #009900;">&#41;</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> URL2Servlet <span style="color: #000000; font-weight: bold;">extends</span> HttpServlet <span style="color: #009900;">&#123;</span>
    	<span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> doGet<span style="color: #009900;">&#40;</span>HttpServletRequest req, HttpServletResponse resp<span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">throws</span> <span style="color: #003399;">IOException</span> <span style="color: #009900;">&#123;</span>
    		resp.<span style="color: #006633;">setContentType</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;text/plain; charset=utf-8&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//显示编码</span>
    &nbsp;
    		<span style="color: #003399;">URL</span> url <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">URL</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;http://fatkun.com&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #666666; font-style: italic;">// 读取源码</span>
    		<span style="color: #666666; font-style: italic;">//读取中文时，使用Reader类是每次读出两个字节的，不会出现中文乱码</span>
    		<span style="color: #003399;">InputStreamReader</span> in <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">InputStreamReader</span><span style="color: #009900;">&#40;</span>url.<span style="color: #006633;">openStream</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, <span style="color: #0000ff;">&quot;UTF-8&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #000066; font-weight: bold;">char</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> buf <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #000066; font-weight: bold;">char</span><span style="color: #009900;">&#91;</span><span style="color: #cc66cc;">2048</span><span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//缓存</span>
    		<span style="color: #003399;">StringBuffer</span> sb <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">StringBuffer</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #000066; font-weight: bold;">int</span> len <span style="color: #339933;">=</span> <span style="color: #cc66cc;">0</span><span style="color: #339933;">;</span>
    		<span style="color: #000000; font-weight: bold;">while</span> <span style="color: #009900;">&#40;</span><span style="color: #009900;">&#40;</span>len <span style="color: #339933;">=</span> in.<span style="color: #006633;">read</span><span style="color: #009900;">&#40;</span>buf<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">!=</span> <span style="color: #339933;">-</span><span style="color: #cc66cc;">1</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span><span style="color: #666666; font-style: italic;">//当没到文档尽头继续读取</span>
    			sb.<span style="color: #006633;">append</span><span style="color: #009900;">&#40;</span>buf, <span style="color: #cc66cc;">0</span>, len<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #009900;">&#125;</span>
    &nbsp;
    		<span style="color: #666666; font-style: italic;">// 输出在网页上</span>
    		resp.<span style="color: #006633;">getWriter</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>sb.<span style="color: #006633;">toString</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">package com.fatkun;
    /**
     * 在GAE上抓取网址
     * @author Fatkun
     * @site http://fatkun.com
     */
    
    import java.io.IOException;
    import java.io.InputStreamReader;
    import java.net.URL;
    
    import javax.servlet.http.*;
    
    @SuppressWarnings(&quot;serial&quot;)
    public class URL2Servlet extends HttpServlet {
    	public void doGet(HttpServletRequest req, HttpServletResponse resp) throws IOException {
    		resp.setContentType(&quot;text/plain; charset=utf-8&quot;);//显示编码
    
    		URL url = new URL(&quot;http://fatkun.com&quot;);
    		// 读取源码
    		//读取中文时，使用Reader类是每次读出两个字节的，不会出现中文乱码
    		InputStreamReader in = new InputStreamReader(url.openStream(), &quot;UTF-8&quot;);
    		char[] buf = new char[2048];//缓存
    		StringBuffer sb = new StringBuffer();
    		int len = 0;
    		while ((len = in.read(buf)) != -1) {//当没到文档尽头继续读取
    			sb.append(buf, 0, len);
    		}
    
    		// 输出在网页上
    		resp.getWriter().println(sb.toString());
    	}
    }</p></div>
    ";i:2;s:4067:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #666666; font-style: italic;">// 此处的地址请换成你的，在本地测试时可以填入http://localhost:8888/request.jsp</span>
    <span style="color: #003399;">URL</span> url <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">URL</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;http://2.latest.fatkuns.appspot.com/request.jsp&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #003399;">HttpURLConnection</span> connection <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">HttpURLConnection</span><span style="color: #009900;">&#41;</span> url.<span style="color: #006633;">openConnection</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    connection.<span style="color: #006633;">setDoOutput</span><span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">true</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">// 使用 URL 连接进行输出</span>
    connection.<span style="color: #006633;">setRequestMethod</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;POST&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">// 取得输出流</span>
    <span style="color: #003399;">OutputStreamWriter</span> writer <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">OutputStreamWriter</span><span style="color: #009900;">&#40;</span>connection.<span style="color: #006633;">getOutputStream</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">// 用UTF-8编码，保证中文传递正常</span>
    <span style="color: #003399;">String</span> message <span style="color: #339933;">=</span> <span style="color: #003399;">URLEncoder</span>.<span style="color: #006633;">encode</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;你好，I'm Fatkun!&quot;</span>, <span style="color: #0000ff;">&quot;UTF-8&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">// 写入发送的内容</span>
    writer.<span style="color: #006633;">write</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;msg=&quot;</span> <span style="color: #339933;">+</span> message<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    writer.<span style="color: #006633;">close</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span></pre></td></tr></table><p class="theCode" style="display:none;">// 此处的地址请换成你的，在本地测试时可以填入http://localhost:8888/request.jsp
    URL url = new URL(&quot;http://2.latest.fatkuns.appspot.com/request.jsp&quot;);
    HttpURLConnection connection = (HttpURLConnection) url.openConnection();
    connection.setDoOutput(true);// 使用 URL 连接进行输出
    connection.setRequestMethod(&quot;POST&quot;);
    // 取得输出流
    OutputStreamWriter writer = new OutputStreamWriter(connection.getOutputStream());
    // 用UTF-8编码，保证中文传递正常
    String message = URLEncoder.encode(&quot;你好，I'm Fatkun!&quot;, &quot;UTF-8&quot;);
    // 写入发送的内容
    writer.write(&quot;msg=&quot; + message);
    writer.close();</p></div>
    ";}
categories:
  - J2EE
tags:
  - GAE
  - google app engine
  - 中文乱码
  - 网址抓取

---
Google App Engine 的网址抓取挺方便的，可以使用java.net.UrlConnection这个类。有了这个我们可以干什么？例如可以从某处获取天气信息等等~  
![][1]  
(提醒一下，上面的是图片。。不要误点了啊。。。)  
看看例子：<http://2.latest.fatkuns.appspot.com/>  
<!--more-->

## GAE网址抓取是什么？

> App Engine 应用程序可以抓取资源，并通过互联网使用 HTTP 和 HTTPS 请求与其他主机通信。应用程序使用网址抓取服务来进行请求。
我觉得其实就是可以通过它抓取别人网页的源代码。
## 使用URL获取源码

<pre escaped="true" lang="java">package com.fatkun;
/**
 * 在GAE上抓取网址
 * @author Fatkun
 * @site http://fatkun.com
 */

import java.io.IOException;
import java.io.InputStreamReader;
import java.net.URL;

import javax.servlet.http.*;

@SuppressWarnings("serial")
public class URL2Servlet extends HttpServlet {
	public void doGet(HttpServletRequest req, HttpServletResponse resp) throws IOException {
		resp.setContentType("text/plain; charset=utf-8");//显示编码

		URL url = new URL("http://fatkun.com");
		// 读取源码
		//读取中文时，使用Reader类是每次读出两个字节的，不会出现中文乱码
		InputStreamReader in = new InputStreamReader(url.openStream(), "UTF-8");
		char[] buf = new char[2048];//缓存
		StringBuffer sb = new StringBuffer();
		int len = 0;
		while ((len = in.read(buf)) != -1) {//当没到文档尽头继续读取
			sb.append(buf, 0, len);
		}

		// 输出在网页上
		resp.getWriter().println(sb.toString());
	}
}</pre>
## 使用HttpURLConnection 来POST内容

<pre escaped="true" lang="java">// 此处的地址请换成你的，在本地测试时可以填入http://localhost:8888/request.jsp
URL url = new URL("http://2.latest.fatkuns.appspot.com/request.jsp");
HttpURLConnection connection = (HttpURLConnection) url.openConnection();
connection.setDoOutput(true);// 使用 URL 连接进行输出
connection.setRequestMethod("POST");
// 取得输出流
OutputStreamWriter writer = new OutputStreamWriter(connection.getOutputStream());
// 用UTF-8编码，保证中文传递正常
String message = URLEncoder.encode("你好，I'm Fatkun!", "UTF-8");
// 写入发送的内容
writer.write("msg=" + message);
writer.close();
</pre>
上面是主要的代码，看注释好了，都很清楚。
## Google App Engine中文乱码问题

注意在读取中文的网页时，由于编码是使用UTF或者GBK,GB2312等编码，使用InputStream类不太方便，另外有可以出现错误。  
试过使用InputStream类，然后用new String(bytes[],&#8221;utf-8&#8243;)来转换编码，不过出现一点问题，不知道是我不会用还是怎么的。  
不过使用这样的写法就方便多了。  
InputStreamReader in = new InputStreamReader(url.openStream(), &#8220;UTF-8&#8221;);  
编码都不用转换了~指定它的编码就行。  
注意这里要加上“UTF-8”，虽然不加在本地测试时没问题，不过上传到GAE上就不能显示中文了。  
PS2:这里的UTF-8是代表你抓取网页的编码。如果你抓取的网页是gb2312的需要根据实质需求改变。
附上我做的例子：<http://2.latest.fatkuns.appspot.com/>  
源码在这里：<http://2.latest.fatkuns.appspot.com/source.rar>,里面的lib目录下的我删除了，请自行添加。

 [1]: http://farm3.static.flickr.com/2724/4297317270_500f2c34b3.jpg