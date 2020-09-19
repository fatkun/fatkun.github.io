---
title: eclipse上单步调试Hive
author: fatkun
type: post
date: 2012-04-14T10:06:16+00:00
url: /2012/04/eclipse-debug-hive.html
duoshuo_thread_id:
  - 6300408840928101121
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:3285:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">    <span style="color: #003399;">URL</span> hconfurl <span style="color: #339933;">=</span> getClassLoader<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getResource</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;hive-default.xml&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>hconfurl <span style="color: #339933;">==</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          l4j.<span style="color: #006633;">debug</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;hive-default.xml not found.&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">else</span> <span style="color: #009900;">&#123;</span>
          addResource<span style="color: #009900;">&#40;</span>hconfurl<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
        <span style="color: #003399;">URL</span> hsiteurl <span style="color: #339933;">=</span> getClassLoader<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getResource</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;hive-site.xml&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>hsiteurl <span style="color: #339933;">==</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          l4j.<span style="color: #006633;">debug</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;hive-site.xml not found.&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">else</span> <span style="color: #009900;">&#123;</span>
          addResource<span style="color: #009900;">&#40;</span>hsiteurl<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">    URL hconfurl = getClassLoader().getResource(&quot;hive-default.xml&quot;);
        if (hconfurl == null) {
          l4j.debug(&quot;hive-default.xml not found.&quot;);
        } else {
          addResource(hconfurl);
        }
        URL hsiteurl = getClassLoader().getResource(&quot;hive-site.xml&quot;);
        if (hsiteurl == null) {
          l4j.debug(&quot;hive-site.xml not found.&quot;);
        } else {
          addResource(hsiteurl);
        }</p></div>
    ";}
categories:
  - J2EE
tags:
  - debug
  - hive

---
在百度找到这篇文章：[在Windows eclipse上单步调试Hive教程][1]
可是我死活搞不定在windows安装hadoop和hive，cgywin不靠普啊。。还是在ubuntu下调试了。
## 准备

前提条件是你已经部署好hadoop和hive，能够正常的执行hive查询。
我在~/workspace/hive新建了两个目录lib和conf
  1. 从hive目录中的lib和hadoop目录中的lib复制一份到一个目录里，我是放在~/workspace/hive/lib
  2. 还要把hadoop目录下的hadoop*.jar都拷贝过来吧。
  3. 如果用mysql做metastore的数据库，还需要把mysql-connector的lib加上
  4. 把hive的conf文件夹拷贝过来（要已配置好的conf文件哦）
  5. 把hive中的src目录拷贝进来
## 创建项目

在这个目录下（~/workspace/hive/src/cli）的代码是hive命令行的代码，我们可以通过调试它来了解hive的执行过程。
在这个目录下，用eclipse新建一个项目。
配置bulid path，把我们准备好的lib全部加上
这个时候，代码应该没有编译错误了，如果有，请检查一下那个lib没加上。
还有个重要的步骤！hive是怎样找它的配置文件的呢？
我们要把conf目录加入classpath中，在debug configuration中的Classpath，点击左侧的advanced，add exteral path，选上我们准备好的conf目录。
这样就可以开始debug了！
如果你运行报does not have a sch错误，应该是由于没找到配置文件引起的。  
&nbsp;
顺便看看hive是怎么找到配置文件的。  
都是通过getClassLoader().getResource()方法来获取的，所以配置文件夹必须在classpath中！
<pre escaped="true" lang="java">URL hconfurl = getClassLoader().getResource("hive-default.xml");
    if (hconfurl == null) {
      l4j.debug("hive-default.xml not found.");
    } else {
      addResource(hconfurl);
    }
    URL hsiteurl = getClassLoader().getResource("hive-site.xml");
    if (hsiteurl == null) {
      l4j.debug("hive-site.xml not found.");
    } else {
      addResource(hsiteurl);
    }</pre>

 [1]: http://wenku.baidu.com/view/f4d9b407e87101f69e319599.html