---
title: k8s安装zookeeper
author: fatkun
type: post
date: 2018-04-30T09:53:32+00:00
url: /2018/04/k8s-install-zookeeper.html
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:2084:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #007800;">HOST_DOMAIN</span>=<span style="color: #000000; font-weight: bold;">`</span><span style="color: #c20cb9; font-weight: bold;">hostname</span> -a<span style="color: #000000; font-weight: bold;">`</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">function</span> print_servers<span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #7a0874; font-weight: bold;">&#41;</span> <span style="color: #7a0874; font-weight: bold;">&#123;</span>
             <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #7a0874; font-weight: bold;">&#40;</span> <span style="color: #007800;">i</span>=<span style="color: #000000;">1</span>; i<span style="color: #000000; font-weight: bold;">&lt;</span>=<span style="color: #007800;">$ZK_REPLICAS</span>; i++ <span style="color: #7a0874; font-weight: bold;">&#41;</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
            <span style="color: #000000; font-weight: bold;">do</span>
                    <span style="color: #7a0874; font-weight: bold;">echo</span> <span style="color: #ff0000;">&quot;server.<span style="color: #007800;">$i</span>=<span style="color: #007800;">$NAME</span>-<span style="color: #007800;">$((i-1)</span>).<span style="color: #007800;">${HOST_DOMAIN#*.}</span>:<span style="color: #007800;">$ZK_SERVER_PORT</span>:<span style="color: #007800;">$ZK_ELECTION_PORT</span>&quot;</span>
            <span style="color: #000000; font-weight: bold;">done</span>
    <span style="color: #7a0874; font-weight: bold;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">HOST_DOMAIN=`hostname -a`
    
    function print_servers() {
             for (( i=1; i&lt;=$ZK_REPLICAS; i++ ))
            do
                    echo &quot;server.$i=$NAME-$((i-1)).${HOST_DOMAIN#*.}:$ZK_SERVER_PORT:$ZK_ELECTION_PORT&quot;
            done
    }</p></div>
    ";i:2;s:1022:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">FROM xxxxxxxxxxxxx<span style="color: #000000; font-weight: bold;">/</span>google_samples<span style="color: #000000; font-weight: bold;">/</span>k8szk:v3
    &nbsp;
    COPY zkGenConfig.sh <span style="color: #000000; font-weight: bold;">/</span>opt<span style="color: #000000; font-weight: bold;">/</span>zookeeper<span style="color: #000000; font-weight: bold;">/</span>bin<span style="color: #000000; font-weight: bold;">/</span>
    &nbsp;
    RUN <span style="color: #c20cb9; font-weight: bold;">chmod</span> +x <span style="color: #000000; font-weight: bold;">/</span>usr<span style="color: #000000; font-weight: bold;">/</span>bin<span style="color: #000000; font-weight: bold;">/</span>zkGenConfig.sh</pre></td></tr></table><p class="theCode" style="display:none;">FROM xxxxxxxxxxxxx/google_samples/k8szk:v3
    
    COPY zkGenConfig.sh /opt/zookeeper/bin/
    
    RUN chmod +x /usr/bin/zkGenConfig.sh</p></div>
    ";}
categories:
  - docker
tags:
  - k8s

---
使用命令安装，里面使用了gcr的镜像换一下
kubectl create -f \  
https://raw.githubusercontent.com/kubernetes/contrib/master/statefulsets/zookeeper/zookeeper.yaml
但装完之后，使用zkCli.sh 无法连接，检查配置，发现server配置的hostname不能互相连接，需要使用全域名访问
修改zkGenConfig.sh文件，重新打包
<pre escaped="true" lang="bash">HOST_DOMAIN=`hostname -a`

function print_servers() {
         for (( i=1; i&lt;=$ZK_REPLICAS; i++ ))
        do
                echo "server.$i=$NAME-$((i-1)).${HOST_DOMAIN#*.}:$ZK_SERVER_PORT:$ZK_ELECTION_PORT"
        done
}
</pre>
<pre escaped="true" lang="bash">FROM xxxxxxxxxxxxx/google_samples/k8szk:v3

COPY zkGenConfig.sh /opt/zookeeper/bin/

RUN chmod +x /usr/bin/zkGenConfig.sh
</pre>