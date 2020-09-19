---
title: Extjs3 EditorGridPanel的beforeedit事件参数
author: fatkun
type: post
date: 2011-06-02T02:21:37+00:00
url: /2011/06/extjs-editorgridpanel-beforeedit.html
duoshuo_thread_id:
  - 6300408814063584002
categories:
  - 网页前端
tags:
  - beforeedit
  - EditorGridPanel
  - extjs

---
## beforeedit : ( Object e )

只有一个事件(edit event)参数，但这个参数内容很丰富，可以满足很多需求。  
参数分别如下：  
grid &#8211; 表格本身  
record &#8211; 你要编辑的那一行记录  
field &#8211; 你编辑的列名  
value &#8211; 你编辑的值  
row &#8211; 行号  
column &#8211; 列号  
cancel &#8211; 设这个为true或者return false可以取消编辑（不显示那个编辑框）