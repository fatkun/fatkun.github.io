---
title: Extjs FormPanel.getForm().getValues()对下拉框(Combobox)取值的问题
author: fatkun
type: post
date: 2011-06-27T05:36:01+00:00
url: /2011/06/formpanel-get-combobox-value.html
duoshuo_thread_id:
  - 6300408818958336769
categories:
  - 网页前端
tags:
  - Combobox
  - extjs
  - getValues

---
## 遇到的问题

我使用的是Extjs3.3  
在FormPanel中，可以通过 FormPanel.getForm().getValues()取得这个FormPanel下的所有值。  
但是，在取下拉框值时，得到的是显示名称（displayValue），而不是真正的值（value）
## 解决方法

原因是没有在下拉框指定hiddenName，指定hiddenName 和 name的值一样就可以了。
<span style="color: #ff0000;">2011-8-30update : 用FormPanel.getForm().getFieldValues()可以不用设置hiddenName。</span>