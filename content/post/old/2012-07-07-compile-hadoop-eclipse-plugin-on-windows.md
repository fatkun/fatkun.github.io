---
title: 在Windows下编译hadoop eclipse-plugin
author: fatkun
type: post
date: 2012-07-07T09:06:01+00:00
url: /2012/07/compile-hadoop-eclipse-plugin-on-windows.html
duoshuo_thread_id:
  - 6300408859722777345
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:320:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="html" style="font-family:monospace;">ant -Declipse.home=D:/eclipse/ -Dversion=0.20.2-cdh3u3 jar</pre></td></tr></table><p class="theCode" style="display:none;">ant -Declipse.home=D:/eclipse/ -Dversion=0.20.2-cdh3u3 jar</p></div>
    ";i:2;s:754:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="html" style="font-family:monospace;">An internal error occurred during: &quot;Map/Reduce location status updater&quot;.
    org/codehaus/jackson/map/JsonMappingException
    An internal error occurred during: &quot;Connecting to DFS myhadoop&quot;.
    org/apache/hadoop/thirdparty/guava/common/collect/LinkedListMultimap</pre></td></tr></table><p class="theCode" style="display:none;">An internal error occurred during: &quot;Map/Reduce location status updater&quot;.
    org/codehaus/jackson/map/JsonMappingException
    An internal error occurred during: &quot;Connecting to DFS myhadoop&quot;.
    org/apache/hadoop/thirdparty/guava/common/collect/LinkedListMultimap</p></div>
    ";i:3;s:210:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="html" style="font-family:monospace;">&nbsp;</pre></td></tr></table><p class="theCode" style="display:none;"></p></div>
    ";}
categories:
  - hadoop
tags:
  - hadoop

---
1.首先准备好ant和maven，配置好ANT\_HOME和MAVEN\_HOME的环境变量，把%ANT_HOME%/bin和%MAVEN/HOME%/bin配置在PATH变量。  
（貌似如果只是编译eclipse-plugin不用安装maven）
我这里的版本是hadoop-core-0.20.2-cdh3u3，其他版本的编译方法也一样。
&nbsp;
2.在你下载的hadoop根目录下，把hadoop-core-0.20.2-cdh3u3.jar解压到build\classes目录下。  
3.把hadoop-core-0.20.2-cdh3u3.jar拷贝到build目录下
&nbsp;
4.从CMD进入到src\contrib\eclipse-plugin目录，执行以下命令：  
eclipse.home=D:/eclipse/需要指定你eclipse的安装目录  
version=0.20.2-cdh3u3 是你的hadoop版本
&nbsp;
<pre lang="html">ant -Declipse.home=D:/eclipse/ -Dversion=0.20.2-cdh3u3 jar</pre>
会在build\contrib\eclipse-plugin生成jar文件，但这时还不可以用。  
否则会出现错误：
<pre lang="html">An internal error occurred during: "Map/Reduce location status updater".
org/codehaus/jackson/map/JsonMappingException
An internal error occurred during: "Connecting to DFS myhadoop".
org/apache/hadoop/thirdparty/guava/common/collect/LinkedListMultimap</pre>
<pre lang="html"></pre>
5.还要从{hadoop根目录}/lib下，找到jackson-core-asl-1.5.2.jar,jackson-mapper-asl-1.5.2.jar,guava-r09-jarjar.jar把他们都解压出来放入刚生成的hadoop-eclipse-plugin-0.20.2-cdh3u3.jar classes目录下（可以通过winrar直接拖进去）
&nbsp;
6.最后，把hadoop-eclipse-plugin-0.20.2-cdh3u3.jar放进eclipse的dropin目录，重启eclipse就可以了。
&nbsp;
PS:本来想把这些包拷贝进lib目录下，然后改MANIFEST.MF，发现打死不可以。。不知道为什么
&nbsp;
我编译的版本，适用于eclipse3.7和hadoop-0.20.2-cdh3u3：<a href="http://115.com/file/e7xzixp3#hadoop-eclipse-plugin-0.20.2-cdh3u3.jar" target="_blank">下载</a>