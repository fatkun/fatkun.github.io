---
title: "使用Frida-il2cpp-bridge"
date: 2025-07-31T10:55:33+08:00
tags: [逆向]
categories: [逆向]
author: "fatkun"
draft: false
typora-root-url: ./..\..\..\static
---

# 说明

代码仓库： https://github.com/vfsfitvnm/frida-il2cpp-bridge

这是一个用来hook Il2Cpp 程序的模块，可以用它dump class，跟踪代码执行，覆盖方法等

# 安装

参考 [wiki的安装说明](https://github.com/vfsfitvnm/frida-il2cpp-bridge/wiki/Installation) 

新建一个 index.ts

```
import "frida-il2cpp-bridge";

Il2Cpp.perform(() => {
    // code here
    console.log(Il2Cpp.unityVersion);
});
```

新建一个 packages.json

```json
{
  "name": "playground",
  "main": "index.ts",
  "version": "1.0.0",
  "private": true,
  "type": "module",
  "scripts": {
    "build": "frida-compile -o _.js -w index.ts",
    "attach": "run() { frida -U \"$1\" -l _.js --runtime=v8; }; run",
    "spawn": "run() { frida -U -f \"$1\" -l _.js --no-pause --runtime=v8; }; run",
    "app0-spawn": "npm run spawn com.example.application0",
    "app1": "npm run \"Application1 Name\"",
    "app1-spawn": "npm run spawn com.example.application1"
  },
  "devDependencies": {
    "@types/frida-gum": "^18.3.1",
    "frida-compile": "^16.2.2",
    "frida-il2cpp-bridge": "*"
  }
}
```

新建一个 tsconfig.json

```
{
  "compilerOptions": {
    "target": "esnext",
    "lib": [ "es2022" ],
    "experimentalDecorators": true,
    "module": "esnext",
    "allowJs": false,
    "noEmit": false,
    "esModuleInterop": false,
    "moduleResolution": "nodenext",
    "strict": true,
    "sourceMap": true
  },
  "files": [ "index.ts" ]
}
```

安装

```
npm install --save-dev frida-il2cpp-bridge
```

# 执行

```
# 由ts代码构建js代码，里面有-w参数，如果ts变更会重新编译js
npm run build
```

由于我是在windows下执行，packages.json 需要修改一下运行命令

```
"attach": "run() { frida -U \"$1\" -l _.js --runtime=v8; }; run",
```

改为

```
"attach": "frida 进程名称.exe -l _.js",
```

然后执行

```
npm run attach
```

# 使用例子

可以看官方的wiki https://github.com/vfsfitvnm/frida-il2cpp-bridge/wiki/Snippets



## 调用堆栈

看这里的[讨论](https://github.com/vfsfitvnm/frida-il2cpp-bridge/issues/10#issuecomment-1680834010)

方法一（受限frida默认只有16个backtrace，信息很少）

```ts
import "frida-il2cpp-bridge";
Il2Cpp.perform(() => {
      const UnityWebRequest = Il2Cpp.domain.assembly("UnityEngine").image.class("UnityEngine.Networking.UnityWebRequest");
        
      Il2Cpp.backtrace().methods(UnityWebRequest.method("Send")).and().attach();
})
```

方法二（更详细）

```ts
import "frida-il2cpp-bridge";
Il2Cpp.perform(() => {
    const get_StackTrace = Il2Cpp.corlib.class("System.Environment").method("get_StackTrace");
    
    const UnityWebRequest = Il2Cpp.domain.assembly("UnityEngine").image.class("UnityEngine.Networking.UnityWebRequest");
    // 重写 SendWebRequest 方法的实现
    UnityWebRequest.method("SendWebRequest").implementation = function (this: Il2Cpp.Object) {
        console.log("TRACE!!!");
        console.log(get_StackTrace.invoke());
        // 调用原始方法
        return this.method("SendWebRequest").invoke();
    };
})
```

## 跟踪方法（Trace）

``` ts
import "frida-il2cpp-bridge";
Il2Cpp.perform(() => {
      const UnityWebRequest = Il2Cpp.domain.assembly("UnityEngine").image.class("UnityEngine.Networking.UnityWebRequest");
        
      Il2Cpp.trace(true).classes(UnityWebRequest).and().attach();
})
```

