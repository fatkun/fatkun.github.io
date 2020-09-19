---
title: '解决M2Crypto报错ImportError: DLL load failed'
author: fatkun
type: post
date: 2012-12-17T06:13:22+00:00
url: /2012/12/m2crypto-install-error.html
duoshuo_thread_id:
  - 6300409441476936450
categories:
  - 未分类

---
## 提示这个错误

>>> import M2Crypto  
Traceback (most recent call last):  
File &#8220;<stdin>&#8220;, line 1, in <module>  
File &#8220;C:\PYTHON26\lib\site-packages\M2Crypto\_\_init\__.py&#8221;, line 22, in <module >  
import __m2crypto  
ImportError: DLL load failed: %1 不是有效的 Win32 应用程序。
## 解决方法

需要安装win32OpenSSL
http://slproweb.com/products/Win32OpenSSL.html