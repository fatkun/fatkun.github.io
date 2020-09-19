---
title: 在用户目录安装python lib
author: fatkun
type: post
date: 2017-08-16T09:46:03+00:00
url: /2017/08/在用户目录安装python-lib.html
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:706:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #c20cb9; font-weight: bold;">wget</span> https:<span style="color: #000000; font-weight: bold;">//</span>bootstrap.pypa.io<span style="color: #000000; font-weight: bold;">/</span>get-pip.py
    &nbsp;
    python get-pip.py <span style="color: #660033;">--user</span>
    &nbsp;
    pip <span style="color: #c20cb9; font-weight: bold;">install</span> <span style="color: #660033;">--user</span> xxxxxx</pre></td></tr></table><p class="theCode" style="display:none;">wget https://bootstrap.pypa.io/get-pip.py
    
    python get-pip.py --user
    
    pip install --user xxxxxx</p></div>
    ";}
categories:
  - python
tags:
  - pip
  - python

---
&nbsp;
<pre lang="bash" escaped="true">wget https://bootstrap.pypa.io/get-pip.py

python get-pip.py --user

pip install --user xxxxxx</pre>