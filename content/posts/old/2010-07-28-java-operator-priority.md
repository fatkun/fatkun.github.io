---
title: Java运算符优先级(表格)
author: fatkun
type: post
date: 2010-07-28T14:45:18+00:00
url: /2010/07/java-operator-priority.html
views:
  - 39
duoshuo_thread_id:
  - 6300408757885076225
categories:
  - J2EE
tags:
  - java基础
  - Thinking in Java 读书笔记

---
Java运算符优先级参考图表
本文来源 <http://blog.csdn.net/xiaoli_feng/archive/2009/09/18/4567184.aspx>
<table border="1" cellspacing="0" cellpadding="0">  <tr>    <td width="73" valign="top">      <p align="left">        优先级      </p>    </td>
    <td width="462" valign="top">      <p align="left">        运算符      </p>    </td>
    <td width="85" valign="top">      <p align="left">        结合性      </p>    </td>  </tr>
  <tr>    <td width="73" valign="top">      <p align="left">        1      </p>    </td>
    <td width="462" valign="top">      <p align="left">        () [] .      </p>    </td>
    <td width="85" valign="top">      <p align="left">        从左到右      </p>    </td>  </tr>
  <tr>    <td width="73" valign="top">      <p align="left">        2      </p>    </td>
    <td width="462" valign="top">      <p align="left">        ! +(正)  -(负) ~ ++ &#8212;      </p>    </td>
    <td width="85" valign="top">      <p align="left">        从右向左      </p>    </td>  </tr>
  <tr>    <td width="73" valign="top">      <p align="left">        3      </p>    </td>
    <td width="462" valign="top">      <p align="left">        * / %      </p>    </td>
    <td width="85" valign="top">      <p align="left">        从左向右      </p>    </td>  </tr>
  <tr>    <td width="73" valign="top">      <p align="left">        4      </p>    </td>
    <td width="462" valign="top">      <p align="left">        +(加) -(减)      </p>    </td>
    <td width="85" valign="top">      <p align="left">        从左向右      </p>    </td>  </tr>
  <tr>    <td width="73" valign="top">      <p align="left">        5      </p>    </td>
    <td width="462" valign="top">      <p align="left">        << >> >>>      </p>    </td>
    <td width="85" valign="top">      <p align="left">        从左向右      </p>    </td>  </tr>
  <tr>    <td width="73" valign="top">      <p align="left">        6      </p>    </td>
    <td width="462" valign="top">      <p align="left">        < <= > >= instanceof      </p>    </td>
    <td width="85" valign="top">      <p align="left">        从左向右      </p>    </td>  </tr>
  <tr>    <td width="73" valign="top">      <p align="left">        7      </p>    </td>
    <td width="462" valign="top">      <p align="left">        ==   !=      </p>    </td>
    <td width="85" valign="top">      <p align="left">        从左向右      </p>    </td>  </tr>
  <tr>    <td width="73" valign="top">      <p align="left">        8      </p>    </td>
    <td width="462" valign="top">      <p align="left">        &(按位与)      </p>    </td>
    <td width="85" valign="top">      <p align="left">        从左向右      </p>    </td>  </tr>
  <tr>    <td width="73" valign="top">      <p align="left">        9      </p>    </td>
    <td width="462" valign="top">      <p align="left">        ^      </p>    </td>
    <td width="85" valign="top">      <p align="left">        从左向右      </p>    </td>  </tr>
  <tr>    <td width="73" valign="top">      <p align="left">        10      </p>    </td>
    <td width="462" valign="top">      <p align="left">        |      </p>    </td>
    <td width="85" valign="top">      <p align="left">        从左向右      </p>    </td>  </tr>
  <tr>    <td width="73" valign="top">      <p align="left">        11      </p>    </td>
    <td width="462" valign="top">      <p align="left">        &&      </p>    </td>
    <td width="85" valign="top">      <p align="left">        从左向右      </p>    </td>  </tr>
  <tr>    <td width="73" valign="top">      <p align="left">        12      </p>    </td>
    <td width="462" valign="top">      <p align="left">        ||      </p>    </td>
    <td width="85" valign="top">      <p align="left">        从左向右      </p>    </td>  </tr>
  <tr>    <td width="73" valign="top">      <p align="left">        13      </p>    </td>
    <td width="462" valign="top">      <p align="left">        ?:      </p>    </td>
    <td width="85" valign="top">      <p align="left">        从右向左      </p>    </td>  </tr>
  <tr>    <td width="73" valign="top">      <p align="left">        14      </p>    </td>
    <td width="462" valign="top">      <p align="left">        = += -= *= /= %= &= |= ^=  ~=  <<= >>= >>>=      </p>    </td>
    <td width="85">      <p align="left">        从右向左      </p>    </td>  </tr></table>
说明：
1、 该表中优先级按照从高到低的顺序书写，也就是优先级为1的优先级最高，优先级14的优先级最低。
2、 结合性是指运算符结合的顺序，通常都是从左到右。从右向左的运算符最典型的就是负号，例如3+-4，则意义为3加-4，符号首先和运算符右侧的内容结合。
3、 instanceof作用是判断对象是否为某个类或接口类型。
4、 注意区分正负号和加减号，以及按位与和逻辑与的区别
其实在实际的开发中，不需要去记忆运算符的优先级别，也不要刻意的使用运算符的优先级别，对于不清楚优先级的地方使用小括号去进行替代，示例代码：
int m = 12;
int n = m << 1 + 2;
int n = m << (1 + 2); //这样更直观
这样书写代码，更方便编写代码，也便于代码的阅读和维护。