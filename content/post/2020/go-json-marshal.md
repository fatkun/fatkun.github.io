---
title: "Go Json Marshal字段不输出"
date: 2020-10-30T14:15:06+08:00
tags: [go json]
categories: [go]
author: "fatkun"
draft: false
---

## 问题

json.Marshal默认不输出非导出的字段

```go
type Test struct {
	Total int    `json:"total"`
	item  string `json:"item"`
}

func main() {
	resp := Test{
		Total: 1,
		item:  "aa",
	}
	body, err := json.Marshal(resp)
	fmt.Printf("body=%v, err=%v \n", string(body), err) // 输出 body={"total":1}, err=<nil>
}
```

## 解决方式

把字段改成大写字母开头