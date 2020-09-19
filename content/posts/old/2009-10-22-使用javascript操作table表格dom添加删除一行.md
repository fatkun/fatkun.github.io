---
title: 使用javascript操作table(表格)Dom,添加/删除一行
author: fatkun
type: post
date: 2009-10-22T19:09:32+00:00
url: /2009/10/使用javascript操作table表格dom添加删除一行.html
views:
  - 24
duoshuo_thread_id:
  - 6300408694047769345
categories:
  - 网页前端
tags:
  - JSP实验

---
看代码吧&#8230;  
主要三个方法是insertRow和insertCell，deleteRow
<!--more-->

  
看代码吧&#8230;
<pre class="brush:js;">&lt;!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd"&gt;&lt;html&gt;&lt;head&gt;&lt;meta http-equiv="Content-Type" content="text/html; charset=gb2312"&gt;&lt;title&gt;无标题文档&lt;/title&gt;&lt;script type="text/javascript" language="javascript"&gt;	function addCell(){		oRow = document.getElementById("mytable").insertRow();//插入行		for (var k=0;k&lt;4;k++){		var oCell = oRow.insertCell();//插入单元格		if (k==0)			oCell.innerHTML = "&lt;input type='checkbox'/&gt;";		else			oCell.innerHTML = document.getElementById("mytable").rows.length;		}	}	function delRow(){		for (var k=0; k&lt;document.getElementById("mytable").rows.length; k++){			var arow = document.getElementById("mytable").rows(k);//得到每一行			var cb = arow.getElementsByTagName("input");			if (cb[0].checked){				document.getElementById("mytable").deleteRow(k);//删除第k行				k--;			}		}	}		function selectAll(){		for (var k=0; k&lt;document.getElementById("mytable").rows.length; k++){			var arow = document.getElementById("mytable").rows(k);			var cb = arow.getElementsByTagName("input");			if (!cb[0].checked){				cb[0].checked = true;			}		}	}	function unSelectAll(){		for (var k=0; k&lt;document.getElementById("mytable").rows.length; k++){			var arow = document.getElementById("mytable").rows(k);			var cb = arow.getElementsByTagName("input");			if (cb[0].checked){				cb[0].checked = false;			}		}	}&lt;/script&gt;&lt;/head&gt;&lt;body&gt;	&lt;input type="button" onClick="addCell()" value="添加"/&gt;	&lt;input type="button" onClick="delRow()" value="删除"/&gt;    &lt;input type="button" onClick="selectAll()" value="全选"&gt;    &lt;input type="button" onClick="unSelectAll()" value="全不选"&gt;    &lt;table id="mytable"&gt;&lt;/table&gt;&lt;/body&gt;&lt;/html&gt;</pre>