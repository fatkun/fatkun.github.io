---
title: minikube生成内置证书的kubeconfig
author: fatkun
type: post
date: 2019-08-12T06:20:20+00:00
url: /2019/08/minikube-embed-certs.html
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:1325:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">kubectl config set-credentials minikube <span style="color: #660033;">--embed-certs</span> <span style="color: #660033;">--client-certificate</span>=<span style="color: #800000;">${HOME}</span><span style="color: #000000; font-weight: bold;">/</span>.minikube<span style="color: #000000; font-weight: bold;">/</span>client.crt <span style="color: #660033;">--client-key</span>=<span style="color: #800000;">${HOME}</span><span style="color: #000000; font-weight: bold;">/</span>.minikube<span style="color: #000000; font-weight: bold;">/</span>client.key
    kubectl config set-cluster minikube <span style="color: #660033;">--embed-certs</span> <span style="color: #660033;">--certificate-authority</span>=<span style="color: #800000;">${HOME}</span><span style="color: #000000; font-weight: bold;">/</span>.minikube<span style="color: #000000; font-weight: bold;">/</span>ca.crt</pre></td></tr></table><p class="theCode" style="display:none;">kubectl config set-credentials minikube --embed-certs --client-certificate=${HOME}/.minikube/client.crt --client-key=${HOME}/.minikube/client.key
    kubectl config set-cluster minikube --embed-certs --certificate-authority=${HOME}/.minikube/ca.crt</p></div>
    ";}
categories:
  - docker
tags:
  - k8s
  - minikube

---
minikube默认生成的证书都是文件路径，如果要在其他地方使用不方便，需要把证书内置。
如果还没启动minikube，可以看下 <a href="https://github.com/kubernetes/minikube/issues/3064" rel="noopener" target="_blank">https://github.com/kubernetes/minikube/issues/3064</a>
如果已经生成了，执行以下命令可以把证书内置。
<pre escaped="true" lang="bash">kubectl config set-credentials minikube --embed-certs --client-certificate=${HOME}/.minikube/client.crt --client-key=${HOME}/.minikube/client.key
kubectl config set-cluster minikube --embed-certs --certificate-authority=${HOME}/.minikube/ca.crt</pre>