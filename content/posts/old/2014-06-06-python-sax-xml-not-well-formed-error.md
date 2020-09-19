---
title: python sax xml解析报错not well-formed error
author: fatkun
type: post
date: 2014-06-06T08:51:43+00:00
url: /2014/06/python-sax-xml-not-well-formed-error.html
duoshuo_thread_id:
  - 6300410318350713602
categories:
  - 未分类

---
可能的原因是有特殊的字符，或者xml编码不正确。
我用notepad++安装xml tool插件，检查xml格式发现错误
可能用命令 sed -i -e &#8216;s/[^[:print:]]/ /g&#8217; 文件名 替换掉不可见字符也可以。
## 参考

http://stackoverflow.com/questions/11964023/python-sax-not-well-formed-error  
http://www.megasolutions.net/python/Please-help!!-SAXParseException_not-well-formed-(invalid-token)-43696.aspx