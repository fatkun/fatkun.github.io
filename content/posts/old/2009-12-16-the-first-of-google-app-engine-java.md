---
title: 开始学习Google App Engine(Java) – 准备篇
author: fatkun
type: post
date: 2009-12-15T12:40:01+00:00
url: /2009/12/the-first-of-google-app-engine-java.html
views:
  - 23
duoshuo_thread_id:
  - 6300408706894922498
categories:
  - J2EE
tags:
  - GAE
  - Google
  - JAVA

---
发现我挺喜欢Google的东西~~也算一个G粉吧~~~好喜欢啊好喜欢·~好多免费的东西~~
## 什么是Google App Engine?

> 按我的理解，简单的一句话就是Google提供一个网络平台，这个平台目前支持 Python、Java，我们可以通过编写程序运行在google的服务器上。
<!--more-->

**官方的介绍：**
> <p style="padding-top: 1em; padding-right: 0px; padding-bottom: 0px; padding-left: 0px; line-height: 20px; margin: 0px;">>   Google App Engine 可让您在 Google 的基础架构上运行您的网络应用程序。App Engine 应用程序易于构建和维护，并可根据您的访问量和数据存储需要的增长轻松扩展。使用 Google App Engine，将不再需要维护服务器：您只需上传您的应用程序，它便可立即为您的用户提供服务。> </p>
> <p style="padding-top: 1em; padding-right: 0px; padding-bottom: 0px; padding-left: 0px; line-height: 20px; margin: 0px;">>   您可以使用 <a style="color: #0000cc;" href="http://www.google.com/a/">Google 企业应用套件</a>通过自己的域名（例如 <code style="font-family: monospace; color: #007000; font-size: 10pt;">http://www.example.com/</code>）提供应用程序。或者，您可以使用 <code style="font-family: monospace; color: #007000; font-size: 10pt;">appspot.com</code> 域上的免费域名来为您的应用程序提供服务。您可以与全世界的人共享您的应用程序，也可以限制为只有贵组织的成员可以访问。> </p>
> <p style="padding-top: 1em; padding-right: 0px; padding-bottom: 0px; padding-left: 0px; line-height: 20px; margin: 0px;">>   Google App Engine 支持以几种编程语言编写的应用程序。通过 App Engine 的 Java 运行时环境，您可以使用标准 Java 技术（包括 JVM、Java servlet 和 Java 编程语言，或使用基于 JVM 的解释器或解译器的任何其他语言，例如 JavaScript 或 Ruby）构建应用程序。App Engine 还提供一个专用的 Python 运行时环境，该环境包括一个快速 Python 解释器和 Python 标准库。Java 和 Python 运行时环境构建为确保应用程序快速、安全运行，并不受系统上的其他应用程序的干扰。> </p>
> <p style="padding-top: 1em; padding-right: 0px; padding-bottom: 0px; padding-left: 0px; line-height: 20px; margin: 0px;">>   在 App Engine 中，您只需为您使用的资源付费。没有设置成本，也没有重复的费用。您的应用程序使用的资源，如存储空间和带宽以千兆字节衡量，并以有竞争力的费率收费。您可以控制您的应用程序可以消费的最大资源量，使其一直保持在预算范围内。> </p>
> <p style="padding-top: 1em; padding-right: 0px; padding-bottom: 0px; padding-left: 0px; line-height: 20px; margin: 0px;">>   可以免费开始使用 App Engine。所有应用程序都可以使用多达 500 MB 的存储空间，以及可支持每月约 500 万页面浏览量的足够的 CPU 和带宽，完全免费。为您的应用程序启用付费后，您的免费配额将提高，您只需为使用的超过免费水平的资源付费。> </p>
<p style="padding-top: 1em; padding-right: 0px; padding-bottom: 0px; padding-left: 0px; line-height: 20px; margin: 0px;">  Google为我们提供了充足的免费限额~~要知道有多少？可以到这里看看<a style="color: #551a8b; vertical-align: middle; zoom: 1; padding-right: 4px;" href="http://code.google.com/intl/zh-CN/appengine/docs/quotas.html">配额</a>。真的足够了，对于我来说~~</p>
<p style="padding-top: 1em; padding-right: 0px; padding-bottom: 0px; padding-left: 0px; line-height: 20px; margin: 0px;">  可以到app Engine 的官方网站来看一下，<a href="http://code.google.com/intl/zh-CN/appengine/">http://code.google.com/intl/zh-CN/appengine/</a>，这里有很多的文档。大部分都汉化了~~ /yy</p>
## 前提准备工作

下载东西啦~~到<a href="http://code.google.com/intl/zh-CN/appengine/downloads.html" target="_blank">这里</a>下载
  1. 下载Google App Engine SDK for Java
  2. 如果你需要使用GWT（Google Web Toolkit）,到<a href="http://code.google.com/intl/zh-CN/webtoolkit/download.html" target="_blank">这里</a>下载(可选)
  3. 下载 Eclipse Google 插件,在<a href="http://code.google.com/intl/zh-CN/eclipse/docs/download.html" target="_blank">这里</a>啊~
下载eclipse插件，可以通过以下地址：（按版本选择）,如果你还不会安装，看[这里][1]的Detailed instructions for installation from update sites，里面有图文介绍耶！！
另外说的是如果你前面下载了两个SDK，那就下载插件的时候就不用勾选那两个SDK了~~直接选插件那个就行。
> <div id="_mcePaste" style="position: absolute; left: -10000px; top: 326px; width: 1px; height: 1px; overflow-x: hidden; overflow-y: hidden;">>   Eclipse 3.5 (Galileo)> </div>
> <div id="_mcePaste" style="position: absolute; left: -10000px; top: 326px; width: 1px; height: 1px; overflow-x: hidden; overflow-y: hidden;">>   http://dl.google.com/eclipse/plugin/3.5> </div>
> <div id="_mcePaste" style="position: absolute; left: -10000px; top: 326px; width: 1px; height: 1px; overflow-x: hidden; overflow-y: hidden;">>   Eclipse 3.4 (Ganymede)> </div>
> <div id="_mcePaste" style="position: absolute; left: -10000px; top: 326px; width: 1px; height: 1px; overflow-x: hidden; overflow-y: hidden;">>   http://dl.google.com/eclipse/plugin/3.4> </div>
> <div id="_mcePaste" style="position: absolute; left: -10000px; top: 326px; width: 1px; height: 1px; overflow-x: hidden; overflow-y: hidden;">>   Eclipse 3.3 (Europa)> </div>
> <div id="_mcePaste" style="position: absolute; left: -10000px; top: 326px; width: 1px; height: 1px; overflow-x: hidden; overflow-y: hidden;">>   http://dl.google.com/eclipse/plugin/3.3> </div>
> > Eclipse 3.5 (Galileo)
> > http://dl.google.com/eclipse/plugin/3.5
> > Eclipse 3.4 (Ganymede)
> > http://dl.google.com/eclipse/plugin/3.4
> > Eclipse 3.3 (Europa)
> > http://dl.google.com/eclipse/plugin/3.3
如果你是自己下载SDK的，那就解压到任意目录下(小白问：“任意目录是哪个目录？”汗！)，先解压，以后有用。~
这时我们可以在eclipse看到工具栏多出的三个小图标，各点一下试试咯~~
如果你是自己下载SDK的，需要配置SDK的路径。我们可以在新建app engine项目的界面下面看到有配置SDK的链接，点进去，然后选择前面解压的路径~另外GWT可以不勾选~如果你用不上~
就这样吧，懒得截图了·~
下一篇文章写它文档带了的一个小例子~一个简单的留言本~那些例子真的很容易懂啊。。大家多看看文档就会了~~
我也是刚学的，才学两天~所以不会太深入~·哇咔咔~
原创文章：fatkun，转载请保留本文链接。

 [1]: http://code.google.com/intl/zh-CN/eclipse/docs/download.html