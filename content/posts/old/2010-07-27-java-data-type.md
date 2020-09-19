---
title: Java的主要类型及它们的取值范围
author: fatkun
type: post
date: 2010-07-26T17:11:29+00:00
url: /2010/07/java-data-type.html
views:
  - 2
duoshuo_thread_id:
  - 6300408751279047425
categories:
  - J2EE
tags:
  - byte取值范围
  - java基础
  - 数据类型

---
## Java的主要类型

<table border="0" cellspacing="0" cellpadding="0" width="651">  <tr>    <td width="75">      <p align="center">        <strong>主类型 </strong>      </p>    </td>
    <td width="139">      <p align="center">        <strong>默认值 </strong>      </p>    </td>
    <td width="87">      <p align="center">        <strong>大小（位）</strong>      </p>    </td>
    <td width="104">      <p align="center">        <strong>最小值</strong>      </p>    </td>
    <td width="149">      <p align="center">        <strong>最大值</strong>      </p>    </td>
    <td width="97">      <p align="center">        <strong>封装器类型</strong>      </p>    </td>  </tr>
  <tr>    <td width="75">      <p align="center">        boolean      </p>    </td>
    <td width="139">      <p align="center">        false      </p>    </td>
    <td width="87">      <p align="center">        1      </p>    </td>
    <td width="104">      <p align="center">        &#8211;      </p>    </td>
    <td width="149">      <p align="center">        &#8211;      </p>    </td>
    <td width="97">      <p align="center">        Boolean      </p>    </td>  </tr>
  <tr>    <td width="75">      <p align="center">        char      </p>    </td>
    <td width="139">      <p align="center">        &#8216;\u0000&#8242;(null)      </p>    </td>
    <td width="87">      <p align="center">        16      </p>    </td>
    <td width="104">      <p align="center">        Unicode 0      </p>    </td>
    <td width="149">      <p align="center">        Unicode 2^16-1      </p>    </td>
    <td width="97">      <p align="center">        Character      </p>    </td>  </tr>
  <tr>    <td width="75">      <p align="center">        byte      </p>    </td>
    <td width="139">      <p align="center">        (byte)0      </p>    </td>
    <td width="87">      <p align="center">        8      </p>    </td>
    <td width="104">      <p align="center">        -128      </p>    </td>
    <td width="149">      <p align="center">        127      </p>    </td>
    <td width="97">      <p align="center">        Byte      </p>    </td>  </tr>
  <tr>    <td width="75">      <p align="center">        short      </p>    </td>
    <td width="139">      <p align="center">        (short)0      </p>    </td>
    <td width="87">      <p align="center">        16      </p>    </td>
    <td width="104">      <p align="center">        -2^15      </p>    </td>
    <td width="149">      <p align="center">        +2^15-1      </p>    </td>
    <td width="97">      <p align="center">        Short      </p>    </td>  </tr>
  <tr>    <td width="75">      <p align="center">        int      </p>    </td>
    <td width="139">      <p align="center">      </p>    </td>
    <td width="87">      <p align="center">        32      </p>    </td>
    <td width="104">      <p align="center">        -2^31      </p>    </td>
    <td width="149">      <p align="center">        +2^31-1      </p>    </td>
    <td width="97">      <p align="center">        Integer      </p>    </td>  </tr>
  <tr>    <td width="75">      <p align="center">        long      </p>    </td>
    <td width="139">      <p align="center">        0L      </p>    </td>
    <td width="87">      <p align="center">        64      </p>    </td>
    <td width="104">      <p align="center">        -2^63      </p>    </td>
    <td width="149">      <p align="center">        -2^63-1      </p>    </td>
    <td width="97">      <p align="center">        Long      </p>    </td>  </tr>
  <tr>    <td width="75">      <p align="center">        float      </p>    </td>
    <td width="139">      <p align="center">        0.0f      </p>    </td>
    <td width="87">      <p align="center">        32      </p>    </td>
    <td width="104">      <p align="center">        IEEE754      </p>    </td>
    <td width="149">      <p align="center">        IEEE754      </p>    </td>
    <td width="97">      <p align="center">        Float      </p>    </td>  </tr>
  <tr>    <td width="75">      <p align="center">        double      </p>    </td>
    <td width="139">      <p align="center">        0.0d      </p>    </td>
    <td width="87">      <p align="center">        64      </p>    </td>
    <td width="104">      <p align="center">        IEEE754      </p>    </td>
    <td width="149">      <p align="center">        IEEE754      </p>    </td>
    <td width="97">      <p align="center">        Double      </p>    </td>  </tr></table>
对于float:共32个bits，Bit 31是MSB（Most Significant Bit），Bit 0是LSB（Least Significant Bit），则  
Bit 31是符号位，接下来的8位是指数位，指数位被视为一个无符号的数，它与127的差就是以2为底的指数的部分。 最后的23位是小数部分。
## 在byte(8位)中的取值范围为-128 到 127的问题

在电脑用是使用补码来存储数字的，我搜索了很多，还不是很明白。以前的反码之类的没认真学习。。。
因为 -0 和 +0 在补码中是不一样的，把 1000 0000 作为-128(补)  ，127(补)=0111 1111，0(补) = 0000 0000， -127(补) = 1111 1111， -128在9位中表示应该为 1 1000 0000，取低八位就变成了  1000 0000
摘录一篇文章如下，更详细可以点链接查看
<http://topic.csdn.net/t/20050828/10/4235813.html>
在机器中  
负数的补码是这样算的:  
先将该负数取绝对值,再用二进制表示出这个绝对值  
对该二进制数进行取反加一操作就得到负数的补码了  
-128   绝对值是   128  
128的二进制表示为:  
1000   0000  
取反  
0111   1111  
加1  
1000   0000  
这就是-128的补码