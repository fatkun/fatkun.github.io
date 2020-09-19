---
title: docker常用命令
author: fatkun
type: post
date: 2017-12-24T07:50:54+00:00
url: /2017/12/docker-command.html
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:1114:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #666666; font-style: italic;"># 指定子网</span>
    docker network create <span style="color: #660033;">--subnet</span>=172.18.0.0<span style="color: #000000; font-weight: bold;">/</span><span style="color: #000000;">16</span> hadoop
    &nbsp;
    <span style="color: #666666; font-style: italic;"># attach进container里面，i参数表示交互，t参数表示tty</span>
    docker <span style="color: #7a0874; font-weight: bold;">exec</span> <span style="color: #660033;">-i</span> <span style="color: #660033;">-t</span> <span style="color: #000000; font-weight: bold;">&lt;</span>CONTAINER_ID<span style="color: #000000; font-weight: bold;">&gt;</span> <span style="color: #c20cb9; font-weight: bold;">bash</span></pre></td></tr></table><p class="theCode" style="display:none;"># 指定子网
    docker network create --subnet=172.18.0.0/16 hadoop
    
    # attach进container里面，i参数表示交互，t参数表示tty
    docker exec -i -t &lt;CONTAINER_ID&gt; bash</p></div>
    ";}
categories:
  - 未分类
tags:
  - docker

---
<pre escaped="true" lang="bash"># 指定子网
docker network create --subnet=172.18.0.0/16 hadoop

# attach进container里面，i参数表示交互，t参数表示tty
docker exec -i -t &lt;CONTAINER_ID&gt; bash</pre>