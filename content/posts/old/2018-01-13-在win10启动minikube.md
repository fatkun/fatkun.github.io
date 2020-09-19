---
title: 在win10启动minikube
author: fatkun
type: post
date: 2018-01-13T13:18:34+00:00
url: /2018/01/在win10启动minikube.html
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:951:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">minikube.exe start <span style="color: #660033;">--kubernetes-version</span>=<span style="color: #ff0000;">&quot;v1.8.0&quot;</span> <span style="color: #660033;">--vm-driver</span>=<span style="color: #ff0000;">&quot;hyperv&quot;</span> <span style="color: #660033;">--memory</span>=<span style="color: #000000;">1024</span> <span style="color: #660033;">--hyperv-virtual-switch</span>=<span style="color: #ff0000;">&quot;myvnet&quot;</span> <span style="color: #660033;">--v</span>=<span style="color: #000000;">7</span> <span style="color: #660033;">--alsologtostderr</span></pre></td></tr></table><p class="theCode" style="display:none;">minikube.exe start --kubernetes-version=&quot;v1.8.0&quot; --vm-driver=&quot;hyperv&quot; --memory=1024 --hyperv-virtual-switch=&quot;myvnet&quot; --v=7 --alsologtostderr</p></div>
    ";}
categories:
  - 未分类
tags:
  - docker

---
<blockquote class="wp-embedded-content" data-secret="1bUZi1A9eJ">  <p>    <a href="https://blogs.msdn.microsoft.com/wasimbloch/2017/01/23/setting-up-kubernetes-on-windows10-laptop-with-minikube/">Setting up Kubernetes on Windows10 Laptop with Minikube</a>  </p></blockquote>

如果建虚拟交换机提示权限失败，使用管理员权限开启hyper-v。如果提示一般性拒绝，试一下把其他的虚拟网卡都卸载掉。
一定要指定虚拟网卡
<pre lang="bash" escaped="true">minikube.exe start --kubernetes-version="v1.8.0" --vm-driver="hyperv" --memory=1024 --hyperv-virtual-switch="myvnet" --v=7 --alsologtostderr</pre>