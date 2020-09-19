---
title: WIN7的菜单栏无法隐藏解决方法（QtTabBar）
author: fatkun
type: post
date: 2010-06-29T07:10:59+00:00
url: /2010/06/win7-menu-can-not-hide.html
views:
  - 28
duoshuo_thread_id:
  - 6300408743540556546
categories:
  - 电脑知识
tags:
  - QTTabBar
  - win7
  - 无法隐藏
  - 菜单栏

---
## 问题

  1. 不能隐藏菜单栏
  2. 已经不选菜单栏了，可它还是显示“File，Edit&#8230;.”这一列，在文件夹选项里设置也无效。今天装了个QTTabBar之后，就一直这样菜单栏隐藏不了了，把QTTabBar卸了也还是这样。
  3. 按照网上说的修改组策略的方法依然不可以隐藏
## 解决方法

按“WIN+R”（也就是键盘左下角的徽标键+R），输入gpedit.msg 打开组策略编辑器（也可以在控制面板中搜索“策略”找到），依次展开“用户配置→管理模版→Windows组件→Windows资源管理器”，然后在右侧窗口中双击“在Windows资源管理器中显示菜单栏”，设置为“已禁用”。
[![组策略][1]][2]{.flickr-image.alignnone}
[][2]{.flickr-image.alignnone}然后现在试试能不能把菜单隐藏掉？如果不行，再看下面。
[![phpvnSF2r][3]][4]{.flickr-image.alignnone}
如果依然不行，把下面的内容保存为1.bat，然后双击它运行。
<pre>reg delete "HKCU\Software\Microsoft\Internet Explorer\Toolbar\WebBrowser" /v ITBar7Layout /f
reg delete "HKCU\Software\Microsoft\Internet Explorer\Toolbar\WebBrowser" /v ITBar7Height /f
reg delete "HKCU\Software\Microsoft\Internet Explorer\Toolbar\ShellBrowser" /v ITBar7Layout /f
reg delete "HKCU\Software\Microsoft\Internet Explorer\Toolbar\ShellBrowser" /v ITBar7Height /f</pre>

 [1]: http://farm5.static.flickr.com/4117/4744639019_573812d9b9_b.jpg
 [2]: http://www.flickr.com/photos/fatkun/4744639019/ "组策略"
 [3]: http://farm5.static.flickr.com/4073/4744647861_4cf606668c.jpg
 [4]: http://www.flickr.com/photos/fatkun/4744647861/ "phpvnSF2r"