---
title: 误删contacts.apk解决方法（不用刷机）
author: fatkun
type: post
date: 2011-10-03T15:21:11+00:00
url: /2011/10/recovery-contacts-apk.html
duoshuo_thread_id:
  - 6300408819893666561
categories:
  - Android
  - 电脑知识
tags:
  - Android
  - contacts.apk
  - 误删android文件

---
从完整的刷机包内，注意，版本最好是和你手机一致的。如果找不到，可以上网问别人要。
在压缩包目录下android2.3.6.zip\system\app找到Contacts.apk，Contacts.odex文件，如果你把其他文件也删了，也可以按照这个步骤。
连接手机U盘，复制到SD卡。
然后用ROOT Explor从SD卡把这两个文件复制到 手机的这个目录下/system/app/
最后一步！注意，一定要给这两个文件**设置权限**，在RE里按住文件，选permissions，都勾上read/write权限。
重启一下你的手机，就可以编辑联系人了。