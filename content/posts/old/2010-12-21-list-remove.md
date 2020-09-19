---
title: List中的remove使用注意
author: fatkun
type: post
date: 2010-12-21T05:09:50+00:00
url: /2010/12/list-remove.html
duoshuo_thread_id:
  - 6300408788885177090
categories:
  - J2EE
tags:
  - java基础
  - list

---
先来看API是怎样写的。
> boolean **remove**(<a title="java.lang 中的类">Object</a> o)
> :   从此列表中移除第一次出现的指定元素（如果存在）（可选操作）。如果列表不包含元素，则不更改列表。更确切地讲，移除满足 <tt>(o==null ? get(i)==null : o.equals(get(i)))</tt> 的最低索引 <tt>i</tt> 的元素（如果存在这样的元素）。如果此列表已包含指定元素（或者此列表由于调用而发生更改），则返回 <tt>true</tt>。 

可以看到是用o.equals来判断是否删除的，在一般情况下使用都没有问题。但我有一次犯了一个错误。
有一个List<子类> list，我用 list.remve(父类对象);这样很明显是不行的，equals不了，所以就删除不了。
解决方法：1，是remove同一类对象
2，在父类覆盖equals方法，用instanceof来判断是不是子类，然后判断相等。
方法2较为麻烦。还是建议方法1。