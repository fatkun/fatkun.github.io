---
title: Linux 编译 hadoop-cdh4.2.1
author: fatkun
type: post
date: 2014-08-10T08:33:37+00:00
url: /2014/08/linux-compile-hadoop-cdh4-2-1.html
duoshuo_thread_id:
  - 6300410318501708545
wp-syntax-cache-content:
  - |
    a:4:{i:1;s:5980:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;">  <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;mirror<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;id<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>nexus-osc<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/id<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;mirrorOf<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>central<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/mirrorOf<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>Nexus osc<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;url<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>http://maven.oschina.net/content/groups/public/<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/url<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/mirror<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    &nbsp;
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;mirror<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;id<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>nexus-spring<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/id<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;mirrorOf<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>cdh.repo<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/mirrorOf<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>spring<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;url<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>http://repo.spring.io/repo/<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/url<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/mirror<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    &nbsp;
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;mirror<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;id<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>nexus-spring2<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/id<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;mirrorOf<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>cdh.releases.repo<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/mirrorOf<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>spring2<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;url<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>http://repo.spring.io/repo/<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/url<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/mirror<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">  &lt;mirror&gt;
      &lt;id&gt;nexus-osc&lt;/id&gt;
      &lt;mirrorOf&gt;central&lt;/mirrorOf&gt;
      &lt;name&gt;Nexus osc&lt;/name&gt;
      &lt;url&gt;http://maven.oschina.net/content/groups/public/&lt;/url&gt;
      &lt;/mirror&gt;
    
      &lt;mirror&gt;
      &lt;id&gt;nexus-spring&lt;/id&gt;
      &lt;mirrorOf&gt;cdh.repo&lt;/mirrorOf&gt;
      &lt;name&gt;spring&lt;/name&gt;
      &lt;url&gt;http://repo.spring.io/repo/&lt;/url&gt;
      &lt;/mirror&gt;
      
      &lt;mirror&gt;
      &lt;id&gt;nexus-spring2&lt;/id&gt;
      &lt;mirrorOf&gt;cdh.releases.repo&lt;/mirrorOf&gt;
      &lt;name&gt;spring2&lt;/name&gt;
      &lt;url&gt;http://repo.spring.io/repo/&lt;/url&gt;
      &lt;/mirror&gt;</p></div>
    ";i:2;s:364:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">mvn package <span style="color: #660033;">-DskipTests</span> -Pdist,native <span style="color: #660033;">-Dtar</span></pre></td></tr></table><p class="theCode" style="display:none;">mvn package -DskipTests -Pdist,native -Dtar</p></div>
    ";i:3;s:1591:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #7a0874; font-weight: bold;">cd</span> <span style="color: #000000; font-weight: bold;">/</span>opt<span style="color: #000000; font-weight: bold;">/</span>cloudera<span style="color: #000000; font-weight: bold;">/</span>parcels<span style="color: #000000; font-weight: bold;">/</span>CDH<span style="color: #000000; font-weight: bold;">/</span>lib<span style="color: #000000; font-weight: bold;">/</span>hadoop-mapreduce
    <span style="color: #666666; font-style: italic;"># 上传jar包</span>
    <span style="color: #c20cb9; font-weight: bold;">chmod</span> <span style="color: #000000;">755</span> hadoop-mapreduce-client-app-2.0.0-cdh4.2.1-<span style="color: #000000;">20140801</span>.jar
    <span style="color: #c20cb9; font-weight: bold;">ln</span> <span style="color: #660033;">-snf</span> hadoop-mapreduce-client-app-2.0.0-cdh4.2.1-<span style="color: #000000;">20140801</span>.jar hadoop-mapreduce-client-app.jar
    <span style="color: #c20cb9; font-weight: bold;">mv</span> hadoop-mapreduce-client-app-2.0.0-cdh4.2.1.jar <span style="color: #000000; font-weight: bold;">/</span>tmp</pre></td></tr></table><p class="theCode" style="display:none;">cd /opt/cloudera/parcels/CDH/lib/hadoop-mapreduce
    # 上传jar包
    chmod 755 hadoop-mapreduce-client-app-2.0.0-cdh4.2.1-20140801.jar
    ln -snf hadoop-mapreduce-client-app-2.0.0-cdh4.2.1-20140801.jar hadoop-mapreduce-client-app.jar
    mv hadoop-mapreduce-client-app-2.0.0-cdh4.2.1.jar /tmp</p></div>
    ";i:4;s:1055:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="other" style="font-family:monospace;">Failed to execute goal org.apache.maven.plugins:maven-antrun-plugin:1.6:run (make) on project hadoop-common: An Ant BuildException has occured: Execute failed: java.io.IOException: Cannot run program &quot;cmake&quot; (in directory &quot;/home/xx/hadoop-fix/hadoop/build/hadoop-2.0.0-cdh4.2.1/src/hadoop-common-project/hadoop-common/target/native&quot;): java.io.IOException: error=2, No such file or directory -&gt; [Help 1]</pre></td></tr></table><p class="theCode" style="display:none;">Failed to execute goal org.apache.maven.plugins:maven-antrun-plugin:1.6:run (make) on project hadoop-common: An Ant BuildException has occured: Execute failed: java.io.IOException: Cannot run program &quot;cmake&quot; (in directory &quot;/home/xx/hadoop-fix/hadoop/build/hadoop-2.0.0-cdh4.2.1/src/hadoop-common-project/hadoop-common/target/native&quot;): java.io.IOException: error=2, No such file or directory -&gt; [Help 1]</p></div>
    ";}
categories:
  - hadoop

---
## 配置

安装Maven, Ant, Findbugs, protobuf, cmake  
参考:http://cn.soulmachine.me/blog/20140214/
注意CDH4.2.1需要用protobuf2.4.1编译，否则hadoop-common那里报错
在apache-maven-3.0.5/conf/settings.xml 更改maven镜像
<pre lang="xml" escaped="true">&lt;mirror&gt;
  &lt;id&gt;nexus-osc&lt;/id&gt;
  &lt;mirrorOf&gt;central&lt;/mirrorOf&gt;
  &lt;name&gt;Nexus osc&lt;/name&gt;
  &lt;url&gt;http://maven.oschina.net/content/groups/public/&lt;/url&gt;
  &lt;/mirror&gt;

  &lt;mirror&gt;
  &lt;id&gt;nexus-spring&lt;/id&gt;
  &lt;mirrorOf&gt;cdh.repo&lt;/mirrorOf&gt;
  &lt;name&gt;spring&lt;/name&gt;
  &lt;url&gt;http://repo.spring.io/repo/&lt;/url&gt;
  &lt;/mirror&gt;
  
  &lt;mirror&gt;
  &lt;id&gt;nexus-spring2&lt;/id&gt;
  &lt;mirrorOf&gt;cdh.releases.repo&lt;/mirrorOf&gt;
  &lt;name&gt;spring2&lt;/name&gt;
  &lt;url&gt;http://repo.spring.io/repo/&lt;/url&gt;
  &lt;/mirror&gt;</pre>
## 编译

<pre lang="bash" escaped="true">mvn package -DskipTests -Pdist,native -Dtar</pre>
## 替换jar包

从src/hadoop-mapreduce-project/hadoop-mapreduce-client/hadoop-mapreduce-client-app/target里面拿出mr-app.jar重命名为hadoop-mapreduce-client-app-2.0.0-cdh4.2.1-20140801.jar
<pre lang="bash" escaped="true">cd /opt/cloudera/parcels/CDH/lib/hadoop-mapreduce
# 上传jar包
chmod 755 hadoop-mapreduce-client-app-2.0.0-cdh4.2.1-20140801.jar
ln -snf hadoop-mapreduce-client-app-2.0.0-cdh4.2.1-20140801.jar hadoop-mapreduce-client-app.jar
mv hadoop-mapreduce-client-app-2.0.0-cdh4.2.1.jar /tmp
</pre>
## 错误处理

<pre lang="other" escaped="true">Failed to execute goal org.apache.maven.plugins:maven-antrun-plugin:1.6:run (make) on project hadoop-common: An Ant BuildException has occured: Execute failed: java.io.IOException: Cannot run program "cmake" (in directory "/home/xx/hadoop-fix/hadoop/build/hadoop-2.0.0-cdh4.2.1/src/hadoop-common-project/hadoop-common/target/native"): java.io.IOException: error=2, No such file or directory -&gt; [Help 1]</pre>
没有安装cmake，yum install cmake