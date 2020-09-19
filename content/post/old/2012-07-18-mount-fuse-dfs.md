---
title: 挂载fuse-dfs遇到的问题
author: fatkun
type: post
date: 2012-07-18T15:27:01+00:00
url: /2012/07/mount-fuse-dfs.html
duoshuo_thread_id:
  - 6300408865787740930
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:1123:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">for</span> f <span style="color: #000000; font-weight: bold;">in</span> $<span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #c20cb9; font-weight: bold;">find</span> <span style="color: #007800;">$HADOOP_HOME</span><span style="color: #000000; font-weight: bold;">/</span> <span style="color: #660033;">-name</span> <span style="color: #ff0000;">'*.jar'</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
    <span style="color: #000000; font-weight: bold;">do</span>
            <span style="color: #7a0874; font-weight: bold;">export</span> <span style="color: #007800;">CLASSPATH</span>=<span style="color: #007800;">$CLASSPATH</span>:<span style="color: #007800;">$f</span>
    <span style="color: #000000; font-weight: bold;">done</span></pre></td></tr></table><p class="theCode" style="display:none;">for f in $(find $HADOOP_HOME/ -name '*.jar')
    do
            export CLASSPATH=$CLASSPATH:$f
    done</p></div>
    ";i:2;s:2625:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #666666; font-style: italic;">#!/bin/sh</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">for</span> f <span style="color: #000000; font-weight: bold;">in</span> $<span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #c20cb9; font-weight: bold;">find</span> <span style="color: #007800;">$HADOOP_HOME</span><span style="color: #000000; font-weight: bold;">/</span> <span style="color: #660033;">-name</span> <span style="color: #ff0000;">'*.jar'</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
    <span style="color: #000000; font-weight: bold;">do</span>
            <span style="color: #7a0874; font-weight: bold;">export</span> <span style="color: #007800;">CLASSPATH</span>=<span style="color: #007800;">$CLASSPATH</span>:<span style="color: #007800;">$f</span>
    <span style="color: #000000; font-weight: bold;">done</span>
    <span style="color: #7a0874; font-weight: bold;">export</span> <span style="color: #007800;">LD_LIBRARY_PATH</span>=<span style="color: #007800;">$LD_LIBRARY_PATH</span>:<span style="color: #007800;">$JAVA_HOME</span><span style="color: #000000; font-weight: bold;">/</span>jre<span style="color: #000000; font-weight: bold;">/</span>lib<span style="color: #000000; font-weight: bold;">/</span>amd64<span style="color: #000000; font-weight: bold;">/</span>server
    <span style="color: #7a0874; font-weight: bold;">export</span> <span style="color: #007800;">LD_LIBRARY_PATH</span>=<span style="color: #007800;">$LD_LIBRARY_PATH</span>:<span style="color: #007800;">$HADOOP_HOME</span><span style="color: #000000; font-weight: bold;">/</span>c++<span style="color: #000000; font-weight: bold;">/</span>lib
    .<span style="color: #000000; font-weight: bold;">/</span>fuse_dfs_wrapper.sh dfs:<span style="color: #000000; font-weight: bold;">//</span>localhost:<span style="color: #000000;">8020</span> <span style="color: #000000; font-weight: bold;">/</span>mnt<span style="color: #000000; font-weight: bold;">/</span>dfs <span style="color: #660033;">-d</span> <span style="color: #000000; font-weight: bold;">&amp;</span></pre></td></tr></table><p class="theCode" style="display:none;">#!/bin/sh
    
    for f in $(find $HADOOP_HOME/ -name '*.jar')
    do
            export CLASSPATH=$CLASSPATH:$f
    done
    export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$JAVA_HOME/jre/lib/amd64/server
    export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$HADOOP_HOME/c++/lib
    ./fuse_dfs_wrapper.sh dfs://localhost:8020 /mnt/dfs -d &amp;</p></div>
    ";}
categories:
  - hadoop
tags:
  - hadoop

---
以下是在ubuntu12.04 amd64， hadoop cdh3u3下安装
在${HADOOP_HOME}/contrib/fuse-dfs目录下已经帮我编译了一个64bit的fuse-dfs了，不用自己编译（苦逼，自己编译出错=。=）
## 缺少某些.so文件

把这些so加入到LD\_LIBRARY\_PATH中，可以写入~/.bashrc文件  
export LD\_LIBRARY\_PATH=$LD\_LIBRARY\_PATH:$JAVA_HOME/jre/lib/amd64/server  
export LD\_LIBRARY\_PATH=$LD\_LIBRARY\_PATH:$HADOOP_HOME/c++/lib
## 提示/etc/fuse.conf没权限

把当前用户加入fuse组， adduser 用户名 fuse  
检查一下/etc/fuse.conf权限是否是可读
## 挂载点input/output error

变成一堆？？？号，原因是没有加上-d参数  
./fuse\_dfs\_wrapper.sh dfs://localhost:8020 /mnt/dfs -d  
变成？？？可以通过sudo umount /mnt/xxx解除挂载
## class not found

Caused by: java.lang.ClassNotFoundException: org.apache.hadoop.conf.Configuration  
把hadoop的lib加进去
<pre escaped="true" lang="bash">for f in $(find $HADOOP_HOME/ -name '*.jar')
do
        export CLASSPATH=$CLASSPATH:$f
done</pre>
最终的脚本是：
<pre escaped="true" lang="bash">#!/bin/sh

for f in $(find $HADOOP_HOME/ -name '*.jar')
do
        export CLASSPATH=$CLASSPATH:$f
done
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$JAVA_HOME/jre/lib/amd64/server
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$HADOOP_HOME/c++/lib
./fuse_dfs_wrapper.sh dfs://localhost:8020 /mnt/dfs -d &</pre>