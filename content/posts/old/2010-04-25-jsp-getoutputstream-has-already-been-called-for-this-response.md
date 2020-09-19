---
title: jsp getOutputStream() has already been called for this response异常解决方法
author: fatkun
type: post
date: 2010-04-25T13:01:06+00:00
url: /2010/04/jsp-getoutputstream-has-already-been-called-for-this-response.html
views:
  - 10
duoshuo_thread_id:
  - 6300408724984955649
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:638:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">out.<span style="color: #006633;">clear</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    out <span style="color: #339933;">=</span> pageContext.<span style="color: #006633;">pushBody</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span></pre></td></tr></table><p class="theCode" style="display:none;">out.clear();
    out = pageContext.pushBody();</p></div>
    ";i:2;s:5605:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #339933;">&lt;%</span>@ page info<span style="color: #339933;">=</span><span style="color: #0000ff;">&quot;Random Image Show&quot;</span> pageEncoding<span style="color: #339933;">=</span><span style="color: #0000ff;">&quot;UTF-8&quot;</span> contentType<span style="color: #339933;">=</span><span style="color: #0000ff;">&quot;image/jpg&quot;</span> autoFlush<span style="color: #339933;">=</span><span style="color: #0000ff;">&quot;true&quot;</span> buffer<span style="color: #339933;">=</span><span style="color: #0000ff;">&quot;16kb&quot;</span> session<span style="color: #339933;">=</span><span style="color: #0000ff;">&quot;false&quot;</span>
    	<span style="color: #000000; font-weight: bold;">import</span><span style="color: #339933;">=</span><span style="color: #0000ff;">&quot;java.io.FileInputStream&quot;</span><span style="color: #339933;">%&gt;</span>
    <span style="color: #339933;">&lt;%</span>
    	ServletOutputStream sos <span style="color: #339933;">=</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #339933;">;</span>
    	<span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>sos <span style="color: #339933;">==</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span> sos <span style="color: #339933;">=</span> response.<span style="color: #006633;">getOutputStream</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	<span style="color: #003399;">FileInputStream</span> fis <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">FileInputStream</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span><span style="color: #009900;">&#41;</span> request.<span style="color: #006633;">getAttribute</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;filename&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	<span style="color: #000066; font-weight: bold;">byte</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> buf <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #000066; font-weight: bold;">byte</span><span style="color: #009900;">&#91;</span><span style="color: #cc66cc;">1024</span><span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">//缓冲区大小  </span>
    	<span style="color: #000066; font-weight: bold;">int</span> len <span style="color: #339933;">=</span> <span style="color: #cc66cc;">0</span><span style="color: #339933;">;</span>
    	<span style="color: #000000; font-weight: bold;">while</span> <span style="color: #009900;">&#40;</span><span style="color: #009900;">&#40;</span>len <span style="color: #339933;">=</span> fis.<span style="color: #006633;">read</span><span style="color: #009900;">&#40;</span>buf<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">!=</span> <span style="color: #339933;">-</span><span style="color: #cc66cc;">1</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    		sos.<span style="color: #006633;">write</span><span style="color: #009900;">&#40;</span>buf, <span style="color: #cc66cc;">0</span>, len<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span>
    	sos.<span style="color: #006633;">flush</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	sos.<span style="color: #006633;">close</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	fis.<span style="color: #006633;">close</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	out.<span style="color: #006633;">clear</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	out <span style="color: #339933;">=</span> pageContext.<span style="color: #006633;">pushBody</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #339933;">%&gt;</span></pre></td></tr></table><p class="theCode" style="display:none;">&lt;%@ page info=&quot;Random Image Show&quot; pageEncoding=&quot;UTF-8&quot; contentType=&quot;image/jpg&quot; autoFlush=&quot;true&quot; buffer=&quot;16kb&quot; session=&quot;false&quot;
    	import=&quot;java.io.FileInputStream&quot;%&gt;
    &lt;%
    	ServletOutputStream sos = null;
    	if (sos == null) sos = response.getOutputStream();
    	FileInputStream fis = new FileInputStream((String) request.getAttribute(&quot;filename&quot;));
    	byte[] buf = new byte[1024]; //缓冲区大小  
    	int len = 0;
    	while ((len = fis.read(buf)) != -1) {
    		sos.write(buf, 0, len);
    	}
    	sos.flush();
    	sos.close();
    	fis.close();
    	out.clear();
    	out = pageContext.pushBody();
    %&gt;</p></div>
    ";}
categories:
  - J2EE
tags:
  - JAVA
  - 错误

---
添加以下两段代码即可，我是在用jsp输出图像的时候出现这个问题
<pre escaped="true" lang="java">out.clear();
out = pageContext.pushBody();</pre>
## 附上我的输出图像的JSP代码

<pre escaped="true" lang="java">&lt;%@ page info="Random Image Show" pageEncoding="UTF-8" contentType="image/jpg" autoFlush="true" buffer="16kb" session="false"
	import="java.io.FileInputStream"%>
&lt;%
	ServletOutputStream sos = null;
	if (sos == null) sos = response.getOutputStream();
	FileInputStream fis = new FileInputStream((String) request.getAttribute("filename"));
	byte[] buf = new byte[1024]; //缓冲区大小  
	int len = 0;
	while ((len = fis.read(buf)) != -1) {
		sos.write(buf, 0, len);
	}
	sos.flush();
	sos.close();
	fis.close();
	out.clear();
	out = pageContext.pushBody();
%>

</pre>