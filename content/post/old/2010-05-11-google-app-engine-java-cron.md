---
title: GAE-使用cron计划任务(java)时无法上传cron.xml，500错误
author: fatkun
type: post
date: 2010-05-11T11:50:22+00:00
url: /2010/05/google-app-engine-java-cron.html
views:
  - 26
duoshuo_thread_id:
  - 6300408725391803137
categories:
  - J2EE
tags:
  - GAE
  - google app engine

---
## 错误信息

> com.google.appengine.tools.admin.AdminException: Unable to update app: Error posting to URL: https://appengine.google.com/api/datastore/cron/update?app_id=fatkuns&version=4&  
> 500 Internal Server Error
> Server Error (500)  
> A server error has occurred.
> at com.google.appengine.tools.admin.AppAdminImpl.update(AppAdminImpl.java:62)
> at com.google.appengine.eclipse.core.proxy.AppEngineBridgeImpl.deploy(AppEngineBridgeImpl.java:271)
> at com.google.appengine.eclipse.core.deploy.DeployProjectJob.runInWorkspace(DeployProjectJob.java:145)
> at org.eclipse.core.internal.resources.InternalWorkspaceJob.run(InternalWorkspaceJob.java:38)
> at org.eclipse.core.internal.jobs.Worker.run(Worker.java:55)
> Caused by: java.io.IOException: Error posting to URL: https://appengine.google.com/api/datastore/cron/update?app_id=fatkuns&version=4&  
> 500 Internal Server Error
> Server Error (500)  
> A server error has occurred.
> at com.google.appengine.tools.admin.ServerConnection.send(ServerConnection.java:149)
> at com.google.appengine.tools.admin.ServerConnection.post(ServerConnection.java:82)
> at com.google.appengine.tools.admin.AppVersionUpload.send(AppVersionUpload.java:559)
> at com.google.appengine.tools.admin.AppVersionUpload.updateCron(AppVersionUpload.java:260)
> at com.google.appengine.tools.admin.AppVersionUpload.doUpload(AppVersionUpload.java:133)
> at com.google.appengine.tools.admin.AppAdminImpl.update(AppAdminImpl.java:56)
> &#8230; 4 more
## 原因：

<span style="font-weight: normal; font-size: 13px;">cron.xml文件书写不正确</span>
<span style="font-size: 13px;"><strong>记得<timezone>Asia/Shanghai</timezone>这个是必须写的，不然无法上传，官方的例子居然有一个没写</strong></span>
> <?xml version=&#8221;1.0&#8243; encoding=&#8221;UTF-8&#8243;?>
> <cronentries>
> <cron>
> <url>/cron</url>
> <description>描述</description>
> <schedule>every 2 minutes</schedule>
> <timezone>Asia/Shanghai</timezone>
> </cron>
> </cronentries>
<div id="_mcePaste" style="position: absolute; left: -10000px; top: 597px; width: 1px; height: 1px; overflow-x: hidden; overflow-y: hidden;">  <?xml version=&#8221;1.0&#8243; encoding=&#8221;UTF-8&#8243;?></div>
<div id="_mcePaste" style="position: absolute; left: -10000px; top: 597px; width: 1px; height: 1px; overflow-x: hidden; overflow-y: hidden;">  <cronentries></div>
<div id="_mcePaste" style="position: absolute; left: -10000px; top: 597px; width: 1px; height: 1px; overflow-x: hidden; overflow-y: hidden;">  <cron></div>
<div id="_mcePaste" style="position: absolute; left: -10000px; top: 597px; width: 1px; height: 1px; overflow-x: hidden; overflow-y: hidden;">  <url>/cron</url></div>
<div id="_mcePaste" style="position: absolute; left: -10000px; top: 597px; width: 1px; height: 1px; overflow-x: hidden; overflow-y: hidden;">  <description>描述</description></div>
<div id="_mcePaste" style="position: absolute; left: -10000px; top: 597px; width: 1px; height: 1px; overflow-x: hidden; overflow-y: hidden;">  <schedule>every 2 minutes</schedule></div>
<div id="_mcePaste" style="position: absolute; left: -10000px; top: 597px; width: 1px; height: 1px; overflow-x: hidden; overflow-y: hidden;">  <timezone>Asia/Shanghai</timezone></div>
<div id="_mcePaste" style="position: absolute; left: -10000px; top: 597px; width: 1px; height: 1px; overflow-x: hidden; overflow-y: hidden;">  </cron></div>
<div id="_mcePaste" style="position: absolute; left: -10000px; top: 597px; width: 1px; height: 1px; overflow-x: hidden; overflow-y: hidden;">  </cronentries></div>
**更新：**发现如果 url填写错误也会上传失败，正确的方式是写“/xxxx”这样的路径，不能写全路径..