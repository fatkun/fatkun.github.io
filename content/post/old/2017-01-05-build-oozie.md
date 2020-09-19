---
title: 编译oozie
author: fatkun
type: post
date: -001-11-30T00:00:00+00:00
draft: true
url: /?p=2021
categories:
  - 未分类

---
编译命令  
bin/mkdistro.sh -DskipTests
Unknown host repository.codehaus.org  
http://stackoverflow.com/questions/32248317/building-oozie-unknown-host-repository-codehaus-org
修改pom文件
<pre escaped="true" lang="xml">&lt;repositories&gt;
     &lt;repository&gt;
       &lt;id&gt;Codehaus repository&lt;/id&gt;
       &lt;name&gt;codehaus-mule-repo&lt;/name&gt;
       &lt;url&gt;https://repository-master.mulesoft.org/nexus/content/groups/public/
       &lt;/url&gt;
       &lt;layout&gt;default&lt;/layout&gt;
     &lt;/repository&gt;
   &lt;/repositories&gt;</pre>