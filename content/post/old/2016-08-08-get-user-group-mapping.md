---
title: 获取linux用户和组映射脚本
author: fatkun
type: post
date: 2016-08-08T03:02:55+00:00
url: /2016/08/get-user-group-mapping.html
duoshuo_thread_id:
  - 6316288373912765186
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:4208:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #808080; font-style: italic;">#!/usr/bin/env python</span>
    <span style="color: #808080; font-style: italic;"># -*- coding: utf-8 -*-</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">import</span> <span style="color: #dc143c;">re</span>
    <span style="color: #ff7700;font-weight:bold;">import</span> <span style="color: #dc143c;">os</span>
    <span style="color: #ff7700;font-weight:bold;">import</span> <span style="color: #dc143c;">sys</span>
    &nbsp;
    p <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">os</span>.<span style="color: black;">popen</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">'id %s'</span> % <span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    s <span style="color: #66cc66;">=</span> p.<span style="color: black;">read</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #808080; font-style: italic;"># s = 'uid=486(yarn) gid=484(yarn) groups=484(yarn),493(hadoop),513(supergroup)'</span>
    &nbsp;
    <span style="color: #dc143c;">user</span> <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">re</span>.<span style="color: black;">findall</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">&quot;uid=<span style="color: #000099; font-weight: bold;">\d</span>+<span style="color: #000099; font-weight: bold;">\(</span>(.*?)<span style="color: #000099; font-weight: bold;">\)</span>&quot;</span><span style="color: #66cc66;">,</span> s<span style="color: black;">&#41;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span>
    &nbsp;
    &nbsp;
    s <span style="color: #66cc66;">=</span> s.<span style="color: black;">split</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">&quot;groups=&quot;</span><span style="color: black;">&#41;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    match <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">re</span>.<span style="color: black;">findall</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">&quot;<span style="color: #000099; font-weight: bold;">\(</span>(.*?)<span style="color: #000099; font-weight: bold;">\)</span>&quot;</span><span style="color: #66cc66;">,</span> s<span style="color: black;">&#41;</span>
    &nbsp;
    groups <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> group <span style="color: #ff7700;font-weight:bold;">in</span> match:
        groups.<span style="color: black;">append</span><span style="color: black;">&#40;</span>group<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #dc143c;">user</span> + <span style="color: #483d8b;">&quot;=&quot;</span> +  <span style="color: #483d8b;">&quot;,&quot;</span>.<span style="color: black;">join</span><span style="color: black;">&#40;</span><span style="color: #008000;">sorted</span><span style="color: black;">&#40;</span>groups<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">#!/usr/bin/env python
    # -*- coding: utf-8 -*-
    
    import re
    import os
    import sys
    
    p = os.popen('id %s' % sys.argv[1])
    s = p.read()
    
    # s = 'uid=486(yarn) gid=484(yarn) groups=484(yarn),493(hadoop),513(supergroup)'
    
    user = re.findall(&quot;uid=\d+\((.*?)\)&quot;, s)[0]
    
    
    s = s.split(&quot;groups=&quot;)[1]
    match = re.findall(&quot;\((.*?)\)&quot;, s)
    
    groups = []
    for group in match:
        groups.append(group)
    
    print user + &quot;=&quot; +  &quot;,&quot;.join(sorted(groups))</p></div>
    ";i:2;s:1272:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">for</span> user <span style="color: #000000; font-weight: bold;">in</span> $<span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #c20cb9; font-weight: bold;">cat</span> <span style="color: #000000; font-weight: bold;">/</span>etc<span style="color: #000000; font-weight: bold;">/</span><span style="color: #c20cb9; font-weight: bold;">passwd</span><span style="color: #000000; font-weight: bold;">|</span><span style="color: #c20cb9; font-weight: bold;">gawk</span> <span style="color: #660033;">-F</span><span style="color: #ff0000;">':'</span> <span style="color: #ff0000;">'{print $1}'</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>; <span style="color: #000000; font-weight: bold;">do</span>
            python .<span style="color: #000000; font-weight: bold;">/</span>f.py <span style="color: #007800;">$user</span>
    <span style="color: #000000; font-weight: bold;">done</span></pre></td></tr></table><p class="theCode" style="display:none;">for user in $(cat /etc/passwd|gawk -F':' '{print $1}'); do
            python ./f.py $user
    done</p></div>
    ";}
categories:
  - hadoop
  - Linux

---
记录一下
python代码
<pre escaped="true" lang="python">#!/usr/bin/env python
# -*- coding: utf-8 -*-

import re
import os
import sys

p = os.popen('id %s' % sys.argv[1])
s = p.read()

# s = 'uid=486(yarn) gid=484(yarn) groups=484(yarn),493(hadoop),513(supergroup)'

user = re.findall("uid=\d+\((.*?)\)", s)[0]


s = s.split("groups=")[1]
match = re.findall("\((.*?)\)", s)

groups = []
for group in match:
    groups.append(group)

print user + "=" +  ",".join(sorted(groups))</pre>
shell脚本
<pre escaped="true" lang="bash">for user in $(cat /etc/passwd|gawk -F':' '{print $1}'); do
        python ./f.py $user
done</pre>