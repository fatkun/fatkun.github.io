---
title: JSP实验二-JSP从Request获取值
author: fatkun
type: post
date: 2009-10-10T04:18:48+00:00
url: /2009/10/jsp实验二-jsp从request获取值.html
views:
  - 23
duoshuo_thread_id:
  - 6300408687705981697
categories:
  - J2EE
tags:
  - JSP实验

---
把这两个文件放入服务器的目录里就可以了，忘记放哪里了？没关系，看这里<a href="http://blog.fatkun.com/view.asp?id=16" target="_blank">JBOSS把网页文件放入哪里</a>  
注意这句代码“request.setCharacterEncoding(&#8220;GBK&#8221;);”不然会导致接收过来的乱码的
<!--more-->

  
把这两个文件放入服务器的目录里就可以了，忘记放哪里了？没关系，看这里<a href="http://blog.fatkun.com/view.asp?id=16" target="_blank">JBOSS把网页文件放入哪里</a>  
注意这句代码“request.setCharacterEncoding(&#8220;GBK&#8221;);”不然会导致接收过来的乱码的  
index.html文件
<pre class="brush:&quot;html&quot;;">&lt;!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd"&gt;&lt;html&gt;&lt;head&gt;&lt;meta http-equiv="Content-Type" content="text/html; charset=GBK"&gt;&lt;title&gt;Insert title here&lt;/title&gt;&lt;/head&gt;&lt;body&gt;&lt;form action="request.jsp" method="post"&gt;文本框:&lt;input type="text" name="txt" /&gt;&lt;br/&gt;单选按钮：&lt;input type="radio" name="rd" value="男" /&gt;男&lt;input type="radio" name="rd" value="女" /&gt;女&lt;br/&gt;多选按钮：&lt;input type="checkbox" name="chb" value="大方" /&gt;大方&lt;input type="checkbox" name="chb" value="体贴" /&gt;体贴&lt;input type="checkbox" name="chb" value="热情" /&gt;热情&lt;br/&gt;大文本框：&lt;textarea rows="8" cols="30" name="memo"&gt;&lt;/textarea&gt;&lt;br/&gt;选择框：&lt;select name="sel"&gt;&lt;option value="北京"&gt;北京&lt;/option&gt;&lt;option value="上海"&gt;上海&lt;/option&gt;&lt;/select&gt;&lt;br/&gt;&lt;input type="submit" value="提交" /&gt;&lt;/form&gt;&lt;/body&gt;&lt;/html&gt;</pre>
request.jsp文件
<pre class="brush:&quot;java&quot;;">&lt;%@ page language="java" contentType="text/html; charset=GBK"pageEncoding="GBK"%&gt;&lt;!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd"&gt;&lt;html&gt;&lt;head&gt;&lt;meta http-equiv="Content-Type" content="text/html; charset=GBK"&gt;&lt;title&gt;Insert title here&lt;/title&gt;&lt;/head&gt;&lt;body&gt;&lt;%request.setCharacterEncoding("GBK");//设置编码out.println("文本框内容是："+request.getParameter("txt"));out.println("&lt;br/&gt;");out.println("单选框内容是："+request.getParameter("rd"));out.println("&lt;br/&gt;");out.println("多选框内容是："+request.getParameter("chb"));out.println("&lt;br/&gt;");out.println("大文本框内容是："+request.getParameter("memo"));out.println("&lt;br/&gt;");out.println("选择框内容是："+request.getParameter("sel"));%&gt;&lt;/body&gt;&lt;/html&gt;</pre>