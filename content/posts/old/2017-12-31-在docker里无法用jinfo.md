---
title: 在docker里无法用jinfo
author: fatkun
type: post
date: 2017-12-31T13:23:10+00:00
url: /2017/12/在docker里无法用jinfo.html
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:545:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">docker run <span style="color: #660033;">--cap-add</span>=SYS_PTRACE alpine <span style="color: #c20cb9; font-weight: bold;">sh</span> <span style="color: #660033;">-c</span> <span style="color: #ff0000;">'apk add -U strace &amp;&amp; strace echo'</span></pre></td></tr></table><p class="theCode" style="display:none;">docker run --cap-add=SYS_PTRACE alpine sh -c 'apk add -U strace &amp;&amp; strace echo'</p></div>
    ";i:2;s:253:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">cap_add:
      - SYS_PTRACE</pre></td></tr></table><p class="theCode" style="display:none;">cap_add:
      - SYS_PTRACE</p></div>
    ";}
categories:
  - 未分类
tags:
  - docker

---
在命令里加参数
<pre lang="bash" escaped="true">docker run --cap-add=SYS_PTRACE alpine sh -c 'apk add -U strace && strace echo'</pre>
或者在compose里某个service里面加
<pre lang="bash" escaped="true">cap_add:
  - SYS_PTRACE</pre>
&nbsp;
[JVM in Docker and&nbsp;PTRACE_ATTACH][1]

 [1]: https://jarekprzygodzki.wordpress.com/2016/12/19/jvm-in-docker-and-ptrace_attach/