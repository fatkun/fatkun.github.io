---
title: 使用jsduck生成extjs3.x的代码
author: fatkun
type: post
date: 2012-12-18T15:54:54+00:00
url: /2012/12/jsduck-generate-extjs3-api.html
duoshuo_thread_id:
  - 6300409441527268097
categories:
  - 网页前端
tags:
  - extjs

---
直接按说明的命令会出错  
Error: Error while parsing /root/PROJECTS/foundation-ui/src/main/webapp/scripts/ext/src/ext-core/src/adapter/ext-base-begin.js: Line 18: Unexpected end of input
## 解决方法

`jsduck ext-3.4.0/src/{core,data,dd,direct,ext-core/src/core,ext-core/src/data,ext-core/src/util,state,widgets} --output api`
来源：http://www.sencha.com/forum/showthread.php?151739-JSDuck-the-tool-for-documenting-your-Ext-JS-apps&p=870848&viewfull=1#post870848