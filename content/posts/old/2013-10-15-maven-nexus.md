---
title: 在windows部署nexus编译hadoop cdh4.3
author: fatkun
type: post
date: 2013-10-14T18:02:45+00:00
url: /2013/10/maven-nexus.html
duoshuo_thread_id:
  - 6300410041228854017
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:613:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">set</span> <span style="color: #007800;">CATALINA_OPTS</span>=-server <span style="color: #660033;">-Xms256m</span> <span style="color: #660033;">-Xmx1024m</span> -XX:<span style="color: #007800;">PermSize</span>=512m -XX:<span style="color: #007800;">MaxPermSize</span>=1024m</pre></td></tr></table><p class="theCode" style="display:none;">set CATALINA_OPTS=-server -Xms256m -Xmx1024m -XX:PermSize=512m -XX:MaxPermSize=1024m</p></div>
    ";i:2;s:586:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">&lt;</span>localRepository<span style="color: #000000; font-weight: bold;">&gt;</span>E:\apache-maven-3.1.0\repository<span style="color: #000000; font-weight: bold;">&lt;/</span>localRepository<span style="color: #000000; font-weight: bold;">&gt;</span></pre></td></tr></table><p class="theCode" style="display:none;">&lt;localRepository&gt;E:\apache-maven-3.1.0\repository&lt;/localRepository&gt;</p></div>
    ";i:3;s:4454:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">    <span style="color: #000000; font-weight: bold;">&lt;</span>mirror<span style="color: #000000; font-weight: bold;">&gt;</span>
          <span style="color: #000000; font-weight: bold;">&lt;</span><span style="color: #c20cb9; font-weight: bold;">id</span><span style="color: #000000; font-weight: bold;">&gt;</span>central<span style="color: #000000; font-weight: bold;">&lt;/</span><span style="color: #c20cb9; font-weight: bold;">id</span><span style="color: #000000; font-weight: bold;">&gt;</span>
          <span style="color: #000000; font-weight: bold;">&lt;</span>mirrorOf<span style="color: #000000; font-weight: bold;">&gt;</span>central<span style="color: #000000; font-weight: bold;">&lt;/</span>mirrorOf<span style="color: #000000; font-weight: bold;">&gt;</span>
          <span style="color: #000000; font-weight: bold;">&lt;</span>name<span style="color: #000000; font-weight: bold;">&gt;</span>central<span style="color: #000000; font-weight: bold;">&lt;/</span>name<span style="color: #000000; font-weight: bold;">&gt;</span>
          <span style="color: #000000; font-weight: bold;">&lt;</span>url<span style="color: #000000; font-weight: bold;">&gt;</span>http:<span style="color: #000000; font-weight: bold;">//</span>127.0.0.1:<span style="color: #000000;">8080</span><span style="color: #000000; font-weight: bold;">/</span>nexus<span style="color: #000000; font-weight: bold;">/</span>content<span style="color: #000000; font-weight: bold;">/</span>repositories<span style="color: #000000; font-weight: bold;">/</span>central<span style="color: #000000; font-weight: bold;">&lt;/</span>url<span style="color: #000000; font-weight: bold;">&gt;</span>
        <span style="color: #000000; font-weight: bold;">&lt;/</span>mirror<span style="color: #000000; font-weight: bold;">&gt;</span>
        <span style="color: #000000; font-weight: bold;">&lt;</span>mirror<span style="color: #000000; font-weight: bold;">&gt;</span>
          <span style="color: #000000; font-weight: bold;">&lt;</span><span style="color: #c20cb9; font-weight: bold;">id</span><span style="color: #000000; font-weight: bold;">&gt;</span>cdh.repo<span style="color: #000000; font-weight: bold;">&lt;/</span><span style="color: #c20cb9; font-weight: bold;">id</span><span style="color: #000000; font-weight: bold;">&gt;</span>
          <span style="color: #000000; font-weight: bold;">&lt;</span>mirrorOf<span style="color: #000000; font-weight: bold;">&gt;</span>cdh.repo<span style="color: #000000; font-weight: bold;">&lt;/</span>mirrorOf<span style="color: #000000; font-weight: bold;">&gt;</span>
          <span style="color: #000000; font-weight: bold;">&lt;</span>name<span style="color: #000000; font-weight: bold;">&gt;</span>cdh.repo<span style="color: #000000; font-weight: bold;">&lt;/</span>name<span style="color: #000000; font-weight: bold;">&gt;</span>
          <span style="color: #000000; font-weight: bold;">&lt;</span>url<span style="color: #000000; font-weight: bold;">&gt;</span>http:<span style="color: #000000; font-weight: bold;">//</span>localhost:<span style="color: #000000;">8080</span><span style="color: #000000; font-weight: bold;">/</span>nexus<span style="color: #000000; font-weight: bold;">/</span>content<span style="color: #000000; font-weight: bold;">/</span>repositories<span style="color: #000000; font-weight: bold;">/</span>cdh.repo<span style="color: #000000; font-weight: bold;">&lt;/</span>url<span style="color: #000000; font-weight: bold;">&gt;</span>
        <span style="color: #000000; font-weight: bold;">&lt;/</span>mirror<span style="color: #000000; font-weight: bold;">&gt;</span>
      <span style="color: #000000; font-weight: bold;">&lt;/</span>mirrors<span style="color: #000000; font-weight: bold;">&gt;</span></pre></td></tr></table><p class="theCode" style="display:none;">    &lt;mirror&gt;
          &lt;id&gt;central&lt;/id&gt;
          &lt;mirrorOf&gt;central&lt;/mirrorOf&gt;
          &lt;name&gt;central&lt;/name&gt;
          &lt;url&gt;http://127.0.0.1:8080/nexus/content/repositories/central&lt;/url&gt;
        &lt;/mirror&gt;
        &lt;mirror&gt;
          &lt;id&gt;cdh.repo&lt;/id&gt;
          &lt;mirrorOf&gt;cdh.repo&lt;/mirrorOf&gt;
          &lt;name&gt;cdh.repo&lt;/name&gt;
          &lt;url&gt;http://localhost:8080/nexus/content/repositories/cdh.repo&lt;/url&gt;
        &lt;/mirror&gt;
      &lt;/mirrors&gt;</p></div>
    ";}
categories:
  - 未分类
tags:
  - hadoop
  - maven
  - nexus

---
## 部署nexus

死活启动不了nexus，下载了多个版本。最后下载tomcat7 + 2.5的war才可以。把war包丢到webapps目录下，启动tomcat会自动解压。。停掉tomcat，把目录改名为nexus吧。。
修改nexus\WEB-INF\plexus.properties里的路径，jar包会下载到这里
nexus-work=E:/sonatype-work/nexus
&nbsp;
为避免出现tomcat内存溢出，新建文件setenv.bat，设置内存
<pre lang="bash" escaped="true">set CATALINA_OPTS=-server -Xms256m -Xmx1024m -XX:PermSize=512m -XX:MaxPermSize=1024m</pre>
重新启动tomcat，启动完成后，访问http://localhost:8080/nexus， 用户名:admin 密码:admin123
&nbsp;
## 配置maven

修改 {maven}/conf/settings.xml文件，指定本地repo目录，会把lib下载到这里
<pre lang="bash" escaped="true">&lt;localRepository&gt;E:\apache-maven-3.1.0\repository&lt;/localRepository&gt;</pre>
修改镜像，找到mirrors这里
<pre lang="bash" escaped="true">&lt;mirror&gt;
      &lt;id&gt;central&lt;/id&gt;
      &lt;mirrorOf&gt;central&lt;/mirrorOf&gt;
      &lt;name&gt;central&lt;/name&gt;
      &lt;url&gt;http://127.0.0.1:8080/nexus/content/repositories/central&lt;/url&gt;
    &lt;/mirror&gt;
    &lt;mirror&gt;
      &lt;id&gt;cdh.repo&lt;/id&gt;
      &lt;mirrorOf&gt;cdh.repo&lt;/mirrorOf&gt;
      &lt;name&gt;cdh.repo&lt;/name&gt;
      &lt;url&gt;http://localhost:8080/nexus/content/repositories/cdh.repo&lt;/url&gt;
    &lt;/mirror&gt;
  &lt;/mirrors&gt;</pre>
上面的cdh.repo是我新增的，要在nexus上新增一个mirror，注意mirrorOf这个参数，这个是从pom.xml里的repositories找出来的，而且有个路径。
&nbsp;
## 编译hadoop

编译前要改hadoop-project\pom.xml等里的protobuf-java版本，否则会下载个2.4的版本会用不了。
<dependency>  
<groupId>com.google.protobuf</groupId>  
<artifactId>protobuf-java</artifactId>  
<version>2.5.0</version>  
<scope>compile</scope>  
</dependency>
需要安装好cygwin和protoc.exe（从网站下载丢到cygwin的bin目录就可以了。。），需要在cygwin里执行 mvn eclipse:eclipse
&nbsp;
&nbsp;