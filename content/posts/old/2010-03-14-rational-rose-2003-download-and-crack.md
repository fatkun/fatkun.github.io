---
title: Rational Rose 2003 下载及破解方法
author: fatkun
type: post
date: 2010-03-14T06:18:52+00:00
url: /2010/03/rational-rose-2003-download-and-crack.html
views:
  - 16
duoshuo_thread_id:
  - 6300408718110491394
categories:
  - 电脑知识

---
这学期要学UML，做实验要用到这个软件。所以找到了这个破解版的破解方法。。还挺烦的。。不过测试破解成功。。
本文来源：<http://blog.csdn.net/fenglibing/archive/2007/08/17/1747693.aspx>
&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-
下载地址（没测试过是否可用）
Flashget://W0ZMQVNIR0VUXWZsYXNoZ2V0eDovL3xtaHRzfGNtRjBhVzl1WVd3Z2NtOXpaVEl3TURNdWNtRnl8MzYxMDMxMTIxfDJBOTdFNkVBN0Q4QTQ5ODhBODBDQTVGMjFCRjQ5NkRDfC9bRkxBU0hHRVRd
<!--more-->操作：

１、安装Rational Rose2003时，在需选择安装项的时候，只选择Rational Rose EnterPrise Edition即可，不需选择其他项。
２、安装好Rational Rose Enterprise Editon后，打开rose2003crack.rar压缩包，里面有四个文件，分别为flexlm.cpl、license.dat、lmgrd.exe、rational.exe。
３、用记事本或者是EditPlus打开license.dat文件，大约在文件的中间位置有：SERVER Microsoft ANY
DAEMON rational “C:\Program Files\Rational\common\rational.exe”　　将其修改为：SERVER 计算机名　ANY DAEMON rational “自己安装的目录\rational.exe”后，保存
注：若是按默认目录安装，则只需修改计算机名即可。
４、将license.dat、 lmgrd.exe 、rational.exe三个文件一起拷贝到：安装目录\rational\common\ 下面。
如：若为默认则为：C:\Program Files\Rational\common\目录。
５、将flexlm.cpl拷贝到system32目录下。如win2000系统中为C:\WINNT\system32目录。
６、进入控制面板，则在控制面板的上方会增加了一个图标，即FLEXlm License Manager，将其打开，在Setup页中lmgrd.exe右侧目录写为：C:\Program Files\Rational\Common\lmgrd.exe（若为默认安装目录）
License File右侧目录写为：C:\Program Files\Rational\Common\license.dat
７、回到Control页，点击Start，若出现”Server Started”，则表示已经成功，可以点击Status,若状态为：计算机名：license server UP(MASTER)则成功。
８、这时可打开安装的Rational Rose Enterprise Edition，若还是出现Error，则打开Rational License Key Administrator ，点击工具栏中的第一个工具（Start WIzard）,点击下一步，在Server Name中的名字改为自己的计算机名即可。因现在的学习需在使用Rational Rose，所以进行了安装，但确实花了不少工夫，所以特把自己安装的经验来跟大家一起分享，希望能对大家有所帮助。