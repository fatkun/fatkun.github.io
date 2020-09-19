---
title: 安装VS2008失败，Microsoft Visual Studio Web创作组件安装失败
author: fatkun
type: post
date: 2011-04-02T06:45:05+00:00
url: /2011/04/vs2008-microsoft-visual-studio-web.html
duoshuo_thread_id:
  - 6300408803552658178
categories:
  - 电脑知识
tags:
  - Microsoft Visual Studio Web创作组件
  - VS2008

---
我的计算机系统是vista家庭版的，已经安装了Office 2007，在安装VS2008的过程中出现安装失败的窗口。
先把vs2008镜像文件下的\WCU\WebDesignerCore\WebDesignerCore.EXE 手动解压(Winrar)，然后找一个office2007光盘或光盘镜像，找到Office.zh-cn文件夹，把该文件夹复制，覆盖WebDesignerCore.EXE 解压后的office.zh-cn文件夹，再点击里面的setup.exe。最后就可以点击根目录下的setup.exe计科安装成功。如果不先执行覆盖操作，就会提示找不到“Office.zh-cn\OfficeMUI.msi文件”文件。
原文：http://blog.csdn.net/shilmey/archive/2010/03/04/5347447.aspx  
更多：http://blogs.itecn.net/blogs/wbpluto/archive/2008/02/17/visual-studio-2008-web.aspx