---
title: 'Failed to initialize NVML: Unknown Error'
author: fatkun
type: post
date: 2018-11-14T13:11:20+00:00
url: /2018/11/failed-to-initialize-nvml-unknown-error.html
categories:
  - docker
tags:
  - gpu

---
在k8s启动的pod内执行nvidia-smi，报错Failed to initialize NVML: Unknown Error，但直接用docker run &#8211;rm nvidia/cuda:9.0-base nvidia-smi 却不会报错。
找到这里的文章提示 https://www.hwchiu.com/gpu-gke.html 可以用strace来查看系统调用，
能看到有这句
open(&#8220;/dev/nvidiactl&#8221;, O_RDWR) = -1 EPERM (Operation not permitted)  
open(&#8220;/dev/nvidiactl&#8221;, O_RDONLY) = -1 EPERM (Operation not permitted)
没有权限去读取/dev/nvidiactl，按上面文章提示，加上
<pre><span class="line">    securityContext:</span>
<span class="line">      privileged: true</span>

但加上<span class="line">privileged会导致/dev下所有显卡暴露，不能加特权。</span>
最终发现是/etc/systemd/system/kubelet.service  加了--feature-gates CPUManager=true  ，具体原因不明为什么有影响。

</pre>