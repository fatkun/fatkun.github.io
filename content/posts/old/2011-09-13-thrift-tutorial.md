---
title: Thrift入门篇-运行Tutorial
author: fatkun
type: post
date: 2011-09-12T16:06:53+00:00
url: /2011/09/thrift-tutorial.html
duoshuo_thread_id:
  - 6300408819830752001
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:378:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">thrift-0.7.0.exe –r –gen py –gen <span style="color: #c20cb9; font-weight: bold;">java</span> tutorial.thrift</pre></td></tr></table><p class="theCode" style="display:none;">thrift-0.7.0.exe –r –gen py –gen java tutorial.thrift</p></div>
    ";i:2;s:280:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="py" style="font-family:monospace;">transport = TSocket.TServerSocket(9090)</pre></td></tr></table><p class="theCode" style="display:none;">transport = TSocket.TServerSocket(9090)</p></div>
    ";i:3;s:290:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="py" style="font-family:monospace;">transport = TSocket.TServerSocket(port=9090)</pre></td></tr></table><p class="theCode" style="display:none;">transport = TSocket.TServerSocket(port=9090)</p></div>
    ";}
categories:
  - python
tags:
  - thrift

---
本文假设你已经了解Thrift是什么了，如果还不了解，请借助强大的谷歌。
本文的开发环境是windows 7 + python2.6
Thrift官方主页：<http://thrift.apache.org/>
&nbsp;
先来这里下载thrift-0.7.0.tar.gz 和Thrift compiler for Windows (thrift-0.7.0.exe) 。thrift-0.7.0.exe是帮你编译好的，可以在windows下运行。
解压thrift-0.7.0.tar.gz
&nbsp;
学一样东西之前，当然是看Tutorial啦，不过文档还不完善啊。下面将以Python来举例子。
### 1.安装thrift库

先要安装thrift-0.7.0\lib\py里的库，setup.py install 注意，在windows下安装不成功，需要用VC编译，还要对代码做相应修改，很麻烦，就不说了，直接在这里下载已经编译好的版本。<http://www.lfd.uci.edu/~gohlke/pythonlibs/> （这里真的是个好地方，感谢大神）
### 2.Thrift生成代码

Thrift能够帮你生成一部分代码，让你更关注你的业务部分，而不必关注它是怎么通信的。
在thrift-0.7.0\tutorial，就是一个官方教程了。可以先看看tutorial.thrift，这是thrift定义的语法，就是通过它来生成各种代码的了。
&nbsp;
生成代码开始啦，使用之前下载的thrift-0.7.0.exe，在thrift-0.7.0\tutorial目录下执行命令
<pre escaped="true" lang="bash">thrift-0.7.0.exe –r –gen py –gen java tutorial.thrift</pre>
搞定，在当前文件夹就产生两个文件夹了，分别是gen-java和gen-py。gen-java咱暂时用不着，生成来玩的：）如果你想生成更多其他类型的代码，&#8211;gen xxx就可以了。
### 3.运行

进入thrift-0.7.0\tutorial\py目录，在运行之前，先改一下PythonServer.py
不知道是我安装的thrift库有问题还是它的tutorial写错了，找到下面这行代码。
<pre escaped="true" lang="py">transport = TSocket.TServerSocket(9090)</pre>
把它改为
<pre escaped="true" lang="py">transport = TSocket.TServerSocket(port=9090)</pre>
好吧，双击运行服务端PythonServer.py。看到Starting the server就证明你成功运行服务端了！如果黑乎乎的窗口一闪而过，那看看哪一步做错了吧。用cmd运行看看。
&nbsp;
接下来，再运行客户端PythonClient.py，这时就可以看到服务端有信息输出了~~成功！
&nbsp;