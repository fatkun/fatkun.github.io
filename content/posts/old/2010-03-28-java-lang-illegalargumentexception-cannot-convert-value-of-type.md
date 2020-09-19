---
title: 'java.lang.IllegalArgumentException: Cannot convert value of type [$Proxy0[解决方法]'
author: fatkun
type: post
date: 2010-03-27T16:35:20+00:00
url: /2010/03/java-lang-illegalargumentexception-cannot-convert-value-of-type.html
views:
  - 36
duoshuo_thread_id:
  - 6300408718253097730
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:1709:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;bean</span> <span style="color: #000066;">class</span>=<span style="color: #ff0000;">&quot;org.springframework.aop.framework.autoproxy.BeanNameAutoProxyCreator&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>  
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;property</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;proxyTargetClass&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
           <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>true<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
           <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/bean<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">&lt;bean class=&quot;org.springframework.aop.framework.autoproxy.BeanNameAutoProxyCreator&quot;&gt;  
    &lt;property name=&quot;proxyTargetClass&quot;&gt;
           &lt;value&gt;true&lt;/value&gt;
           &lt;/property&gt;
    &lt;/bean&gt;</p></div>
    ";}
categories:
  - J2EE
tags:
  - 事务
  - 报错

---
> Caused by: java.lang.IllegalArgumentException: Cannot convert value of type [$Proxy0 implementing com.mysoft.applications.database.interfaces.MyInterface,org.springframework.aop.SpringProxy,org.springframework.aop.framework.Advised] to required type [ibatis.ibator.services.TestService] for property &#8216;service&#8217;: no matching editors or conversion strategy found  
> at org.springframework.beans.TypeConverterDelegate.convertIfNecessary(TypeConverterDelegate.java:231)  
> at org.springframework.beans.TypeConverterDelegate.convertIfNecessary(TypeConverterDelegate.java:138)  
> at org.springframework.beans.BeanWrapperImpl.convertForProperty(BeanWrapperImpl.java:386)  
> &#8230; 42 more
在配置事务时加入了aspectjweaver.jar这个包后出现了这个问题。
本文来源：<http://blog.csdn.net/taochenpfj/archive/2009/07/29/4390158.aspx>  
<!--more-->

如果在Spring配置文件中配置的事务是通过AOP标签实现的，那就在<aop:config />中增加proxy-target-class=&#8221;true&#8221;属性。就异常显示的信息可以看到，Spring在转换时，主要是将代理类转换成接口，反而不能转换成实际类。
如果是通过bean方式增加事务控制，则在配置文件中增加
<pre escaped="true" lang="xml">&lt;bean class="org.springframework.aop.framework.autoproxy.BeanNameAutoProxyCreator">  
&lt;property name="proxyTargetClass">
       &lt;value>true&lt;/value>
       &lt;/property>
&lt;/bean>
</pre>
上面这段配置信息只是一部分。其他的各位再摸索吧！
这里有个兄弟也是这样的问题，他的是bean控制事务的http://longterm.javaeye.com/blog/394395