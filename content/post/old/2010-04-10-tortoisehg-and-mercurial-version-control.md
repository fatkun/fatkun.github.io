---
title: TortoiseHg 1.0.1 与 Mercurial 1.5.1 版本控制软件
author: fatkun
type: post
date: 2010-04-10T15:12:11+00:00
url: /2010/04/tortoisehg-and-mercurial-version-control.html
views:
  - 9
duoshuo_thread_id:
  - 6300408719117124353
categories:
  - 胡言乱语
tags:
  - hg
  - svn
  - 版本控制

---
Mercurial 是一款跨平台的快速、轻量级的分布式源代码管理软件， 使用python开发，免费开源。高效的实现、简易的学习曲线使得它既适合于大规模项目，也适用于小项目的代码管理。目前很多著名项目都已经开始使用 Mercurial来管理代码， 如 Mozilla、OpenOffice、Python等。**Google Code在09年早期也已经提供了对Mercurial的支持。（在后台source设置一下即可）**
TortoiseHg为Mercurial集成了一系列图形化工具和Shell扩展， 类似于TortoiseSVN为SVN提供的功能。  
![][1]  
<!--more-->

  
TortoiseHg还是那只龟~如果用惯了TortoiseSVN，这个也是很容易上手的。
暂时感觉hg 相对于 svn的好处是 ：
1，不像svn那样在每个目录都建一个.svn文件夹
2，有一个完整的本地库，所以浏览历史版本是很快的，不用联网。
3，如果不能联网可以先提交到本地的版本库，有网络再提交上服务器
官方网站：<http://tortoisehg.bitbucket.org/>
win_x86版下载地址：<http://bitbucket.org/tortoisehg/stable/downloads/tortoisehg-1.0.1-hg-1.5.1-x86.msi>
This is a bug fix release. We recommend all users upgrade to this release.
<h2 id="packaged-versions" style="margin-top: 0.83em !important; padding-top: 0px; margin-bottom: 0.83em !important; font: normal normal normal 1.3em/normal 'Lucida Grande', 'Trebuchet MS', Tahoma, Arial, sans-serif; letter-spacing: -1px; font-size: 2em !important; margin-right: 0px !important; margin-left: 0px !important; font-family: Georgia, Times, 'Times New Roman', serif; font-weight: normal;">  Packaged Versions</h2>
<ul style="margin-top: 1.33em; margin-right: 0px; margin-bottom: 1.33em; margin-left: 0px; list-style-position: inside; padding-left: 1px;">  <li>    Mercurial 1.5.1  </li>
  <li>    GTK has been downgraded from 2.18.7 to 2.16.6  </li>
  <li>    dulwich has been upgraded to 0.5.1  </li>
  <li>    See extension-versions.txt in the install directory for the complete list of bundled extensions and modules and their versions  </li></ul>

 [1]: http://farm5.static.flickr.com/4009/4508101528_e9d8aa127b_o.png