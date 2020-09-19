---
title: 【记录】为Kubernetes集群添加用户
author: fatkun
type: post
date: 2019-02-17T09:47:39+00:00
url: /2019/02/kubernetes-add-user.html
wp-syntax-cache-content:
  - |
    a:4:{i:1;s:2980:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #c20cb9; font-weight: bold;">mkdir</span> <span style="color: #000000; font-weight: bold;">/</span>var<span style="color: #000000; font-weight: bold;">/</span>lib<span style="color: #000000; font-weight: bold;">/</span>minikube<span style="color: #000000; font-weight: bold;">/</span>certs<span style="color: #000000; font-weight: bold;">/</span>tmp<span style="color: #000000; font-weight: bold;">/</span>
    <span style="color: #7a0874; font-weight: bold;">cd</span> <span style="color: #000000; font-weight: bold;">/</span>var<span style="color: #000000; font-weight: bold;">/</span>lib<span style="color: #000000; font-weight: bold;">/</span>minikube<span style="color: #000000; font-weight: bold;">/</span>certs<span style="color: #000000; font-weight: bold;">/</span>tmp<span style="color: #000000; font-weight: bold;">/</span>
    &nbsp;
    <span style="color: #666666; font-style: italic;"># 首先需要为此用户创建一个私钥</span>
    openssl genrsa <span style="color: #660033;">-out</span> knative.key <span style="color: #000000;">2048</span>
    <span style="color: #666666; font-style: italic;"># 接着用此私钥创建一个csr(证书签名请求)文件，其中我们需要在subject里带上用户信息(CN为用户名，O为用户组)</span>
    openssl req <span style="color: #660033;">-new</span> <span style="color: #660033;">-key</span> knative.key <span style="color: #660033;">-out</span> knative.csr <span style="color: #660033;">-subj</span> <span style="color: #ff0000;">&quot;/CN=knative/O=MGM&quot;</span>
    <span style="color: #666666; font-style: italic;"># 通过集群的CA证书和之前创建的csr文件，来为用户颁发证书</span>
    openssl x509 <span style="color: #660033;">-req</span> <span style="color: #660033;">-in</span> knative.csr <span style="color: #660033;">-CA</span> ..<span style="color: #000000; font-weight: bold;">/</span>ca.crt <span style="color: #660033;">-CAkey</span> ..<span style="color: #000000; font-weight: bold;">/</span>ca.key <span style="color: #660033;">-CAcreateserial</span> <span style="color: #660033;">-out</span> knative.crt <span style="color: #660033;">-days</span> <span style="color: #000000;">365</span></pre></td></tr></table><p class="theCode" style="display:none;">mkdir /var/lib/minikube/certs/tmp/
    cd /var/lib/minikube/certs/tmp/
    
    # 首先需要为此用户创建一个私钥
    openssl genrsa -out knative.key 2048
    # 接着用此私钥创建一个csr(证书签名请求)文件，其中我们需要在subject里带上用户信息(CN为用户名，O为用户组)
    openssl req -new -key knative.key -out knative.csr -subj &quot;/CN=knative/O=MGM&quot;
    # 通过集群的CA证书和之前创建的csr文件，来为用户颁发证书
    openssl x509 -req -in knative.csr -CA ../ca.crt -CAkey ../ca.key -CAcreateserial -out knative.crt -days 365</p></div>
    ";i:2;s:3370:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #666666; font-style: italic;"># KUBE_APISERVER 可以进一个容器里面看环境变量</span>
    <span style="color: #666666; font-style: italic;"># 如果是用虚拟机启动，执行minikube ip 拿到minikube的ip，加上端口8443。'https://192.168.39.23:8443'，这个地址也可以从.kube/config里的server配置得到</span>
    &nbsp;
    <span style="color: #666666; font-style: italic;"># 设置集群参数</span>
    <span style="color: #7a0874; font-weight: bold;">export</span> <span style="color: #007800;">KUBE_APISERVER</span>=<span style="color: #ff0000;">&quot;https://10.96.0.1:443&quot;</span>
    kubectl config set-cluster kubernetes \
    <span style="color: #660033;">--certificate-authority</span>=..<span style="color: #000000; font-weight: bold;">/</span>ca.crt \
    <span style="color: #660033;">--embed-certs</span>=<span style="color: #c20cb9; font-weight: bold;">true</span> \
    <span style="color: #660033;">--server</span>=<span style="color: #800000;">${KUBE_APISERVER}</span> \
    <span style="color: #660033;">--kubeconfig</span>=knative.kubeconfig
    &nbsp;
    <span style="color: #666666; font-style: italic;"># 设置客户端认证参数</span>
    kubectl config set-credentials knative \
    <span style="color: #660033;">--client-certificate</span>=.<span style="color: #000000; font-weight: bold;">/</span>knative.crt \
    <span style="color: #660033;">--client-key</span>=.<span style="color: #000000; font-weight: bold;">/</span>knative.key \
    <span style="color: #660033;">--embed-certs</span>=<span style="color: #c20cb9; font-weight: bold;">true</span> \
    <span style="color: #660033;">--kubeconfig</span>=knative.kubeconfig
    &nbsp;
    <span style="color: #666666; font-style: italic;"># 设置上下文参数</span>
    kubectl config set-context kubernetes \
    <span style="color: #660033;">--cluster</span>=kubernetes \
    <span style="color: #660033;">--user</span>=knative \
    <span style="color: #660033;">--namespace</span>=default \
    <span style="color: #660033;">--kubeconfig</span>=knative.kubeconfig
    &nbsp;
    <span style="color: #666666; font-style: italic;"># 设置默认上下文</span>
    kubectl config use-context kubernetes <span style="color: #660033;">--kubeconfig</span>=knative.kubeconfig</pre></td></tr></table><p class="theCode" style="display:none;"># KUBE_APISERVER 可以进一个容器里面看环境变量
    # 如果是用虚拟机启动，执行minikube ip 拿到minikube的ip，加上端口8443。'https://192.168.39.23:8443'，这个地址也可以从.kube/config里的server配置得到
    
    # 设置集群参数
    export KUBE_APISERVER=&quot;https://10.96.0.1:443&quot;
    kubectl config set-cluster kubernetes \
    --certificate-authority=../ca.crt \
    --embed-certs=true \
    --server=${KUBE_APISERVER} \
    --kubeconfig=knative.kubeconfig
    
    # 设置客户端认证参数
    kubectl config set-credentials knative \
    --client-certificate=./knative.crt \
    --client-key=./knative.key \
    --embed-certs=true \
    --kubeconfig=knative.kubeconfig
    
    # 设置上下文参数
    kubectl config set-context kubernetes \
    --cluster=kubernetes \
    --user=knative \
    --namespace=default \
    --kubeconfig=knative.kubeconfig
    
    # 设置默认上下文
    kubectl config use-context kubernetes --kubeconfig=knative.kubeconfig</p></div>
    ";i:3;s:537:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">kubectl create rolebinding knative-admin-binding <span style="color: #660033;">--clusterrole</span>=admin <span style="color: #660033;">--user</span>=knative <span style="color: #660033;">--namespace</span>=knative-serving</pre></td></tr></table><p class="theCode" style="display:none;">kubectl create rolebinding knative-admin-binding --clusterrole=admin --user=knative --namespace=knative-serving</p></div>
    ";i:4;s:410:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">kubectl  <span style="color: #660033;">--kubeconfig</span>=knative.kubeconfig <span style="color: #660033;">-n</span> knative-serving get po</pre></td></tr></table><p class="theCode" style="display:none;">kubectl  --kubeconfig=knative.kubeconfig -n knative-serving get po</p></div>
    ";}
categories:
  - docker
tags:
  - k8s

---
具体按照这篇文章配置 <https://zhuanlan.zhihu.com/p/43237959>  ，本文用于记录命令
minikube的证书在/var/lib/minikube/certs 目录下，或者/var/lib/localkube/certs，可以通过查询进程kube-controller-manager，查看它的参数cluster-signing-cert-file是什么。  
在.minikube目录里面的ca.crt和ca.key也是一样的。
<pre lang="bash" escaped="true">mkdir /var/lib/minikube/certs/tmp/
cd /var/lib/minikube/certs/tmp/

# 首先需要为此用户创建一个私钥
openssl genrsa -out knative.key 2048
# 接着用此私钥创建一个csr(证书签名请求)文件，其中我们需要在subject里带上用户信息(CN为用户名，O为用户组)
openssl req -new -key knative.key -out knative.csr -subj "/CN=knative/O=MGM"
# 通过集群的CA证书和之前创建的csr文件，来为用户颁发证书
openssl x509 -req -in knative.csr -CA ../ca.crt -CAkey ../ca.key -CAcreateserial -out knative.crt -days 365
</pre>
生成kubeconfig，具体见 [jimmysong 的文章][1]。
<pre lang="bash" escaped="true"># KUBE_APISERVER 可以进一个容器里面看环境变量
# 如果是用虚拟机启动，执行minikube ip 拿到minikube的ip，加上端口8443。'https://192.168.39.23:8443'，这个地址也可以从.kube/config里的server配置得到

# 设置集群参数
export KUBE_APISERVER="https://10.96.0.1:443"
kubectl config set-cluster kubernetes \
--certificate-authority=../ca.crt \
--embed-certs=true \
--server=${KUBE_APISERVER} \
--kubeconfig=knative.kubeconfig

# 设置客户端认证参数
kubectl config set-credentials knative \
--client-certificate=./knative.crt \
--client-key=./knative.key \
--embed-certs=true \
--kubeconfig=knative.kubeconfig

# 设置上下文参数
kubectl config set-context kubernetes \
--cluster=kubernetes \
--user=knative \
--namespace=default \
--kubeconfig=knative.kubeconfig

# 设置默认上下文
kubectl config use-context kubernetes --kubeconfig=knative.kubeconfig
</pre>
绑定namespace管理员权限
<pre lang="bash" escaped="true">kubectl create rolebinding knative-admin-binding --clusterrole=admin --user=knative --namespace=knative-serving</pre>
使用账号访问
<pre lang="bash" escaped="true">kubectl  --kubeconfig=knative.kubeconfig -n knative-serving get po</pre>
## 参考

<https://jimmysong.io/kubernetes-handbook/guide/kubectl-user-authentication-authorization.html>

 [1]: https://jimmysong.io/kubernetes-handbook/guide/kubectl-user-authentication-authorization.html