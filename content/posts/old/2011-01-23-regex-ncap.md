---
title: 正则表达式-非捕获组
author: fatkun
type: post
date: 2011-01-23T05:59:32+00:00
url: /2011/01/regex-ncap.html
duoshuo_thread_id:
  - 6300408796741108481
categories:
  - 网页前端

---
&nbsp;
## 非捕获组 (?:xxx)

<p style="font-family: Verdana, Arial, Helvetica, sans-serif, SimSun, 'MS Gothic', 'New Gulim'; font-size: 12px; line-height: 16px; ">  使用 (?: ) 包含其他表达式，可使被包含的表达式组成一个整体，在被修饰匹配次数时，可作为整体被修饰。</p>
<p style="font-family: Verdana, Arial, Helvetica, sans-serif, SimSun, 'MS Gothic', 'New Gulim'; font-size: 12px; line-height: 16px; ">  &nbsp;</p>
## 说明

<p style="font-family: Verdana, Arial, Helvetica, sans-serif, SimSun, 'MS Gothic', 'New Gulim'; font-size: 12px; line-height: 16px; ">  与普通分组不同的是，非捕获组不记录所匹配的内容，比普通分组更节约内存资源。</p>
<p style="font-family: Verdana, Arial, Helvetica, sans-serif, SimSun, 'MS Gothic', 'New Gulim'; font-size: 12px; line-height: 16px; ">  通过格式 (?ismg-ismg:xxx) 可对匹配模式进行修改，修改后的模式只对当前非捕获组内部起作用。</p>
## 举例

匹配一个URL链接,当中可以有端口或者没有端口号,如下
> url1 = "http://fatkun.com:8080"
> url2 = "http://fatkun.com"
如果有端口号需要匹配端口号,如果没则忽略它
正则表达式:\/{0,2}([0-9.\-A-Za-z]+)(?::(\d+))?$
url1匹配结果
> $0 =&nbsp;//fatkun.com
> $1 =&nbsp;fatkun.com
> $2 = 8080
> url2匹配的$2结果为空
## 解释

\/{0,2} 匹配//
([0-9.\-A-Za-z]+) 匹配fatkun.com
(?::(\d+))? 注意这里的(?:),这里是非捕获分组,判断是不是有:开头的数字,把匹配的数字取出
&nbsp;