---
title: 在Windows上编译hadoop cdh5.4
author: fatkun
type: post
date: 2015-05-17T14:07:27+00:00
url: /2015/05/compile-hadoop-cdh5-4-on-windows.html
duoshuo_thread_id:
  - 6300410895910568705
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:2563:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;build<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    ...
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;plugins<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      ...
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;plugin<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
          <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;groupId<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>org.apache.maven.plugins<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/groupId<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
          <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;artifactId<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>maven-eclipse-plugin<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/artifactId<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
          <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;version<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>2.6<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/version<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/plugin<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/plugins<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/build<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">&lt;build&gt;
    ...
      &lt;plugins&gt;
      ...
        &lt;plugin&gt;
          &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
          &lt;artifactId&gt;maven-eclipse-plugin&lt;/artifactId&gt;
          &lt;version&gt;2.6&lt;/version&gt;
        &lt;/plugin&gt;
      &lt;/plugins&gt;
    &lt;/build&gt;</p></div>
    ";}
categories:
  - hadoop
tags:
  - 5.4
  - cdh
  - hadoop
  - 编译

---
<h2 data-anchor-id="tbvu">  我的环境</h2>
系统:win8.1 ， maven3.1, eclipse 4.4
hadoop cdh5.4对应apache的源码是hadoop 2.6
<h2 id="准备条件" data-anchor-id="tbvu">  准备条件</h2>
<p data-anchor-id="3iwr">  安装以下软件，见源码src/BUILDING.txt里的要求<br /> jdk1.7<br /> <a href="https://github.com/google/protobuf/releases" target="_blank">protoc.exe 2.5</a><br /> cygwin<br /> maven3<br /> cygwin<br /> <a href="http://www.cmake.org/download/" target="_blank">cmake</a> （注意要单独安装，不要使用cygwin里面的，否则在编译hadoop-hdfs会有cmake错误）<br /> <a href="http://www.microsoft.com/en-us/download/details.aspx?id=8279" target="_blank">Windows SDK</a> 或者 Visual Studio 2010 Professional（我用的是Windows SDK）</p>
<p data-anchor-id="zlh3">  配置环境变量JAVA_HOME等，把下载的protoc.exe放入c:\windows</p>
<div class="md-section-divider"></div>
<h2 id="下载源码" data-anchor-id="qaxk">  下载源码</h2>
<p data-anchor-id="06vn">  略</p>
<div class="md-section-divider"></div>
<h2 id="编译" data-anchor-id="q8u0">  编译</h2>
<p data-anchor-id="gjw9">  使用&#8221;Windows SDK 7.1 Command Prompt&#8221;进入命令行</p>
<pre data-anchor-id="lkay"><code>mvn org.apache.maven.plugins:maven-eclipse-plugin:2.6:eclipse
mvn package -Pdist,native-win -DskipTests -Dtar
</code></pre>
<div class="md-section-divider"></div>
<h2 id="导入eclipse" data-anchor-id="d3aa">  导入eclipse</h2>
<p data-anchor-id="kvt9">  为了使得Eclipse中安装的Maven插件，同windows中安装的那个相同，需要让eclipse中的maven重新定位一下，点击Window -> Preference -> Maven -> Installation -> Add进行设置</p>
<p data-anchor-id="t8hn">  使用import -> Existing Projects into Workspace方式导入</p>
<div class="md-section-divider"></div>
<h2 id="错误处理" data-anchor-id="c7my">  错误处理</h2>
<div class="md-section-divider"></div>
<h3 id="报错-request-to-merge-when-filtering-is-not-identical" data-anchor-id="b4hd">  报错 Request to merge when &#8216;filtering&#8217; is not identical</h3>
<pre data-anchor-id="ehns"><code>Failed to execute goal org.apache.maven.plugins:maven-eclipse-plugin:2.8:eclipse (default-cli) on project hadoop-yarn-common: Request to merge when 'filtering' is not identical. Original=resource src/main/resources: output=target/classes, include=[], exclude=[yarn-version-info.properties|**/*.java], test=false, filtering=false, merging with=resource src/main/resources: output=target/classes, include=[yarn-version-info.properties], exclude=[**/*.java], test=false, filtering=true -&gt; [Help 1]
</code></pre>
<p data-anchor-id="5bwd">  改用mvn org.apache.maven.plugins:maven-eclipse-plugin:2.6:eclipse 编译</p>
<p data-anchor-id="wkn5">  或者修改hadoop-2.6.0-cdh5.4.0\src\hadoop-common-project\hadoop-common\pom.xml文件，加入</p>
<pre lang="xml" escaped="true">&lt;build&gt;
...
  &lt;plugins&gt;
  ...
    &lt;plugin&gt;
      &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
      &lt;artifactId&gt;maven-eclipse-plugin&lt;/artifactId&gt;
      &lt;version&gt;2.6&lt;/version&gt;
    &lt;/plugin&gt;
  &lt;/plugins&gt;
&lt;/build&gt;</pre>
<p data-anchor-id="1j1h">  <a href="http://stackoverflow.com/questions/1397903/setting-project-for-eclipse-using-maven" target="_blank">来源</a></p>
<div class="md-section-divider"></div>
<h3 id="报错-echorequestproto-cannot-be-resolved" data-anchor-id="9l7i">  报错 EchoRequestProto cannot be resolved</h3>
<p data-anchor-id="zdyo">  在根src目录下执行一次 mvn install -DskipTests<br /> 你会看到最终这个是在hadoop-common*test.jar包里面的，应该是由hadoop-common-project\hadoop-common\src\test\proto编译出来的</p>
<div class="md-section-divider"></div>
<h3 id="报错-avrorecord-cannot-be-resolved" data-anchor-id="6ar4">  报错 AvroRecord cannot be resolved</h3>
<p data-anchor-id="e2eo">  把hadoop-common*test.jar加入bulid path，或者下载下载avro-tools-x.x.x.jar，进入源码根目录下的“hadoop-common-project\hadoop-common\src\test\avro”执行命令，java -jar <所在目录>/avro-tools-1.7.7.jar compile schema avroRecord.avsc ..\java</p>
<div class="md-section-divider"></div>
<h3 id="报错-applicationattemptstartdatapbimpl-cannot-be-resolved" data-anchor-id="9lul">  报错 ApplicationAttemptStartDataPBImpl cannot be resolved</h3>
<p data-anchor-id="4389">  这个是因为解压的时候失败了，导致文件丢失。还有一个文件是ApplicationAttemptStartDataPBImpl，目录在hadoop-2.6.0-cdh5.4.0\src\hadoop-yarn-project\hadoop-yarn\hadoop-yarn-server\hadoop-yarn-server-applicationhistoryservice\src\main\java\org\apache\hadoop\yarn\server\applicationhistoryservice\records\impl\pb<br /> 在Windows下文件名目录不能长于260个字符，想办法把目录缩短一些，然后把文件拷贝回来。</p>
<div class="md-section-divider"></div>
<h3 id="导入eclipse后maven-jdktools报错" data-anchor-id="sgxm">  导入eclipse后maven jdk.tools报错</h3>
<p data-anchor-id="q01y">  修改hadoop-annotations/pom.xml，找到jdk.tools，把“<span id="MathJax-Element-153-Frame" class="MathJax"><span id="MathJax-Span-3953" class="math"><span id="MathJax-Span-3954" class="mrow"><span id="MathJax-Span-3955" class="texatom"><span id="MathJax-Span-3956" class="mrow"><span id="MathJax-Span-3957" class="mi">j</span><span id="MathJax-Span-3958" class="mi">a</span><span id="MathJax-Span-3959" class="mi">v</span><span id="MathJax-Span-3960" class="mi">a</span><span id="MathJax-Span-3961" class="mo">.</span><span id="MathJax-Span-3962" class="mi">h</span><span id="MathJax-Span-3963" class="mi">o</span><span id="MathJax-Span-3964" class="mi">m</span><span id="MathJax-Span-3965" class="mi">e</span></span></span><span id="MathJax-Span-3966" class="mo">.</span><span id="MathJax-Span-3967" class="mo">.</span><span id="MathJax-Span-3968" class="texatom"><span id="MathJax-Span-3969" class="mrow"><span id="MathJax-Span-3970" class="mo">/</span></span></span><span id="MathJax-Span-3971" class="mo">”</span><span id="MathJax-Span-3972" class="texatom"><span id="MathJax-Span-3973" class="mrow"><span id="MathJax-Span-3974" class="mo">改</span></span></span><span id="MathJax-Span-3975" class="texatom"><span id="MathJax-Span-3976" class="mrow"><span id="MathJax-Span-3977" class="mo">为</span></span></span><span id="MathJax-Span-3978" class="mo">“</span></span></span></span>{JAVA_HOME}/”,也就是jdk下面的tools.jar路径</p>
<div class="md-section-divider"></div>
<h3 id="提示maven-resource-plugin版本低于24错误" data-anchor-id="ewgx">  提示maven-resource-plugin版本低于2.4错误</h3>
<p data-anchor-id="q6jc">  修改pom.xml文件，把版本改为2.4，忘记是哪个pom了</p>
<div class="md-section-divider"></div>
<h3 id="maven报错lifecycle错误" data-anchor-id="8cui">  maven报错lifecycle错误</h3>
<p data-anchor-id="k7ww">  在eclipse配置maven，把这些错误忽略掉。</p>
<div class="md-section-divider"></div>
<h3 id="其他还有一些bulid-path的报错" data-anchor-id="rqtq">  其他还有一些bulid path的报错</h3>
<p data-anchor-id="6wgc">  看着错误处理吧</p>
<div class="md-section-divider"></div>
<h2 id="参考" data-anchor-id="vxyq">  参考</h2>
<p data-anchor-id="4rxn">  <a href="https://wiki.apache.org/hadoop/Hadoop2OnWindows" target="_blank">https://wiki.apache.org/hadoop/Hadoop2OnWindows</a><br /> <a href="http://blog.csdn.net/oneinmore/article/details/44984419" target="_blank">将Hadoop 2.6.0源码导入到Eclipse</a><br /> <a href="http://www.srccodes.com/p/article/38/build-install-configure-run-apache-hadoop-2.2.0-microsoft-windows-os" target="_blank">Build, Install, Configure and Run Apache Hadoop 2.2.0 in Microsoft Windows OS</a></p>