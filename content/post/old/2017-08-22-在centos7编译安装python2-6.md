---
title: 在centos7编译安装python2.6
author: fatkun
type: post
date: 2017-08-22T06:40:07+00:00
url: /2017/08/在centos7编译安装python2-6.html
categories:
  - 未分类
tags:
  - 运维

---
遇到一些库安装不上，可以忽略掉，具体见网址 http://blog.useasp.net/archive/2014/05/07/compile-and-install-python-2-dot-7-dot-6-on-centos.aspx
&nbsp;
<div class="line number1 index0 alt2">  <code class="bash plain">Python build finished, but the necessary bits to build these modules were not found:</code></div>
<div class="line number2 index1 alt1">  <code class="bash spaces">   </code><code class="bash plain">_bsddb             _sqlite3           _ssl</code></div>
<div class="line number3 index2 alt2">  <code class="bash spaces">   </code><code class="bash plain">_tkinter           bsddb185           bz2</code></div>
<div class="line number4 index3 alt1">  <code class="bash spaces">   </code><code class="bash plain">dbm                gdbm               readline</code></div>
<div class="line number5 index4 alt2">  <code class="bash spaces">   </code><code class="bash plain">sunaudiodev</code></div>
<div class="line number6 index5 alt1">  <code class="bash plain">To </code><code class="bash functions">find</code> <code class="bash plain">the necessary bits, </code><code class="bash functions">look</code> <code class="bash keyword">in</code> <code class="bash plain">setup.py </code><code class="bash keyword">in</code> <code class="bash plain">detect_modules() </code><code class="bash keyword">for</code> <code class="bash plain">the module's name.</code></div>
&nbsp;
<table class="table table-bordered">  <tr>    <td>      模块    </td>
    <td>      依赖    </td>
    <td>      说明    </td>  </tr>
  <tr>    <td>      _bsddb    </td>
    <td>      bsddb    </td>
    <td>      Interface to Berkeley DB library。Berkeley数据库的接口    </td>  </tr>
  <tr>    <td>      _curses    </td>
    <td>      ncurses    </td>
    <td>      Terminal handling for character-cell displays。    </td>  </tr>
  <tr>    <td>      _curses_panel    </td>
    <td>      ncurses    </td>
    <td>      A panel stack extension for curses。    </td>  </tr>
  <tr>    <td>      _sqlite3    </td>
    <td>      sqlite    </td>
    <td>      DB-API 2.0 interface for SQLite databases。SqlLite，CentOS可以安装sqlite-devel    </td>  </tr>
  <tr>    <td>      _ssl    </td>
    <td>      openssl-devel.i686    </td>
    <td>      TLS/SSL wrapper for socket objects。    </td>  </tr>
  <tr>    <td>      _tkinter    </td>
    <td>      N/A    </td>
    <td>      a thin object-oriented layer on top of Tcl/Tk。如果不使用桌面程序可以忽略TKinter    </td>  </tr>
  <tr>    <td>      bsddb185    </td>
    <td>      old bsddb module    </td>
    <td>      老的bsddb模块，可忽略。    </td>  </tr>
  <tr>    <td>      bz2    </td>
    <td>      bzip2-devel.i686    </td>
    <td>      Compression compatible with bzip2。bzip2-devel    </td>  </tr>
  <tr>    <td>      dbm    </td>
    <td>      bsddb    </td>
    <td>      Simple “database” interface。    </td>  </tr>
  <tr>    <td>      dl    </td>
    <td>      N/A    </td>
    <td>      Call C functions in shared objects.Python2.6开始，已经弃用。    </td>  </tr>
  <tr>    <td>      gdbm    </td>
    <td>      gdbm-devel.i686    </td>
    <td>      GNU’s reinterpretation of dbm    </td>  </tr>
  <tr>    <td>      imageop    </td>
    <td>      N/A    </td>
    <td>      Manipulate raw image data。已经弃用。    </td>  </tr>
  <tr>    <td>      readline    </td>
    <td>      readline-devel    </td>
    <td>      GNU readline interface    </td>  </tr>
  <tr>    <td>      sunaudiodev    </td>
    <td>      N/A    </td>
    <td>      Access to Sun audio hardware。这个是针对Sun平台的，CentOS下可以忽略    </td>  </tr>
  <tr>    <td>      zlib    </td>
    <td>      Zlib    </td>
    <td>      Compression compatible with gzip    </td>  </tr></table>