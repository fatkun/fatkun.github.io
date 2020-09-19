---
title: 解决“已在此计算机上检测到Microsoft Visual C++ 2010 Redistributable的更新版本”
author: fatkun
type: post
date: 2015-05-17T08:55:41+00:00
url: /2015/05/microsoft-visual-c-2010-redistributable.html
duoshuo_thread_id:
  - 6300410895860237057
categories:
  - 未分类

---
安装Windows SDK for win7时失败，查看错误日志发现是安装vcredist_x64.exe时出错，原因是已经安装了Microsoft Visual C++ 2010 Redistributable新版本，再装旧版本会失败。
安装vcredist_x64.exe提示 “<span class="ask-title ">已在此计算机上检测到Microsoft Visual C++ 2010 Redistributable的更新版本</span>” 错误。
## 解决

尝试卸载Microsoft Visual C++ 2010 Redistributable，如果还不行删除注册表 HKEY\_LOCAL\_MACHINE\SOFTWARE\Wow6432Node\Microsoft\VisualStudio\10.0
## 来源

http://blogs.msdn.com/b/vsnetsetup/archive/2014/07/17/installation-failing-with-a-newer-version-of-microsoft-visual-c-2010-redistributable-has-been-detected-on-this-machine.aspx