---
title: GAE-简单的留言板(Simple Guestbook)
author: fatkun
type: post
date: 2009-12-20T06:32:26+00:00
excerpt: 这个例子其实就是Google官方给出来的例子~你可以在文档中看到，我在原例子的基础上添加了修改与删除功能~（...
draft: true
private: true
url: /2009/12/gae-guestbook.html
views:
  - 95
duoshuo_thread_id:
  - 6300408706957837057
categories:
  - J2EE
tags:
  - GAE
  - Google
  - google app engine
  - 留言本

---
这个例子其实就是Google官方给出来的例子~你可以在<a href="http://code.google.com/intl/zh-CN/appengine/docs/java/gettingstarted/" target="_blank" rel="noopener noreferrer">文档</a>中看到，我在原例子的基础上添加了修改与删除功能~（没判断权限~谁都可以删除~要判断也很简单&#8230;判断一下登陆的email）
我就不说那么详细了·官方例子说的已经很清楚了，需要源码在这里下载：<a href="http://115.com/file/bhqlcqtq" target="_blank" rel="noopener noreferrer">http://115.com/file/bhqlcqtq</a>
这个例子显示效果在此：<a href="http://1.latest.fatkuns.appspot.com/" target="_blank" rel="noopener noreferrer">http://1.latest.fatkuns.appspot.com/</a>  
![][1] 
这个例子涉及了
  1. 如何使用用户服务（也就是使用google账号登陆~我有点担心的是别人伪造一个假的登录页面怎么办？放心，我做的那个是真的&#8230;- -!）
  2. 如何存储数据（使用JDO）
  3. JSP
  4. Servlet
<!--more-->

好~开始了~那些准备工作就不说了，创建项目，包名这些~
## 一、要保存留言，我们需要创建一个这样的文件~Greeting.java

<pre lang="java">package com.fatkun.guestbook;

import java.util.Date;

import javax.jdo.annotations.IdGeneratorStrategy;
import javax.jdo.annotations.IdentityType;
import javax.jdo.annotations.PersistenceCapable;
import javax.jdo.annotations.Persistent;
import javax.jdo.annotations.PrimaryKey;

import com.google.appengine.api.users.User;

@PersistenceCapable(identityType = IdentityType.APPLICATION)
public class Greeting {
	//主键的设置，自增的方式
	@PrimaryKey
	@Persistent(valueStrategy = IdGeneratorStrategy.IDENTITY)
	private Long id;
	//其他的值设置一个@Persistent在前面就会保存到数据库里了
	@Persistent
	private User author;
	@Persistent
	private String content;
	@Persistent
	private Date date;

	//下面是一些Getter,Setter方法，对于JDO是不需要的，只是为了方便你写程序
	public Greeting(User author, String content, Date date) {
		super();
		this.author = author;
		this.content = content;
		this.date = date;
	}

	public Long getId() {
		return id;
	}

	public void setId(Long id) {
		this.id = id;
	}

	public User getAuthor() {
		return author;
	}

	public void setAuthor(User author) {
		this.author = author;
	}

	public String getContent() {
		return content;
	}

	public void setContent(String content) {
		this.content = content;
	}

	public Date getDate() {
		return date;
	}

	public void setDate(Date date) {
		this.date = date;
	}

}</pre>
## 二、我们还要创建PMF.java用来取得PersistenceManager。官方说取这个东西要花费很多资源，所以只获得一个就好，单例模式~

<pre lang="java">package com.fatkun.guestbook;

import javax.jdo.JDOHelper;
import javax.jdo.PersistenceManagerFactory;

/**
 * 用来取得PersistenceManager
 * @author Administrator
 *
 */
public final class PMF {
	private static final PersistenceManagerFactory pmfInstance = JDOHelper.getPersistenceManagerFactory("transactions-optional");

	private PMF() {
	}

	public static PersistenceManagerFactory get() {
		return pmfInstance;
	}
}</pre>
## 三、我们在war目录下新建一个guestbook.jsp用来显示所有留言

<pre escaped="true" lang="java">&lt;?xml version="1.0" encoding="UTF-8" ?&gt;
&lt;%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%&gt;
&lt;%@ page import="java.util.List"%&gt;
&lt;%@ page import="javax.jdo.PersistenceManager"%&gt;
&lt;%@ page import="com.google.appengine.api.users.User"%&gt;
&lt;%@ page import="com.google.appengine.api.users.UserService"%&gt;
&lt;%@ page import="com.google.appengine.api.users.UserServiceFactory"%&gt;
&lt;%@ page import="com.fatkun.guestbook.Greeting"%&gt;
&lt;%@ page import="com.fatkun.guestbook.PMF"%&gt;

&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"&gt;
&lt;html xmlns="http://www.w3.org/1999/xhtml"&gt;
&lt;head&gt;
&lt;meta http-equiv="Content-Type" content="text/html; charset=UTF-8" /&gt;
&lt;title&gt;Google App Engine留言板 - fatkun.com&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;%
	UserService userService = UserServiceFactory.getUserService();
	User user = userService.getCurrentUser();
	if (user != null) {
%&gt;
&lt;p&gt;你好, &lt;%=user.getNickname()%&gt;! (&lt;a href="&lt;%=userService.createLogoutURL(request.getRequestURI())%&gt;"&gt;退出&lt;/a&gt;.)&lt;/p&gt;
&lt;%
	} else {
%&gt;
&lt;p&gt;你好! 你可以使用google账号&lt;a href="&lt;%=userService.createLoginURL(request.getRequestURI())%&gt;"&gt;登陆&lt;/a&gt;&lt;/p&gt;
&lt;%
	}
%&gt;

&lt;%
	PersistenceManager pm = PMF.get().getPersistenceManager();
	//String query = "select from " + Greeting.class.getName()+" order by id desc";
	//也可以写成下面的形式
	String query = "select from com.fatkun.guestbook.Greeting order by id desc";
	List&lt;Greeting&gt; greetings = (List&lt;Greeting&gt;) pm.newQuery(query).execute();
	if (greetings.isEmpty()) {
%&gt;
&lt;p&gt;还没有留言。&lt;/p&gt;
&lt;%
	} else {
		for (Greeting g : greetings) {
			if (g.getAuthor() == null) {
				out.print("&lt;p&gt;一位匿名人士说:&lt;/p&gt;");
			} else {
				out.print("&lt;p&gt;&lt;b&gt;"+g.getAuthor().getNickname()+"&lt;/b&gt; 说:&lt;/p&gt;");
			}
%&gt;
&lt;a href="del?id=&lt;%=g.getId()%&gt;"&gt;删除&lt;/a&gt; - &lt;a href="guestbook-modify.jsp?id=&lt;%=g.getId()%&gt;"&gt;修改&lt;/a&gt;
&lt;blockquote&gt;&lt;%=g.getContent()%&gt;&lt;/blockquote&gt;
&lt;%
	}
	}
	pm.close();
%&gt;

&lt;form action="/add" method="post"&gt;
&lt;div&gt;&lt;textarea name="content" rows="3" cols="60"&gt;&lt;/textarea&gt;&lt;/div&gt;
&lt;div&gt;&lt;input type="submit" value="我要留言" /&gt;&lt;/div&gt;
&lt;/form&gt;

&lt;/body&gt;
&lt;/html&gt;</pre>
这里注意要引入自己使用的包~~GQL是针对对象来写查询语句的~~有点儿像Hibernate的HQL~
## 四、没有内容怎么显示呢~我们加一个添加到数据库的GuestbookAddServlet.java

<pre lang="java">package com.fatkun.guestbook;

import java.io.IOException;
import java.util.Date;

import javax.jdo.PersistenceManager;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import com.google.appengine.api.users.User;
import com.google.appengine.api.users.UserService;
import com.google.appengine.api.users.UserServiceFactory;

@SuppressWarnings("serial")
public class GuestbookAddServlet extends HttpServlet {

	@Override
	protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		//取得用户Service，这里是Google的用户管理
		UserService userService = UserServiceFactory.getUserService();
		//取得当前登录的用户，当不存在的时候为null
		User user = userService.getCurrentUser();

		String content = req.getParameter("content");
		Date date = new Date();
		//创建一个Greeting对象
		Greeting greeting = new Greeting(user, content, date);

		PersistenceManager pm = PMF.get().getPersistenceManager();
		try {
			//持久化~也就是把greeting添加进数据库
			pm.makePersistent(greeting);
		} finally {
			pm.close();
		}
		resp.sendRedirect("guestbook.jsp");
	}

}</pre>
写完了上面这个文件，注意还得在web.xml加入下面的，要告诉服务器说，我在这里啊，你可以通过这个链接找我~~
<pre escaped="true" lang="xml">&lt;servlet&gt;
		&lt;servlet-name&gt;add&lt;/servlet-name&gt;
		&lt;servlet-class&gt;com.fatkun.guestbook.GuestbookAddServlet&lt;/servlet-class&gt;
	&lt;/servlet&gt;
	&lt;servlet-mapping&gt;
		&lt;servlet-name&gt;add&lt;/servlet-name&gt;
		&lt;url-pattern&gt;/add&lt;/url-pattern&gt;
	&lt;/servlet-mapping&gt;</pre>
这时，你应该就可以留言啦~~运行一下试试~~可以先在本地测试，再上传到GAE服务器上。
伍、我最后给出修改和删除的部分代码~其实就主要是数据库的问题~~
GuestbookModifyServlet.java
<pre lang="java">protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		Long id = Long.parseLong(req.getParameter("id"));
		String content = req.getParameter("content");

		//先获取PersistenceManager
		PersistenceManager pm = PMF.get().getPersistenceManager();
		try {
			//根据ID从数据库得到一条记录
			Greeting greeting = pm.getObjectById(Greeting.class, id);
			//修改记录
			greeting.setContent(content);
		} finally {
			//当关闭pm的时候，会自动把已经修改的记录更新到数据库
			pm.close();
		}
		resp.sendRedirect("guestbook.jsp");
	}</pre>
GuestbookDeleteServlet.java
<pre lang="java">protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		Long id = Long.parseLong(req.getParameter("id"));

		PersistenceManager pm = PMF.get().getPersistenceManager();
		try {
			//取得这条记录
			Greeting greeting = pm.getObjectById(Greeting.class, id);
			//删除
			pm.deletePersistent(greeting);
		} finally {
			//关闭
			pm.close();
		}
		resp.sendRedirect("guestbook.jsp");
	}</pre>
好，一个简单的留言板就这样诞生了~~如果想弄得更加漂亮，就自己弄吧~~^_^  
我做的例子：<http://1.latest.fatkuns.appspot.com/>

 [1]: http://farm3.static.flickr.com/2771/4199535918_3d3cf61b53_o.jpg