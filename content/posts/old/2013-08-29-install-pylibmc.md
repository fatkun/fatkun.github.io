---
title: 安装pylibmc
author: fatkun
type: post
date: 2013-08-29T10:51:00+00:00
url: /2013/08/install-pylibmc.html
duoshuo_thread_id:
  - 6300410041035916033
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:1661:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">&gt;&gt;&gt;</span> import pylibmc
    Traceback <span style="color: #7a0874; font-weight: bold;">&#40;</span>most recent call <span style="color: #c20cb9; font-weight: bold;">last</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>:
    File <span style="color: #ff0000;">&quot;&lt;stdin&gt;&quot;</span>, line <span style="color: #000000;">1</span>, <span style="color: #000000; font-weight: bold;">in</span> <span style="color: #000000; font-weight: bold;">&lt;</span>module<span style="color: #000000; font-weight: bold;">&gt;</span>
    File <span style="color: #ff0000;">&quot;/usr/local/python2.6/lib/python2.6/site-packages/pylibmc/__init__.py&quot;</span>, line <span style="color: #000000;">70</span>, <span style="color: #000000; font-weight: bold;">in</span> <span style="color: #000000; font-weight: bold;">&lt;</span>module<span style="color: #000000; font-weight: bold;">&gt;</span>
    import _pylibmc
    ImportError: libmemcached.so.8: cannot open shared object file: No such <span style="color: #c20cb9; font-weight: bold;">file</span> or directory</pre></td></tr></table><p class="theCode" style="display:none;">&gt;&gt;&gt; import pylibmc
    Traceback (most recent call last):
    File &quot;&lt;stdin&gt;&quot;, line 1, in &lt;module&gt;
    File &quot;/usr/local/python2.6/lib/python2.6/site-packages/pylibmc/__init__.py&quot;, line 70, in &lt;module&gt;
    import _pylibmc
    ImportError: libmemcached.so.8: cannot open shared object file: No such file or directory</p></div>
    ";}
categories:
  - python
tags:
  - pylibmc

---
首先需要安装libmemcached ，不要安装太新的版本，对gcc有要求
<a href="http://launchpad.net/libmemcached/1.0/0.51/+download/libmemcached-0.51.tar.gz" rel="nofollow">http://launchpad.net/libmemcached/1.0/0.51/+download/libmemcached-0.51.tar.gz</a>
然后就可以安装了，
./configuare
make && sudo make install
之后用pip安装pylibmc， <https://pypi.python.org/pypi/pylibmc>
pip install pylibmc
&nbsp;
&nbsp;
装完后报错
<pre lang="bash" escaped="true">&gt;&gt;&gt; import pylibmc
Traceback (most recent call last):
File "&lt;stdin&gt;", line 1, in &lt;module&gt;
File "/usr/local/python2.6/lib/python2.6/site-packages/pylibmc/__init__.py", line 70, in &lt;module&gt;
import _pylibmc
ImportError: libmemcached.so.8: cannot open shared object file: No such file or directory</pre>
&nbsp;
把/usr/local/lib加入/etc/ld.so.conf,然后执行/sbin/ldconfig
&nbsp;