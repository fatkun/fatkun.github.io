---
title: 用一个Tomcat建立多个Server
author: fatkun
type: post
date: 2010-09-16T12:41:37+00:00
url: /2010/09/tomcat-with-multiple-server.html
duoshuo_thread_id:
  - 6300408770291827457
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:1953:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="line_numbers"><pre>1
    2
    </pre></td><td class="code"><pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;Context</span> <span style="color: #000066;">path</span>=<span style="color: #ff0000;">&quot;app1&quot;</span> <span style="color: #000066;">docBase</span>=<span style="color: #ff0000;">&quot;E:/workspace/app1/WebRoot&quot;</span> <span style="color: #000066;">debug</span>=<span style="color: #ff0000;">&quot;0&quot;</span> <span style="color: #000066;">reloadable</span>=<span style="color: #ff0000;">&quot;true&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span><span style="color: #000000; font-weight: bold;">&lt;/Context<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;Context</span> <span style="color: #000066;">path</span>=<span style="color: #ff0000;">&quot;app2&quot;</span> <span style="color: #000066;">docBase</span>=<span style="color: #ff0000;">&quot;E:/workspace/app2/WebRoot&quot;</span> <span style="color: #000066;">debug</span>=<span style="color: #ff0000;">&quot;0&quot;</span> <span style="color: #000066;">reloadable</span>=<span style="color: #ff0000;">&quot;true&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span><span style="color: #000000; font-weight: bold;">&lt;/Context<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">&lt;Context path=&quot;app1&quot; docBase=&quot;E:/workspace/app1/WebRoot&quot; debug=&quot;0&quot; reloadable=&quot;true&quot;&gt;&lt;/Context&gt;
    &lt;Context path=&quot;app2&quot; docBase=&quot;E:/workspace/app2/WebRoot&quot; debug=&quot;0&quot; reloadable=&quot;true&quot;&gt;&lt;/Context&gt;</p></div>
    ";i:2;s:3213:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="line_numbers"><pre>1
    2
    3
    4
    5
    6
    </pre></td><td class="code"><pre class="xml" style="font-family:monospace;">  <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;Host</span> <span style="color: #000066;">appBase</span>=<span style="color: #ff0000;">&quot;webapps&quot;</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;192.168.1.110&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
       <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;Context</span> <span style="color: #000066;">path</span>=<span style="color: #ff0000;">&quot;&quot;</span> <span style="color: #000066;">docBase</span>=<span style="color: #ff0000;">&quot;E:/workspace/app1/WebRoot&quot;</span> <span style="color: #000066;">debug</span>=<span style="color: #ff0000;">&quot;0&quot;</span> <span style="color: #000066;">reloadable</span>=<span style="color: #ff0000;">&quot;true&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span><span style="color: #000000; font-weight: bold;">&lt;/Context<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/Host<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;Host</span> <span style="color: #000066;">appBase</span>=<span style="color: #ff0000;">&quot;webapps&quot;</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;192.168.1.114&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
       <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;Context</span> <span style="color: #000066;">path</span>=<span style="color: #ff0000;">&quot;&quot;</span> <span style="color: #000066;">docBase</span>=<span style="color: #ff0000;">&quot;E:/workspace/app2/WebRoot&quot;</span> <span style="color: #000066;">debug</span>=<span style="color: #ff0000;">&quot;0&quot;</span> <span style="color: #000066;">reloadable</span>=<span style="color: #ff0000;">&quot;true&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span><span style="color: #000000; font-weight: bold;">&lt;/Context<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/Host<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">  &lt;Host appBase=&quot;webapps&quot; name=&quot;192.168.1.110&quot;&gt;
       &lt;Context path=&quot;&quot; docBase=&quot;E:/workspace/app1/WebRoot&quot; debug=&quot;0&quot; reloadable=&quot;true&quot;&gt;&lt;/Context&gt;
      &lt;/Host&gt;
      &lt;Host appBase=&quot;webapps&quot; name=&quot;192.168.1.114&quot;&gt;
       &lt;Context path=&quot;&quot; docBase=&quot;E:/workspace/app2/WebRoot&quot; debug=&quot;0&quot; reloadable=&quot;true&quot;&gt;&lt;/Context&gt;
      &lt;/Host&gt;</p></div>
    ";i:3;s:10648:"
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
    </pre></td><td class="code"><pre class="xml" style="font-family:monospace;">  <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;Service</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;Catalina1&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;Connector</span> <span style="color: #000066;">port</span>=<span style="color: #ff0000;">&quot;90&quot;</span> <span style="color: #000066;">protocol</span>=<span style="color: #ff0000;">&quot;HTTP/1.1&quot;</span>  <span style="color: #000066;">connectionTimeout</span>=<span style="color: #ff0000;">&quot;20000&quot;</span>  <span style="color: #000066;">redirectPort</span>=<span style="color: #ff0000;">&quot;8443&quot;</span> <span style="color: #000066;">URIEncoding</span>=<span style="color: #ff0000;">&quot;gbk&quot;</span> <span style="color: #000000; font-weight: bold;">/&gt;</span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;Connector</span> <span style="color: #000066;">port</span>=<span style="color: #ff0000;">&quot;8009&quot;</span> <span style="color: #000066;">protocol</span>=<span style="color: #ff0000;">&quot;AJP/1.3&quot;</span> <span style="color: #000066;">redirectPort</span>=<span style="color: #ff0000;">&quot;8443&quot;</span> <span style="color: #000000; font-weight: bold;">/&gt;</span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;Engine</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;Catalina2&quot;</span> <span style="color: #000066;">defaultHost</span>=<span style="color: #ff0000;">&quot;localhost&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
          <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;Realm</span> <span style="color: #000066;">className</span>=<span style="color: #ff0000;">&quot;org.apache.catalina.realm.UserDatabaseRealm&quot;</span>  <span style="color: #000066;">resourceName</span>=<span style="color: #ff0000;">&quot;UserDatabase&quot;</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
          <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;Host</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;localhost&quot;</span>  <span style="color: #000066;">appBase</span>=<span style="color: #ff0000;">&quot;webapps&quot;</span> <span style="color: #000066;">unpackWARs</span>=<span style="color: #ff0000;">&quot;true&quot;</span> <span style="color: #000066;">autoDeploy</span>=<span style="color: #ff0000;">&quot;true&quot;</span>  <span style="color: #000066;">xmlValidation</span>=<span style="color: #ff0000;">&quot;false&quot;</span> <span style="color: #000066;">xmlNamespaceAware</span>=<span style="color: #ff0000;">&quot;false&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
    			<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;Context</span> <span style="color: #000066;">path</span>=<span style="color: #ff0000;">&quot;&quot;</span> <span style="color: #000066;">docBase</span>=<span style="color: #ff0000;">&quot;F:/workspace/app1/WebRoot&quot;</span> <span style="color: #000066;">debug</span>=<span style="color: #ff0000;">&quot;0&quot;</span> <span style="color: #000066;">reloadable</span>=<span style="color: #ff0000;">&quot;true&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span><span style="color: #000000; font-weight: bold;">&lt;/Context<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
          <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/Host<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/Engine<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/Service<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;Service</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;Catalina2&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;Connector</span> <span style="color: #000066;">port</span>=<span style="color: #ff0000;">&quot;91&quot;</span> <span style="color: #000066;">protocol</span>=<span style="color: #ff0000;">&quot;HTTP/1.1&quot;</span>  <span style="color: #000066;">connectionTimeout</span>=<span style="color: #ff0000;">&quot;20000&quot;</span>  <span style="color: #000066;">redirectPort</span>=<span style="color: #ff0000;">&quot;8443&quot;</span> <span style="color: #000066;">URIEncoding</span>=<span style="color: #ff0000;">&quot;gbk&quot;</span> <span style="color: #000000; font-weight: bold;">/&gt;</span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;Connector</span> <span style="color: #000066;">port</span>=<span style="color: #ff0000;">&quot;8009&quot;</span> <span style="color: #000066;">protocol</span>=<span style="color: #ff0000;">&quot;AJP/1.3&quot;</span> <span style="color: #000066;">redirectPort</span>=<span style="color: #ff0000;">&quot;8443&quot;</span> <span style="color: #000000; font-weight: bold;">/&gt;</span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;Engine</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;Catalina2&quot;</span> <span style="color: #000066;">defaultHost</span>=<span style="color: #ff0000;">&quot;localhost&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
          <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;Realm</span> <span style="color: #000066;">className</span>=<span style="color: #ff0000;">&quot;org.apache.catalina.realm.UserDatabaseRealm&quot;</span>  <span style="color: #000066;">resourceName</span>=<span style="color: #ff0000;">&quot;UserDatabase&quot;</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
          <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;Host</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;localhost&quot;</span>  <span style="color: #000066;">appBase</span>=<span style="color: #ff0000;">&quot;webapps&quot;</span> <span style="color: #000066;">unpackWARs</span>=<span style="color: #ff0000;">&quot;true&quot;</span> <span style="color: #000066;">autoDeploy</span>=<span style="color: #ff0000;">&quot;true&quot;</span>  <span style="color: #000066;">xmlValidation</span>=<span style="color: #ff0000;">&quot;false&quot;</span> <span style="color: #000066;">xmlNamespaceAware</span>=<span style="color: #ff0000;">&quot;false&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
    			<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;Context</span> <span style="color: #000066;">path</span>=<span style="color: #ff0000;">&quot;&quot;</span> <span style="color: #000066;">docBase</span>=<span style="color: #ff0000;">&quot;F:/workspace/app2/WebRoot&quot;</span> <span style="color: #000066;">debug</span>=<span style="color: #ff0000;">&quot;0&quot;</span> <span style="color: #000066;">reloadable</span>=<span style="color: #ff0000;">&quot;true&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span><span style="color: #000000; font-weight: bold;">&lt;/Context<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
          <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/Host<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/Engine<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/Service<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">  &lt;Service name=&quot;Catalina1&quot;&gt;
        &lt;Connector port=&quot;90&quot; protocol=&quot;HTTP/1.1&quot;  connectionTimeout=&quot;20000&quot;  redirectPort=&quot;8443&quot; URIEncoding=&quot;gbk&quot; /&gt;
        &lt;Connector port=&quot;8009&quot; protocol=&quot;AJP/1.3&quot; redirectPort=&quot;8443&quot; /&gt;
        &lt;Engine name=&quot;Catalina2&quot; defaultHost=&quot;localhost&quot;&gt;
          &lt;Realm className=&quot;org.apache.catalina.realm.UserDatabaseRealm&quot;  resourceName=&quot;UserDatabase&quot;/&gt;
          &lt;Host name=&quot;localhost&quot;  appBase=&quot;webapps&quot; unpackWARs=&quot;true&quot; autoDeploy=&quot;true&quot;  xmlValidation=&quot;false&quot; xmlNamespaceAware=&quot;false&quot;&gt;
    			&lt;Context path=&quot;&quot; docBase=&quot;F:/workspace/app1/WebRoot&quot; debug=&quot;0&quot; reloadable=&quot;true&quot;&gt;&lt;/Context&gt;
          &lt;/Host&gt;
        &lt;/Engine&gt;
      &lt;/Service&gt;
      &lt;Service name=&quot;Catalina2&quot;&gt;
        &lt;Connector port=&quot;91&quot; protocol=&quot;HTTP/1.1&quot;  connectionTimeout=&quot;20000&quot;  redirectPort=&quot;8443&quot; URIEncoding=&quot;gbk&quot; /&gt;
        &lt;Connector port=&quot;8009&quot; protocol=&quot;AJP/1.3&quot; redirectPort=&quot;8443&quot; /&gt;
        &lt;Engine name=&quot;Catalina2&quot; defaultHost=&quot;localhost&quot;&gt;
          &lt;Realm className=&quot;org.apache.catalina.realm.UserDatabaseRealm&quot;  resourceName=&quot;UserDatabase&quot;/&gt;
          &lt;Host name=&quot;localhost&quot;  appBase=&quot;webapps&quot; unpackWARs=&quot;true&quot; autoDeploy=&quot;true&quot;  xmlValidation=&quot;false&quot; xmlNamespaceAware=&quot;false&quot;&gt;
    			&lt;Context path=&quot;&quot; docBase=&quot;F:/workspace/app2/WebRoot&quot; debug=&quot;0&quot; reloadable=&quot;true&quot;&gt;&lt;/Context&gt;
          &lt;/Host&gt;
        &lt;/Engine&gt;
      &lt;/Service&gt;</p></div>
    ";}
categories:
  - J2EE
tags:
  - tomcat分享JVM
  - Tomcat绑定域名

---
## 1.通过配置多个<Context>元素（不同目录）

(fatkun:这个和直接放在webapps不用配置差不多)
在<Host>下配置多个<Context>元素
<pre escaped="true" lang="xml" line="1">&lt;Context path="app1" docBase="E:/workspace/app1/WebRoot" debug="0" reloadable="true"&gt;&lt;/Context&gt;
&lt;Context path="app2" docBase="E:/workspace/app2/WebRoot" debug="0" reloadable="true"&gt;&lt;/Context&gt;</pre>
然后通过 主机名:端口/应用名 访问,如: http://localhost:8080/app1 或 http://localhost:8080/app2
## 2.通过配置多个<Host>元素（不同域名）

<pre escaped="true" lang="xml" line="1">&lt;Host appBase="webapps" name="192.168.1.110"&gt;
   &lt;Context path="" docBase="E:/workspace/app1/WebRoot" debug="0" reloadable="true"&gt;&lt;/Context&gt;
  &lt;/Host&gt;
  &lt;Host appBase="webapps" name="192.168.1.114"&gt;
   &lt;Context path="" docBase="E:/workspace/app2/WebRoot" debug="0" reloadable="true"&gt;&lt;/Context&gt;
  &lt;/Host&gt;</pre>
然后通过 主机名:端口 访问,如: http://192.168.1.110:8080 或 http://192.168.1.114:8080  
name中的192.168.1.110可以是你的域名或者需要绑定的IP
## 3.通过配置多个<Service>元素(不同端口)

在<Server>下配置多个<Service>元素
<pre escaped="true" lang="xml" line="1">&lt;Service name="Catalina1"&gt;
    &lt;Connector port="90" protocol="HTTP/1.1"  connectionTimeout="20000"  redirectPort="8443" URIEncoding="gbk" /&gt;
    &lt;Connector port="8009" protocol="AJP/1.3" redirectPort="8443" /&gt;
    &lt;Engine name="Catalina2" defaultHost="localhost"&gt;
      &lt;Realm className="org.apache.catalina.realm.UserDatabaseRealm"  resourceName="UserDatabase"/&gt;
      &lt;Host name="localhost"  appBase="webapps" unpackWARs="true" autoDeploy="true"  xmlValidation="false" xmlNamespaceAware="false"&gt;
			&lt;Context path="" docBase="F:/workspace/app1/WebRoot" debug="0" reloadable="true"&gt;&lt;/Context&gt;
      &lt;/Host&gt;
    &lt;/Engine&gt;
  &lt;/Service&gt;
  &lt;Service name="Catalina2"&gt;
    &lt;Connector port="91" protocol="HTTP/1.1"  connectionTimeout="20000"  redirectPort="8443" URIEncoding="gbk" /&gt;
    &lt;Connector port="8009" protocol="AJP/1.3" redirectPort="8443" /&gt;
    &lt;Engine name="Catalina2" defaultHost="localhost"&gt;
      &lt;Realm className="org.apache.catalina.realm.UserDatabaseRealm"  resourceName="UserDatabase"/&gt;
      &lt;Host name="localhost"  appBase="webapps" unpackWARs="true" autoDeploy="true"  xmlValidation="false" xmlNamespaceAware="false"&gt;
			&lt;Context path="" docBase="F:/workspace/app2/WebRoot" debug="0" reloadable="true"&gt;&lt;/Context&gt;
      &lt;/Host&gt;
    &lt;/Engine&gt;
  &lt;/Service&gt;</pre>
定义了两个Service分别是Catalina和Catalina2,侦听的端口分别是90和91  
然后通过 主机名:端口 访问,如: http://localhost:90 或 http://localhost:91
原文来自：<http://www.blogjava.net/siyn/archive/2008/07/07/213133.html>