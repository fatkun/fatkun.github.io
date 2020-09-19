---
title: k8s 拉取私有仓库失败
author: fatkun
type: post
date: 2018-09-27T08:59:02+00:00
url: /2018/09/k8s-errimagepull.html
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:834:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="html" style="font-family:monospace;">{--root-dir:-/var/lib/kubelet}/config.json
    {cwd of kubelet}/config.json
    ${HOME}/.docker/config.json
    /.docker/config.json
    {--root-dir:-/var/lib/kubelet}/.dockercfg
    {cwd of kubelet}/.dockercfg
    ${HOME}/.dockercfg
    /.dockercfg
    Note: You may have to set HOME=/root explicitly in your environment file for kubelet.</pre></td></tr></table><p class="theCode" style="display:none;">{--root-dir:-/var/lib/kubelet}/config.json
    {cwd of kubelet}/config.json
    ${HOME}/.docker/config.json
    /.docker/config.json
    {--root-dir:-/var/lib/kubelet}/.dockercfg
    {cwd of kubelet}/.dockercfg
    ${HOME}/.dockercfg
    /.dockercfg
    Note: You may have to set HOME=/root explicitly in your environment file for kubelet.</p></div>
    ";}
categories:
  - docker
tags:
  - k8s

---
k8s 报错拉取镜像失败 Error response from daemon: pull access denied for istio/citadel, repository does not exist or may require &#8216;docker login&#8217;
&nbsp;
docker login后，把配置拷贝到以下目录的其中一个。如果是${HOME}/.docker/config.json看说明是要额外设环境变量给kubelet的，可以试试放在/var/lib/kubelet/config.json
&nbsp;
Docker stores keys for private registries in the $HOME/.dockercfg or $HOME/.docker/config.json file. If you put the same file in the search paths list below, kubelet uses it as the credential provider when pulling images.
<pre lang="html" escaped="true">{--root-dir:-/var/lib/kubelet}/config.json
{cwd of kubelet}/config.json
${HOME}/.docker/config.json
/.docker/config.json
{--root-dir:-/var/lib/kubelet}/.dockercfg
{cwd of kubelet}/.dockercfg
${HOME}/.dockercfg
/.dockercfg
Note: You may have to set HOME=/root explicitly in your environment file for kubelet.</pre>
https://kubernetes.io/docs/concepts/containers/images/