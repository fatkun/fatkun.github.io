---
title: 在MyEclipse Tomcat配置JNDI(mysql)
author: fatkun
type: post
date: 2010-09-05T14:16:36+00:00
url: /2010/09/myeclipse-tomcat-jndi.html
duoshuo_thread_id:
  - 6300408764579185409
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:2316:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;">	<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;Resource</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;jdbc/xxxx&quot;</span> <span style="color: #000066;">auth</span>=<span style="color: #ff0000;">&quot;Container&quot;</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">&quot;javax.sql.DataSource&quot;</span></span>
    <span style="color: #009900;">	<span style="color: #000066;">maxActive</span>=<span style="color: #ff0000;">&quot;100&quot;</span> <span style="color: #000066;">maxIdle</span>=<span style="color: #ff0000;">&quot;30&quot;</span> <span style="color: #000066;">maxWait</span>=<span style="color: #ff0000;">&quot;1000&quot;</span> <span style="color: #000066;">username</span>=<span style="color: #ff0000;">&quot;root&quot;</span> <span style="color: #000066;">password</span>=<span style="color: #ff0000;">&quot;123&quot;</span></span>
    <span style="color: #009900;">	<span style="color: #000066;">driverClassName</span>=<span style="color: #ff0000;">&quot;com.mysql.jdbc.Driver&quot;</span> <span style="color: #000066;">url</span>=<span style="color: #ff0000;">&quot;jdbc:mysql://127.0.0.1:3306/xxxxxxxxxx&quot;</span></span>
    <span style="color: #009900;">	<span style="color: #000066;">removeAbandoned</span>=<span style="color: #ff0000;">&quot;true&quot;</span> <span style="color: #000066;">removeAbandonedTimeout</span>=<span style="color: #ff0000;">&quot;60&quot;</span> <span style="color: #000066;">logAbandoned</span>=<span style="color: #ff0000;">&quot;true&quot;</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span></pre></td></tr></table><p class="theCode" style="display:none;">	&lt;Resource name=&quot;jdbc/xxxx&quot; auth=&quot;Container&quot; type=&quot;javax.sql.DataSource&quot;
    	maxActive=&quot;100&quot; maxIdle=&quot;30&quot; maxWait=&quot;1000&quot; username=&quot;root&quot; password=&quot;123&quot;
    	driverClassName=&quot;com.mysql.jdbc.Driver&quot; url=&quot;jdbc:mysql://127.0.0.1:3306/xxxxxxxxxx&quot;
    	removeAbandoned=&quot;true&quot; removeAbandonedTimeout=&quot;60&quot; logAbandoned=&quot;true&quot;/&gt;</p></div>
    ";}
categories:
  - J2EE
tags:
  - jndi
  - MyEclipse
  - mysql
  - tomcat

---
在<workspace目录>\.metadata\.me_tcat\conf目录下找到context.xml文件  
加入以下内容，按照需要进行更改
<pre escaped="true" lang="xml">&lt;Resource name="jdbc/xxxx" auth="Container" type="javax.sql.DataSource"
	maxActive="100" maxIdle="30" maxWait="1000" username="root" password="123"
	driverClassName="com.mysql.jdbc.Driver" url="jdbc:mysql://127.0.0.1:3306/xxxxxxxxxx"
	removeAbandoned="true" removeAbandonedTimeout="60" logAbandoned="true"/&gt;</pre>
在Myeclipse安装目录找到类似下面的路径，可能你的和我不太一样  
<Myeclipse安装目录>\Common\plugins\com.genuitec.eclipse.easie.tomcat.myeclipse_8.5.0.me201003121946\tomcat\lib
复制mysql的驱动包进这个目录