---
title: 在容器外访问k8s apiserver
author: fatkun
type: post
date: 2018-07-20T01:59:16+00:00
url: /2018/07/在容器外访问k8s-apiserver.html
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:4457:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">$ <span style="color: #007800;">APISERVER</span>=$<span style="color: #7a0874; font-weight: bold;">&#40;</span>kubectl config view <span style="color: #660033;">--minify</span> <span style="color: #000000; font-weight: bold;">|</span> <span style="color: #c20cb9; font-weight: bold;">grep</span> server <span style="color: #000000; font-weight: bold;">|</span> <span style="color: #c20cb9; font-weight: bold;">cut</span> <span style="color: #660033;">-f</span> <span style="color: #000000;">2</span>- <span style="color: #660033;">-d</span> <span style="color: #ff0000;">&quot;:&quot;</span> <span style="color: #000000; font-weight: bold;">|</span> <span style="color: #c20cb9; font-weight: bold;">tr</span> <span style="color: #660033;">-d</span> <span style="color: #ff0000;">&quot; &quot;</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
    $ <span style="color: #007800;">TOKEN</span>=$<span style="color: #7a0874; font-weight: bold;">&#40;</span>kubectl describe secret $<span style="color: #7a0874; font-weight: bold;">&#40;</span>kubectl get secrets <span style="color: #000000; font-weight: bold;">|</span> <span style="color: #c20cb9; font-weight: bold;">grep</span> ^default <span style="color: #000000; font-weight: bold;">|</span> <span style="color: #c20cb9; font-weight: bold;">cut</span> <span style="color: #660033;">-f1</span> <span style="color: #660033;">-d</span> <span style="color: #ff0000;">' '</span><span style="color: #7a0874; font-weight: bold;">&#41;</span> <span style="color: #000000; font-weight: bold;">|</span> <span style="color: #c20cb9; font-weight: bold;">grep</span> <span style="color: #660033;">-E</span> <span style="color: #ff0000;">'^token'</span> <span style="color: #000000; font-weight: bold;">|</span> <span style="color: #c20cb9; font-weight: bold;">cut</span> <span style="color: #660033;">-f2</span> <span style="color: #660033;">-d</span><span style="color: #ff0000;">':'</span> <span style="color: #000000; font-weight: bold;">|</span> <span style="color: #c20cb9; font-weight: bold;">tr</span> <span style="color: #660033;">-d</span> <span style="color: #ff0000;">&quot; &quot;</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
    $ curl <span style="color: #007800;">$APISERVER</span><span style="color: #000000; font-weight: bold;">/</span>api <span style="color: #660033;">--header</span> <span style="color: #ff0000;">&quot;Authorization: Bearer <span style="color: #007800;">$TOKEN</span>&quot;</span> <span style="color: #660033;">--insecure</span>
    <span style="color: #7a0874; font-weight: bold;">&#123;</span>
      <span style="color: #ff0000;">&quot;kind&quot;</span>: <span style="color: #ff0000;">&quot;APIVersions&quot;</span>,
      <span style="color: #ff0000;">&quot;versions&quot;</span>: <span style="color: #7a0874; font-weight: bold;">&#91;</span>
        <span style="color: #ff0000;">&quot;v1&quot;</span>
      <span style="color: #7a0874; font-weight: bold;">&#93;</span>,
      <span style="color: #ff0000;">&quot;serverAddressByClientCIDRs&quot;</span>: <span style="color: #7a0874; font-weight: bold;">&#91;</span>
        <span style="color: #7a0874; font-weight: bold;">&#123;</span>
          <span style="color: #ff0000;">&quot;clientCIDR&quot;</span>: <span style="color: #ff0000;">&quot;0.0.0.0/0&quot;</span>,
          <span style="color: #ff0000;">&quot;serverAddress&quot;</span>: <span style="color: #ff0000;">&quot;10.0.1.149:443&quot;</span>
        <span style="color: #7a0874; font-weight: bold;">&#125;</span>
      <span style="color: #7a0874; font-weight: bold;">&#93;</span>
    <span style="color: #7a0874; font-weight: bold;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">$ APISERVER=$(kubectl config view --minify | grep server | cut -f 2- -d &quot;:&quot; | tr -d &quot; &quot;)
    $ TOKEN=$(kubectl describe secret $(kubectl get secrets | grep ^default | cut -f1 -d ' ') | grep -E '^token' | cut -f2 -d':' | tr -d &quot; &quot;)
    $ curl $APISERVER/api --header &quot;Authorization: Bearer $TOKEN&quot; --insecure
    {
      &quot;kind&quot;: &quot;APIVersions&quot;,
      &quot;versions&quot;: [
        &quot;v1&quot;
      ],
      &quot;serverAddressByClientCIDRs&quot;: [
        {
          &quot;clientCIDR&quot;: &quot;0.0.0.0/0&quot;,
          &quot;serverAddress&quot;: &quot;10.0.1.149:443&quot;
        }
      ]
    }</p></div>
    ";}
categories:
  - docker
tags:
  - k8s

---
使用 <code class="language-shell" data-lang="shell">kubectl proxy --port=8080 &</code>
或者使用token
<pre lang="bash" escaped="true">$ APISERVER=$(kubectl config view --minify | grep server | cut -f 2- -d ":" | tr -d " ")
$ TOKEN=$(kubectl describe secret $(kubectl get secrets | grep ^default | cut -f1 -d ' ') | grep -E '^token' | cut -f2 -d':' | tr -d " ")
$ curl $APISERVER/api --header "Authorization: Bearer $TOKEN" --insecure
{
  "kind": "APIVersions",
  "versions": [
    "v1"
  ],
  "serverAddressByClientCIDRs": [
    {
      "clientCIDR": "0.0.0.0/0",
      "serverAddress": "10.0.1.149:443"
    }
  ]
}</pre>
&nbsp;
具体见文档
https://kubernetes.io/docs/tasks/access-application-cluster/access-cluster/#without-kubectl-proxy-post-v13x