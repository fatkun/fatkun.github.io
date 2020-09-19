---
title: Extjs renderer参数
author: fatkun
type: post
date: 2011-05-31T09:05:24+00:00
url: /2011/05/extjs-renderer.html
duoshuo_thread_id:
  - 6300408814021640961
categories:
  - 网页前端
tags:
  - extjs
  - renderer

---
function myRenderer(value, cellmeta, record, rowIndex, columnIndex, store) {  
[&#8230;]  
}  
看上面的myRenderer，依次最多有6个参数  
1 value： 当前单元格的值  
2 cellmeta里保存的是cellId单元格id，id不知道是干啥的，似乎是列号，css是这个单元格的css样式。（没看懂？？？）  
3 record：这行的所有数据，可以通过record.data[&#8220;id&#8221;]获得本行中“id”字段的值。  
4 rowIndex：行号，不是从头往下数的意思，而是计算了分页以后的结果。  
5 columnIndex：列号  
6 store：整个grid关联的数据
来源：<http://blog.sina.com.cn/s/blog_5140a6a50100bfat.html>  
关于该store的访问，可以看<http://blog.chinaunix.net/u1/37472/showart_2190023.html>