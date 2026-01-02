---
title: "golang逆向，还原符号表"
date: 2026-01-02T00:22:01+08:00
tags: [golang, 逆向]
categories: [逆向]
author: "fatkun"
draft: false
typora-root-url: ./..\..\..\static
---

查看是否加了upx壳，可以下载upx，使用`upx -d`解压。

使用 https://github.com/mandiant/GoReSym 导出符号
```bash
GoReSym.exe -t -d -p /path/to/input.exe > symbol.json
```

导出之后，把 https://github.com/mandiant/GoReSym/blob/master/IDAPython/goresym_rename.py 下载下来，然后用ida执行python脚本，选择刚才导出的json。
