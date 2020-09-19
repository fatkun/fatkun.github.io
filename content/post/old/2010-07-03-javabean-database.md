---
title: 使用JavaBean操作数据库的例子(JSP)
author: fatkun
type: post
date: 2010-07-03T06:58:23+00:00
url: /2010/07/javabean-database.html
views:
  - 14
duoshuo_thread_id:
  - 6300408743632847618
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:11046:"
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
    28
    29
    30
    31
    32
    33
    34
    35
    36
    37
    38
    39
    40
    41
    42
    43
    44
    45
    46
    47
    48
    49
    50
    51
    52
    </pre></td><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">package</span> <span style="color: #006699;">DB</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">java.sql.*</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> Conn <span style="color: #009900;">&#123;</span>
    	<span style="color: #000000; font-weight: bold;">private</span> <span style="color: #003399;">String</span> db <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;test&quot;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">// 数据库名</span>
    	<span style="color: #000000; font-weight: bold;">private</span> <span style="color: #003399;">String</span> user <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;root&quot;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">// 数据库用户名</span>
    	<span style="color: #000000; font-weight: bold;">private</span> <span style="color: #003399;">String</span> pass <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;&quot;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">// 数据库密码</span>
    	<span style="color: #000000; font-weight: bold;">private</span> <span style="color: #003399;">String</span> drivername <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;com.mysql.jdbc.Driver&quot;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">// mysql driver</span>
    	<span style="color: #000000; font-weight: bold;">private</span> <span style="color: #003399;">String</span> <span style="color: #003399;">URL</span> <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;jdbc:mysql://localhost:3306/&quot;</span> <span style="color: #339933;">+</span> db
    			<span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot;?useUnicode=true&amp;characterEncoding=UTF8&amp;user=&quot;</span> <span style="color: #339933;">+</span> user
    			<span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot;&amp;password=&quot;</span> <span style="color: #339933;">+</span> pass<span style="color: #339933;">;</span>
    	<span style="color: #000000; font-weight: bold;">private</span> <span style="color: #003399;">Connection</span> conn <span style="color: #339933;">=</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #339933;">;</span>
    &nbsp;
    	<span style="color: #000000; font-weight: bold;">public</span> Conn<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#123;</span>
    		conn <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">getConn</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span>
    &nbsp;
    	<span style="color: #000000; font-weight: bold;">public</span> <span style="color: #003399;">Connection</span> getConn<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span> <span style="color: #666666; font-style: italic;">// get database connection</span>
    		<span style="color: #003399;">Connection</span> aconn <span style="color: #339933;">=</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #339933;">;</span>
    		<span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#123;</span>
    			<span style="color: #000000; font-weight: bold;">Class</span>.<span style="color: #006633;">forName</span><span style="color: #009900;">&#40;</span>drivername<span style="color: #009900;">&#41;</span>.<span style="color: #006633;">newInstance</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">// 载入驱动器</span>
    			aconn <span style="color: #339933;">=</span> <span style="color: #003399;">DriverManager</span>.<span style="color: #006633;">getConnection</span><span style="color: #009900;">&#40;</span><span style="color: #003399;">URL</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">// 连接到数据库</span>
    		<span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">Exception</span> e<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    			e.<span style="color: #006633;">printStackTrace</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #009900;">&#125;</span>
    		<span style="color: #000000; font-weight: bold;">return</span> aconn<span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span>
    &nbsp;
    	<span style="color: #000000; font-weight: bold;">public</span> <span style="color: #003399;">ResultSet</span> executeQuery<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> str<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    		<span style="color: #003399;">ResultSet</span> rs <span style="color: #339933;">=</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #339933;">;</span>
    		<span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#123;</span>
    			<span style="color: #003399;">Statement</span> stmt <span style="color: #339933;">=</span> conn.<span style="color: #006633;">createStatement</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">// 语句接口</span>
    			rs <span style="color: #339933;">=</span> stmt.<span style="color: #006633;">executeQuery</span><span style="color: #009900;">&#40;</span>str<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">// 获得结果集</span>
    		<span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">Exception</span> e<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    			e.<span style="color: #006633;">printStackTrace</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #009900;">&#125;</span>
    		<span style="color: #000000; font-weight: bold;">return</span> rs<span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span>
    &nbsp;
    	<span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">int</span> executeUpdate<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> str<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    		<span style="color: #000066; font-weight: bold;">int</span> ret <span style="color: #339933;">=</span> <span style="color: #cc66cc;">0</span><span style="color: #339933;">;</span>
    		<span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#123;</span>
    			<span style="color: #003399;">Statement</span> stmt <span style="color: #339933;">=</span> conn.<span style="color: #006633;">createStatement</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    			ret <span style="color: #339933;">=</span> stmt.<span style="color: #006633;">executeUpdate</span><span style="color: #009900;">&#40;</span>str<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//执行sql语句，返回影响行数</span>
    		<span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">SQLException</span> e<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    			e.<span style="color: #006633;">printStackTrace</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #009900;">&#125;</span>
    		<span style="color: #000000; font-weight: bold;">return</span> ret<span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">package DB;
    
    import java.sql.*;
    
    public class Conn {
    	private String db = &quot;test&quot;; // 数据库名
    	private String user = &quot;root&quot;; // 数据库用户名
    	private String pass = &quot;&quot;; // 数据库密码
    	private String drivername = &quot;com.mysql.jdbc.Driver&quot;; // mysql driver
    	private String URL = &quot;jdbc:mysql://localhost:3306/&quot; + db
    			+ &quot;?useUnicode=true&amp;characterEncoding=UTF8&amp;user=&quot; + user
    			+ &quot;&amp;password=&quot; + pass;
    	private Connection conn = null;
    	
    	public Conn(){
    		conn = this.getConn();
    	}
    
    	public Connection getConn() { // get database connection
    		Connection aconn = null;
    		try {
    			Class.forName(drivername).newInstance(); // 载入驱动器
    			aconn = DriverManager.getConnection(URL); // 连接到数据库
    		} catch (Exception e) {
    			e.printStackTrace();
    		}
    		return aconn;
    	}
    
    	public ResultSet executeQuery(String str) {
    		ResultSet rs = null;
    		try {
    			Statement stmt = conn.createStatement(); // 语句接口
    			rs = stmt.executeQuery(str); // 获得结果集
    		} catch (Exception e) {
    			e.printStackTrace();
    		}
    		return rs;
    	}
    	
    	public int executeUpdate(String str) {
    		int ret = 0;
    		try {
    			Statement stmt = conn.createStatement();
    			ret = stmt.executeUpdate(str);//执行sql语句，返回影响行数
    		} catch (SQLException e) {
    			e.printStackTrace();
    		}
    		return ret;
    	}
    
    }</p></div>
    ";}
categories:
  - J2EE
tags:
  - javabean
  - jsp

---
这个只是一个登陆的 页面，只做了查询和增加。非常简洁，适合新手。  
1.使用前先创建一个数据库，然后用“查询”，用记事本打开user.sql内容，复制到SQL查询窗口运行，就会帮你建立一个user表和插入几条数据。  
2.Eclipse 中导入该项目即可，(菜单File->Import->General->Existing Projects into Workspace)  
3.src\DB\Conn.java为数据库连接代码，请修改为你本机对应的参数  
private String db = &#8220;test&#8221;; // 数据库名  
private String user = &#8220;root&#8221;; // 数据库用户名  
private String pass = &#8220;&#8221;; // 数据库密码
<pre escaped="true" lang="java" line="1">package DB;

import java.sql.*;

public class Conn {
	private String db = "test"; // 数据库名
	private String user = "root"; // 数据库用户名
	private String pass = ""; // 数据库密码
	private String drivername = "com.mysql.jdbc.Driver"; // mysql driver
	private String URL = "jdbc:mysql://localhost:3306/" + db
			+ "?useUnicode=true&characterEncoding=UTF8&user=" + user
			+ "&password=" + pass;
	private Connection conn = null;
	
	public Conn(){
		conn = this.getConn();
	}

	public Connection getConn() { // get database connection
		Connection aconn = null;
		try {
			Class.forName(drivername).newInstance(); // 载入驱动器
			aconn = DriverManager.getConnection(URL); // 连接到数据库
		} catch (Exception e) {
			e.printStackTrace();
		}
		return aconn;
	}

	public ResultSet executeQuery(String str) {
		ResultSet rs = null;
		try {
			Statement stmt = conn.createStatement(); // 语句接口
			rs = stmt.executeQuery(str); // 获得结果集
		} catch (Exception e) {
			e.printStackTrace();
		}
		return rs;
	}
	
	public int executeUpdate(String str) {
		int ret = 0;
		try {
			Statement stmt = conn.createStatement();
			ret = stmt.executeUpdate(str);//执行sql语句，返回影响行数
		} catch (SQLException e) {
			e.printStackTrace();
		}
		return ret;
	}

}
</pre>
下载地址:<a href="http://cid-48ca6ece8e801d64.office.live.com/self.aspx/.Public/Demo%5E_JavaBean.rar" target="_blank">http://cid-48ca6ece8e801d64.office.live.com/self.aspx/.Public/Demo%5E_JavaBean.rar</a>