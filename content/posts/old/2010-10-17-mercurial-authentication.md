---
title: Mercurial(HG)版本控制服务用户名验证
author: fatkun
type: post
date: 2010-10-17T03:22:18+00:00
url: /2010/10/mercurial-authentication.html
duoshuo_thread_id:
  - 6300408770774172418
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:379:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">htpasswd <span style="color: #339933;">-</span>c hguser fatkun.<span style="color: #006633;">com</span>
    htpasswd hguser aaaa</pre></td></tr></table><p class="theCode" style="display:none;">htpasswd -c hguser fatkun.com
    htpasswd hguser aaaa</p></div>
    ";i:2;s:1306:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;Location</span> /hg<span style="color: #000000; font-weight: bold;">&gt;</span></span>
        AuthType Basic
        AuthName &quot;Mercurial repositories&quot;
        AuthUserFile &quot;D:/Program Files/Apache2.2/conf/hguser&quot;
    	<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;LimitExcept</span> GET<span style="color: #000000; font-weight: bold;">&gt;</span></span>
            Require valid-user
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/LimitExcept<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/Location<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">&lt;Location /hg&gt;
        AuthType Basic
        AuthName &quot;Mercurial repositories&quot;
        AuthUserFile &quot;D:/Program Files/Apache2.2/conf/hguser&quot;
    	&lt;LimitExcept GET&gt;
            Require valid-user
        &lt;/LimitExcept&gt;
    &lt;/Location&gt;</p></div>
    ";i:3;s:678:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;">[web]
    allowpull = false //不允许所有人下载该项目
    allow_read = &quot;John Doe, PhD&quot;, fatkun//允许哪些人可以下载，如果有空格或特殊字符用引号&quot;&quot;括起来
    //还有deny_read，allow_push 等等</pre></td></tr></table><p class="theCode" style="display:none;">[web]
    allowpull = false //不允许所有人下载该项目
    allow_read = &quot;John Doe, PhD&quot;, fatkun//允许哪些人可以下载，如果有空格或特殊字符用引号&quot;&quot;括起来
    //还有deny_read，allow_push 等等</p></div>
    ";}
categories:
  - J2EE
tags:
  - hg
  - htpasswd
  - 权限设置
  - 版本控制

---
在之前的文章中，**<a rel="bookmark" href="http://fatkun.com/2010/08/mercurial-server-with-apache.html">在Windows使用apache搭建Mercurial版本控制服务</a><span style="font-weight: normal;">，并没有说到如何验证用户，而是允许所有人都提交。当时还不会怎么配置。</span>**
<span style="font-size: medium;"><span>以下就是配置方法：</span></span>
## <span style="font-size: medium;">1，用htpasswd.exe建立用户密码文件</span>

<span style="font-size: medium;">htpasswd.exe在apache的bin目录可以找到，使用方法主要有</span>
<span style="font-size: small;">htpasswd -c 文件名 用户名               //参数-c创建密码文件，输入后会提示你输入密码</span>
<span style="font-size: small;">htpasswd 文件名 用户名                 //如果用户名一样会更新密码</span>
<span style="font-size: small;">举个例子，我现在要建两个用户</span>
<pre escaped="true" lang="java">htpasswd -c hguser fatkun.com
htpasswd hguser aaaa</pre>
这时会得到一个hguser的文件，把它拷贝到conf目录下
## 2,修改httpd.conf配置

在httpd.conf配置最末尾加入，注意路径改为你的
<pre escaped="true" lang="xml">&lt;Location /hg&gt;
    AuthType Basic
    AuthName "Mercurial repositories"
    AuthUserFile "D:/Program Files/Apache2.2/conf/hguser"
	&lt;LimitExcept GET&gt;
        Require valid-user
    &lt;/LimitExcept&gt;
&lt;/Location&gt;</pre>
这样就可以了，重启apache服务以后，试试从浏览器访问hg的网页？会提示你输入用户名和密码。
## 3，针对某些项目的权限设置

在服务器存放项目的文件中，在.hg目录新建一个hgrc文件，里面可以配置为  
这里是配置单个项目的，如果需要对所有项目配置，可以修改hgweb.config文件
<pre escaped="true" lang="xml">[web]
allowpull = false //不允许所有人下载该项目
allow_read = "John Doe, PhD", fatkun//允许哪些人可以下载，如果有空格或特殊字符用引号""括起来
//还有deny_read，allow_push 等等</pre>
更多的配置可以查看这里<http://www.selenic.com/mercurial/hgrc.5.html>