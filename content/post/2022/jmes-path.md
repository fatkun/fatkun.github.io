---
title: "JMES Path - 提取json内容"
date: 2022-08-30T10:38:28+08:00
tags: []
categories: []
author: "fatkun"
draft: false
---



JMESPath有很多方法，可以提取json内容

例如 keys(@) 可以把所有key取出来

```json
{
  "xx": {}, 
  "bb": {}
}
```

这个例子的结果是

```json
[
  "xx",
  "bb"
]
```



# 参考

https://jmespath.org/tutorial.html

https://jmespath.org/specification.html#functions