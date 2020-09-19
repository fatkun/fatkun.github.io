---
title: 使用cookie获取QQ头像（JSP版）
author: fatkun
type: post
date: 2010-07-11T16:21:00+00:00
url: /2010/07/get-qq-avatar-with-cookie.html
views:
  - 27
duoshuo_thread_id:
  - 6300408750880588545
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:9296:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #339933;">&lt;%</span>@ page language<span style="color: #339933;">=</span><span style="color: #0000ff;">&quot;java&quot;</span> contentType<span style="color: #339933;">=</span><span style="color: #0000ff;">&quot;image/bmp&quot;</span> pageEncoding<span style="color: #339933;">=</span><span style="color: #0000ff;">&quot;UTF-8&quot;</span><span style="color: #339933;">%&gt;&lt;%</span>@ page <span style="color: #000000; font-weight: bold;">import</span><span style="color: #339933;">=</span><span style="color: #0000ff;">&quot;java.net.*,java.util.*,java.io.*&quot;</span><span style="color: #339933;">%&gt;&lt;%</span>
    	<span style="color: #003399;">String</span> qqnum <span style="color: #339933;">=</span> request.<span style="color: #006633;">getParameter</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;qq&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	<span style="color: #003399;">URL</span> url <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">URL</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;http://face6.qun.qq.com/cgi/svr/face/getface?type=1&amp;uin=&quot;</span><span style="color: #339933;">+</span>qqnum<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	<span style="color: #003399;">HttpURLConnection</span> http <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">HttpURLConnection</span><span style="color: #009900;">&#41;</span> url.<span style="color: #006633;">openConnection</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	<span style="color: #666666; font-style: italic;">//设置Header</span>
    	http.<span style="color: #006633;">setRequestProperty</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;User-Agent&quot;</span>, <span style="color: #0000ff;">&quot;Mozilla/5.0 (compatible; MSIE 6.0; Windows NT)&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	http.<span style="color: #006633;">setRequestProperty</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Content-Type&quot;</span>, <span style="color: #0000ff;">&quot;application/x-www-form-urlencoded&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	<span style="color: #666666; font-style: italic;">//设置Cookie，登陆WebQQ或者QQ空间可以查看cookie得到下面的值，请替换过来</span>
    	<span style="color: #666666; font-style: italic;">//还不知道skey这个值会不会定期变化,QQ号码不够10位前面补0</span>
    	http.<span style="color: #006633;">setRequestProperty</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Cookie&quot;</span>, <span style="color: #0000ff;">&quot;uin=oQQ号码; skey=@安全码;&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	http.<span style="color: #006633;">setRequestMethod</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;GET&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	http.<span style="color: #006633;">setDoInput</span><span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">true</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	<span style="color: #003399;">InputStream</span> is <span style="color: #339933;">=</span> http.<span style="color: #006633;">getInputStream</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	<span style="color: #666666; font-style: italic;">//得到输出流，注意out是Writer类的对象，这里要用字节流</span>
    	<span style="color: #003399;">OutputStream</span> os <span style="color: #339933;">=</span> response.<span style="color: #006633;">getOutputStream</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>  
    &nbsp;
    	<span style="color: #666666; font-style: italic;">//输出头像</span>
    	<span style="color: #000000; font-weight: bold;">while</span> <span style="color: #009900;">&#40;</span>is.<span style="color: #006633;">available</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">&gt;</span> <span style="color: #cc66cc;">0</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    		os.<span style="color: #006633;">write</span><span style="color: #009900;">&#40;</span>is.<span style="color: #006633;">read</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span>
    &nbsp;
    	<span style="color: #666666; font-style: italic;">//在后台打印Header信息,不是必须</span>
    	<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>http.<span style="color: #006633;">getResponseCode</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	Map<span style="color: #339933;">&lt;</span><span style="color: #003399;">String</span>, List<span style="color: #339933;">&lt;</span>String<span style="color: #339933;">&gt;&gt;</span> header <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> HashMap<span style="color: #339933;">&lt;</span><span style="color: #003399;">String</span>, List<span style="color: #339933;">&lt;</span>String<span style="color: #339933;">&gt;&gt;</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	header <span style="color: #339933;">=</span> http.<span style="color: #006633;">getHeaderFields</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	<span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> str <span style="color: #339933;">:</span> header.<span style="color: #006633;">keySet</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>str <span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot;&quot;</span> <span style="color: #339933;">+</span> header.<span style="color: #006633;">get</span><span style="color: #009900;">&#40;</span>str<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span>
    <span style="color: #339933;">%&gt;</span></pre></td></tr></table><p class="theCode" style="display:none;">&lt;%@ page language=&quot;java&quot; contentType=&quot;image/bmp&quot; pageEncoding=&quot;UTF-8&quot;%&gt;&lt;%@ page import=&quot;java.net.*,java.util.*,java.io.*&quot;%&gt;&lt;%
    	String qqnum = request.getParameter(&quot;qq&quot;);
    	URL url = new URL(&quot;http://face6.qun.qq.com/cgi/svr/face/getface?type=1&amp;uin=&quot;+qqnum);
    	HttpURLConnection http = (HttpURLConnection) url.openConnection();
    	//设置Header
    	http.setRequestProperty(&quot;User-Agent&quot;, &quot;Mozilla/5.0 (compatible; MSIE 6.0; Windows NT)&quot;);
    	http.setRequestProperty(&quot;Content-Type&quot;, &quot;application/x-www-form-urlencoded&quot;);
    	//设置Cookie，登陆WebQQ或者QQ空间可以查看cookie得到下面的值，请替换过来
    	//还不知道skey这个值会不会定期变化,QQ号码不够10位前面补0
    	http.setRequestProperty(&quot;Cookie&quot;, &quot;uin=oQQ号码; skey=@安全码;&quot;);
    	http.setRequestMethod(&quot;GET&quot;);
    	http.setDoInput(true);
    	InputStream is = http.getInputStream();
    	//得到输出流，注意out是Writer类的对象，这里要用字节流
    	OutputStream os = response.getOutputStream();  
    	
    	//输出头像
    	while (is.available() &gt; 0) {
    		os.write(is.read());
    	}
    	
    	//在后台打印Header信息,不是必须
    	System.out.println(http.getResponseCode());
    	Map&lt;String, List&lt;String&gt;&gt; header = new HashMap&lt;String, List&lt;String&gt;&gt;();
    	header = http.getHeaderFields();
    	for (String str : header.keySet()) {
    		System.out.println(str + &quot;&quot; + header.get(str));
    	}
    %&gt;</p></div>
    ";}
categories:
  - J2EE
tags:
  - 得到QQ头像
  - 最新获取QQ头像

---
由于腾讯现在QQ头像必须要登录才能看到原头像，所以以前直接获取头像已经失效了（如这篇文章<a rel="bookmark" href="http://fatkun.com/2010/01/get-qq-avatar-url/">获取QQ头像地址</a>），既然直接获取不行，那来个曲线救国吧~</span>
PS:写完代码后才发现腾讯的头像隐私保护得挺好的，只有自己的好友或群友能获取全头像，非好友只能获取QQ内置头像。悲剧啊。。。
直接贴代码,以下代码是通过带cookie访问头像的链接，其实其他PHP等也可以实现的：
<pre escaped="true" lang="java">&lt;%@ page language="java" contentType="image/bmp" pageEncoding="UTF-8"%&gt;&lt;%@ page import="java.net.*,java.util.*,java.io.*"%&gt;&lt;%
	String qqnum = request.getParameter("qq");
	URL url = new URL("http://face6.qun.qq.com/cgi/svr/face/getface?type=1&uin="+qqnum);
	HttpURLConnection http = (HttpURLConnection) url.openConnection();
	//设置Header
	http.setRequestProperty("User-Agent", "Mozilla/5.0 (compatible; MSIE 6.0; Windows NT)");
	http.setRequestProperty("Content-Type", "application/x-www-form-urlencoded");
	//设置Cookie，登陆WebQQ或者QQ空间可以查看cookie得到下面的值，请替换过来
	//还不知道skey这个值会不会定期变化,QQ号码不够10位前面补0
	http.setRequestProperty("Cookie", "uin=oQQ号码; skey=@安全码;");
	http.setRequestMethod("GET");
	http.setDoInput(true);
	InputStream is = http.getInputStream();
	//得到输出流，注意out是Writer类的对象，这里要用字节流
	OutputStream os = response.getOutputStream();  
	
	//输出头像
	while (is.available() &gt; 0) {
		os.write(is.read());
	}
	
	//在后台打印Header信息,不是必须
	System.out.println(http.getResponseCode());
	Map&lt;String, List&lt;String&gt;&gt; header = new HashMap&lt;String, List&lt;String&gt;&gt;();
	header = http.getHeaderFields();
	for (String str : header.keySet()) {
		System.out.println(str + "" + header.get(str));
	}
%&gt;</pre>
可是只能获取自己好友的自定义头像，其他非好友只能获取QQ内置头像（一般不是那只企鹅），所以就懒得上传到服务器了，JSP可以上传到Google app engine^_^