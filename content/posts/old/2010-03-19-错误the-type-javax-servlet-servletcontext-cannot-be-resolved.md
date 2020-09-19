---
title: 错误:The type javax.servlet.ServletContext cannot be resolved
author: fatkun
type: post
date: 2010-03-19T12:08:56+00:00
url: /2010/03/错误the-type-javax-servlet-servletcontext-cannot-be-resolved.html
views:
  - 51
duoshuo_thread_id:
  - 6300408718160823042
categories:
  - J2EE
tags:
  - 错误

---
碰到这个错误，原来是tomcat里的包没有加入Build Path，我把servlet-api.jar加入jdk1.6.0\jre\lib\ext 目录就解决了。  
&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;
来源：http://blog.csdn.net/cnrefresh/archive/2009/03/10/3977242.aspx  
软件包 javax.servlet 不存在
原来这个包在web服务器才有，j2se中并没有，所以导致了错误。  
解决方法：  
方法(1) 找到%tomcat%\common\lib目录下的servlet-api.jar，把这个路径添加到环境变量classpath当中，就可以了。（这个好像不是很管用，我重装了tomcat之后，再重新配置好像就不行了）  
方法(2) 找到%tomcat%\common\lib目录下的servlet-api.jar，把这个jar添加到%java_home%\jdk1.6.0\jre\lib\ext目录下面，不同的jdk版本都一样。