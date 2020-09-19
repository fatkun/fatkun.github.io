---
title: 在Windows使用apache搭建Mercurial版本控制服务
author: fatkun
type: post
date: 2010-08-29T07:40:28+00:00
url: /2010/08/mercurial-server-with-apache.html
duoshuo_thread_id:
  - 6300408764403024641
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:3350:"
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
    </pre></td><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #808080; font-style: italic;">#!C:/Python26/python.exe</span>
    <span style="color: #808080; font-style: italic;">#</span>
    <span style="color: #808080; font-style: italic;"># An example CGI script to export multiple hgweb repos, edit as necessary</span>
    <span style="color: #808080; font-style: italic;"># 配置为你的library.zip解压的目录:</span>
    <span style="color: #ff7700;font-weight:bold;">import</span> <span style="color: #dc143c;">sys</span>
    <span style="color: #dc143c;">sys</span>.<span style="color: black;">path</span>.<span style="color: black;">insert</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">&quot;D:<span style="color: #000099; font-weight: bold;">\\</span>xampplite<span style="color: #000099; font-weight: bold;">\\</span>mlib&quot;</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">from</span> mercurial <span style="color: #ff7700;font-weight:bold;">import</span> demandimport<span style="color: #66cc66;">;</span>
    demandimport.<span style="color: black;">enable</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">import</span> <span style="color: #dc143c;">cgitb</span>
    <span style="color: #dc143c;">cgitb</span>.<span style="color: black;">enable</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #808080; font-style: italic;">#import os</span>
    <span style="color: #808080; font-style: italic;">#os.environ[&quot;HGENCODING&quot;] = &quot;UTF-8&quot;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">from</span> mercurial.<span style="color: black;">hgweb</span>.<span style="color: black;">hgwebdir_mod</span> <span style="color: #ff7700;font-weight:bold;">import</span> hgwebdir
    <span style="color: #ff7700;font-weight:bold;">import</span> mercurial.<span style="color: black;">hgweb</span>.<span style="color: black;">wsgicgi</span> <span style="color: #ff7700;font-weight:bold;">as</span> wsgicgi
    application <span style="color: #66cc66;">=</span> hgwebdir<span style="color: black;">&#40;</span><span style="color: #483d8b;">'hgweb.config'</span><span style="color: black;">&#41;</span>
    wsgicgi.<span style="color: black;">launch</span><span style="color: black;">&#40;</span>application<span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">#!C:/Python26/python.exe
    #
    # An example CGI script to export multiple hgweb repos, edit as necessary
    # 配置为你的library.zip解压的目录:
    import sys
    sys.path.insert(0, &quot;D:\\xampplite\\mlib&quot;)
    
    from mercurial import demandimport;
    demandimport.enable()
    
    import cgitb
    cgitb.enable()
    
    #import os
    #os.environ[&quot;HGENCODING&quot;] = &quot;UTF-8&quot;
    
    from mercurial.hgweb.hgwebdir_mod import hgwebdir
    import mercurial.hgweb.wsgicgi as wsgicgi
    application = hgwebdir('hgweb.config')
    wsgicgi.launch(application)</p></div>
    ";i:2;s:470:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="line_numbers"><pre>1
    2
    3
    4
    5
    6
    7
    </pre></td><td class="code"><pre class="xml" style="font-family:monospace;">[collections]
    F:/workspace/hg = F:/workspace/hg
    &nbsp;
    [web]
    allow_push =*
    push_ssl = false
    style = gitweb</pre></td></tr></table><p class="theCode" style="display:none;">[collections]
    F:/workspace/hg = F:/workspace/hg
    
    [web]
    allow_push =*
    push_ssl = false
    style = gitweb</p></div>
    ";i:3;s:1107:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="line_numbers"><pre>1
    2
    3
    4
    5
    6
    7
    </pre></td><td class="code"><pre class="xml" style="font-family:monospace;"># 版本管理
    ScriptAliasMatch ^/hg(.*) D:/xampplite/htdocs/hg/hgwebdir.cgi$1
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;Directory</span> <span style="color: #ff0000;">&quot;D:/xampplite/htdocs/hg&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
      Options ExecCGI FollowSymLinks
    #去掉SSLRequireSSL的#号就强迫使用ssl来访问
     #SSLRequireSSL
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/Directory<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;"># 版本管理
    ScriptAliasMatch ^/hg(.*) D:/xampplite/htdocs/hg/hgwebdir.cgi$1
    &lt;Directory &quot;D:/xampplite/htdocs/hg&quot;&gt;
      Options ExecCGI FollowSymLinks
    #去掉SSLRequireSSL的#号就强迫使用ssl来访问
     #SSLRequireSSL
    &lt;/Directory&gt;</p></div>
    ";}
categories:
  - 电脑知识
tags:
  - Apache
  - Mercurial
  - 搭建服务
  - 服务器
  - 版本服务

---
最近工作需要，建立一个本地版本控制服务，用来共享代码。搭建简单的SVN服务可以使用VisualSVN，但Mercurial有没有类似的工具呢？
<span style="font-weight: normal;">权限控制可以看这篇文章 </span><a rel="bookmark" href="http://fatkun.com/2010/10/mercurial-authentication.html"><span style="font-weight: normal;">Mercurial(HG)版本控制服务用户名验证</span></a> <span style="font-weight: normal;"></span>
## 使用Serve

如果你需要简单的共享代码，可以直接使用TortoiseHG的Serve，可以push，pull，clone，不过没有什么验证。安全性不高，当然在内部网络这就可以了，但是同时只能提供一个项目的使用。  
使用serve时push默认是不启用的，需要把Push require SSL设为False和Allow Push设为*
## 使用Apache搭建

如果你英文不错，可以到官方wiki这里看看~ 俺英文太菜了。。<http://mercurial.selenic.com/wiki/PublishingRepositories> ，
搜索了一下，再找到一篇文章，跟着这里做 <http://makinggames.ca/dev/version-control-mercurial-apache-tortoisehg/>（依然是英文）
### 1.准备工作

下载<a href="http://tortoisehg.bitbucket.org/" target="_blank">TortoiseHG</a>，<a href="http://mercurial.selenic.com/" target="_blank">Mercurial v1.6</a>，<a href="http://www.python.org/" target="_blank">Python v2.6</a>(建议使用此版本),<a href="http://www.apachefriends.org/en/xampp.html" target="_blank">XAMPP v1.7.3</a>(比较简单的apache服务)，把上面的软件都安装了。
### 2.注意事项

  * 最好是使用没有空格的路径！例如c:\Program Files这样的路径最好不要用，不然可能出现乱七八糟的错误。
  * 在配置文件中路径使用“/” 或者使用&#8221;\\&#8221;，例如 &#8220;D:\\xampp\\htdocs&#8221;
### 3.创建**repositories**

使用TortoiseHG在某个目录创建**repositorie，我的目录是F:\workspace\hg**
### **4.配置**

从Mercurial中找到library.zip(注意是Mercurial里的，不是TortoiseHG的library.zip，不然会出错！！)，解压到一个目录，我这里是解压到<span style="font-family: Consolas, Monaco, 'Courier New', Courier, monospace; line-height: 18px; font-size: 12px; white-space: pre;"><strong>D:\\xampplite\\mlib</strong>目录，把Mercurial中templates目录同样复制到此目录下。</span>
在xampp安装目录htdocs下，建立一个hg文件夹  
<xampp install>\htdocs\hg  
在hg目录下，建立一个**hgwebdir.cgi**文件，把下面的内容拷贝进去
<pre escaped="true" lang="python" line="1">#!C:/Python26/python.exe
#
# An example CGI script to export multiple hgweb repos, edit as necessary
# 配置为你的library.zip解压的目录:
import sys
sys.path.insert(0, "D:\\xampplite\\mlib")

from mercurial import demandimport;
demandimport.enable()

import cgitb
cgitb.enable()

#import os
#os.environ["HGENCODING"] = "UTF-8"

from mercurial.hgweb.hgwebdir_mod import hgwebdir
import mercurial.hgweb.wsgicgi as wsgicgi
application = hgwebdir('hgweb.config')
wsgicgi.launch(application)</pre>
注意第一行中的#!C:/Python26/python.exe改为你python.exe所在的路径  
sys.path.insert(0, &#8220;D:\\xampplite\\mlib&#8221;)这句中的D:\\xampplite\\mlib是上面把library.zip解压的目录  
再建立一个**hgweb.config**文件
<pre escaped="true" lang="xml" line="1">[collections]
F:/workspace/hg = F:/workspace/hg

[web]
allow_push =*
push_ssl = false
style = gitweb</pre>
上面的**F:/workspace/hg**请换为你自己的项目的存放目录
最后一步
打开ampp/apache/conf/httpd.conf文件，在最末尾加入
<pre escaped="true" lang="xml" line="1"># 版本管理
ScriptAliasMatch ^/hg(.*) D:/xampplite/htdocs/hg/hgwebdir.cgi$1
&lt;Directory "D:/xampplite/htdocs/hg"&gt;
  Options ExecCGI FollowSymLinks
#去掉SSLRequireSSL的#号就强迫使用ssl来访问
 #SSLRequireSSL
&lt;/Directory&gt;</pre>
现在试试重启你的apache服务吧，重启后，通过_<a href="https://localhost/hg/" target="_blank">https://localhost/hg/</a><span style="font-style: normal;">访问</span>_
## _<span style="font-style: normal;">错误处理</span>_

Premature end of script headers: hgwebdir.cgi
如果遇到这个问题，建议把它改为hgwebdir.py，用python运行检查一下出现什么错误，注意路径中有空格要用双引号括起来，路径用&#8221;/&#8221;来隔开。最终会有个SCRIPT的错误，没关系，把它改回hgwebdir.cgi就可以从网页上浏览了。