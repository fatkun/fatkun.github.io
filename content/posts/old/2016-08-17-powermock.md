---
title: 使用powermock
author: fatkun
type: post
date: 2016-08-17T06:10:27+00:00
url: /2016/08/powermock.html
duoshuo_thread_id:
  - 6319676557812040450
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:6322:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;">        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;dependency<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;groupId<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>org.easymock<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/groupId<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;artifactId<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>easymock<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/artifactId<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;version<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>3.3.1<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/version<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;scope<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>test<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/scope<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/dependency<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;dependency<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;groupId<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>org.powermock<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/groupId<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;artifactId<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>powermock-module-junit4<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/artifactId<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;version<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>1.6.5<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/version<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;scope<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>test<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/scope<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/dependency<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;dependency<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;groupId<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>org.powermock<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/groupId<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;artifactId<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>powermock-api-easymock<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/artifactId<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;version<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>1.6.5<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/version<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;scope<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>test<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/scope<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/dependency<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">        &lt;dependency&gt;
                &lt;groupId&gt;org.easymock&lt;/groupId&gt;
                &lt;artifactId&gt;easymock&lt;/artifactId&gt;
                &lt;version&gt;3.3.1&lt;/version&gt;
                &lt;scope&gt;test&lt;/scope&gt;
            &lt;/dependency&gt;
            &lt;dependency&gt;
                &lt;groupId&gt;org.powermock&lt;/groupId&gt;
                &lt;artifactId&gt;powermock-module-junit4&lt;/artifactId&gt;
                &lt;version&gt;1.6.5&lt;/version&gt;
                &lt;scope&gt;test&lt;/scope&gt;
            &lt;/dependency&gt;
            &lt;dependency&gt;
                &lt;groupId&gt;org.powermock&lt;/groupId&gt;
                &lt;artifactId&gt;powermock-api-easymock&lt;/artifactId&gt;
                &lt;version&gt;1.6.5&lt;/version&gt;
                &lt;scope&gt;test&lt;/scope&gt;
            &lt;/dependency&gt;</p></div>
    ";i:2;s:800:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">java.<span style="color: #006633;">lang</span>.<span style="color: #003399;">NoSuchMethodError</span><span style="color: #339933;">:</span> javassist.<span style="color: #006633;">CtMethod</span>.<span style="color: #006633;">hasAnnotation</span><span style="color: #009900;">&#40;</span>Ljava<span style="color: #339933;">/</span>lang<span style="color: #339933;">/</span><span style="color: #000000; font-weight: bold;">Class</span><span style="color: #339933;">;</span><span style="color: #009900;">&#41;</span>Z</pre></td></tr></table><p class="theCode" style="display:none;">java.lang.NoSuchMethodError: javassist.CtMethod.hasAnnotation(Ljava/lang/Class;)Z</p></div>
    ";i:3;s:2232:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;">        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;dependency<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;groupId<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>org.javassist<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/groupId<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;artifactId<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>javassist<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/artifactId<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;version<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>3.19.0-GA<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/version<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
                <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;scope<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>test<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/scope<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/dependency<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">        &lt;dependency&gt;
                &lt;groupId&gt;org.javassist&lt;/groupId&gt;
                &lt;artifactId&gt;javassist&lt;/artifactId&gt;
                &lt;version&gt;3.19.0-GA&lt;/version&gt;
                &lt;scope&gt;test&lt;/scope&gt;
            &lt;/dependency&gt;</p></div>
    ";}
categories:
  - J2EE

---
在pom.xml加入
<pre escaped="true" lang="xml">&lt;dependency&gt;
            &lt;groupId&gt;org.easymock&lt;/groupId&gt;
            &lt;artifactId&gt;easymock&lt;/artifactId&gt;
            &lt;version&gt;3.3.1&lt;/version&gt;
            &lt;scope&gt;test&lt;/scope&gt;
        &lt;/dependency&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;org.powermock&lt;/groupId&gt;
            &lt;artifactId&gt;powermock-module-junit4&lt;/artifactId&gt;
            &lt;version&gt;1.6.5&lt;/version&gt;
            &lt;scope&gt;test&lt;/scope&gt;
        &lt;/dependency&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;org.powermock&lt;/groupId&gt;
            &lt;artifactId&gt;powermock-api-easymock&lt;/artifactId&gt;
            &lt;version&gt;1.6.5&lt;/version&gt;
            &lt;scope&gt;test&lt;/scope&gt;
        &lt;/dependency&gt;</pre>
如果报错，有可能项目中包含有低版本的javassist
<pre escaped="true" lang="java">java.lang.NoSuchMethodError: javassist.CtMethod.hasAnnotation(Ljava/lang/Class;)Z</pre>
尝试加入新版本的javassist，注意classpath的优先级是否正确
<pre escaped="true" lang="xml">&lt;dependency&gt;
            &lt;groupId&gt;org.javassist&lt;/groupId&gt;
            &lt;artifactId&gt;javassist&lt;/artifactId&gt;
            &lt;version&gt;3.19.0-GA&lt;/version&gt;
            &lt;scope&gt;test&lt;/scope&gt;
        &lt;/dependency&gt;</pre>
使用文档可以看官网：https://github.com/jayway/powermock