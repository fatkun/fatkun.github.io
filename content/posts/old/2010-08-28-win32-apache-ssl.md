---
title: Windows平台Apache2.x配置SSL
author: fatkun
type: post
date: 2010-08-28T06:32:39+00:00
url: /2010/08/win32-apache-ssl.html
duoshuo_thread_id:
  - 6300408764465939202
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:435:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">openssl req <span style="color: #660033;">-config</span> ..\conf\openssl.cnf <span style="color: #660033;">-new</span> <span style="color: #660033;">-out</span> server.csr</pre></td></tr></table><p class="theCode" style="display:none;">openssl req -config ..\conf\openssl.cnf -new -out server.csr</p></div>
    ";i:2;s:364:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">openssl rsa <span style="color: #660033;">-in</span> privkey.pem <span style="color: #660033;">-out</span> server.key</pre></td></tr></table><p class="theCode" style="display:none;">openssl rsa -in privkey.pem -out server.key</p></div>
    ";i:3;s:584:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">openssl x509 <span style="color: #660033;">-in</span> server.csr <span style="color: #660033;">-out</span> server.crt <span style="color: #660033;">-req</span> <span style="color: #660033;">-signkey</span> server.key <span style="color: #660033;">-days</span> <span style="color: #000000;">4000</span></pre></td></tr></table><p class="theCode" style="display:none;">openssl x509 -in server.csr -out server.crt -req -signkey server.key -days 4000</p></div>
    ";}
categories:
  - 电脑知识
tags:
  - Apache
  - SSL
  - win32

---
需要在apache配置SSL，所以找了几篇文章，摘录如下：  
参考网址：  
[Windows平台下Apache2.2.4的SSL配置过程(及错误整理)][1]  
[Windows环境下配置Apache 2.2.x + SSL][2]
&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-摘录部分By fatkun，部分有删改简化&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;
## 安装Apache

下载带有SSL的Apache，<http://httpd.apache.org/download.cgi>（Win32 Binary including OpenSSL 0.9.8o (MSI Installer)）  
安装以后，需要配置SSL。
打开conf/httpd.conf文件  
默认目录为：C:\Program Files\Apache Software Foundation\Apache2.2\conf
将下面两行前面的#号去掉：  
LoadModule ssl\_module modules/mod\_ssl.so  
Include conf/extra/httpd-ssl.conf
## 生成SSL证书

到这一步，剩下的就是如何生成SSL配置所需要的两个文件了：  
server.crt  
server.key
打开CMD，cd切换到C:\Program Files\Apache Software Foundation\Apache2.2\bin目录下运行以下命令  
首先需要建立证书签名请求和私钥文件：
<pre lang="bash" escaped="true">openssl req -config ..\conf\openssl.cnf -new -out server.csr</pre>
它会问一系列的问题，第一个是密码，要记住，下一步要用到  
然后RSA签名：
<pre lang="bash" escaped="true">openssl rsa -in privkey.pem -out server.key</pre>
最后创建自签证书：
<pre lang="bash" escaped="true">openssl x509 -in server.csr -out server.crt -req -signkey server.key -days 4000</pre>
完成之后，将生成的server.crt和server.key这两个文件拷贝到apache的conf目录下。
现在使用https://www.yourdomain.com，应该就可以看到It works了。

 [1]: http://mdjhaitao.blog.163.com/blog/static/10143121200772333432345/
 [2]: http://wangxiaojs.javaeye.com/blog/294328