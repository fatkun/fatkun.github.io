---
title: Hibernate状态transient、persistent、detached的转换
author: fatkun
type: post
date: 2010-09-15T13:48:25+00:00
url: /2010/09/transient-persistent-detached.html
duoshuo_thread_id:
  - 6300408770228912898
categories:
  - J2EE
tags:
  - hibernate

---
transient、persistent、detached状态关系图如下：
![系统学习hibernate之三：transient、persistent、detached状态][1] 
1、transient状态的特征：
* 在数据库中没有与之匹配的数据
* 没有纳入session的管理
2、persistent状态的特征：
* persistent状态的对象在数据库中有与之匹配的数据
* 纳入了session的管理
* 在清理缓存（脏数据检查）的时候,会和数据库同步
3、detached状态的特征：
* 在数据库中有与之匹配的数据
* 没有纳入session的管理
PS：了解这几种状态对深入使用hibernate有比较大的意义，开发过程中减少很多不必要的错误。
来源：[系统学习hibernate之三：transient、persistent、detached状态][2]{#ctl04_TitleUrl}

 [1]: http://img.ddvip.com/2008_10_10/1223608862_ddvip_5325.png
 [2]: http://www.cnblogs.com/sunwei2012/archive/2010/01/02/1637967.html