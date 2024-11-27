---
title: "某枝网wasm签名验证逆向"
date: 2024-11-27T22:36:34+08:00
tags: [逆向]
categories: [逆向]
author: "fatkun"
draft: false
typora-root-url: ./..\..\..\static
---

# 声明

只用于学习，不可用于非法用途，参考 [分析视频](https://www.bilibili.com/video/BV1eEyoYAEcM/?vd_source=cae69f5f7f437d5b10d6bfe1a9306e80) 学习。

# 概要

某枝网的加密算法是在wasm上实现的，由于直接分析wasm文件比较困难，还是采用直接调用wasm文件的方式。

# 分析

网站核心请求会调用wasm生成header信息，其中带有签名。调用wasm的代码在`/sitecdn/platforms/**tv/js/vendor_w_dceabe2b.js`里面。

<img src="/img/crack_gdtv/image-20241127225618140.png" alt="image-20241127225618140" style="zoom:60%;" />

代码里面使用webpack打包，不太熟悉怎样单独抽取出来，所以不太好在浏览器提取出来验证，只好手工抽取代码出来验证。

代码入口在B.a方法，这里会生成header信息。代码抽取的时候，注意有一些局部变量也要提取出来，而且有些变量的赋值在后面。

```javascript
        B.a = function(A, g, I, B, Q, C) {
            try {
                var E = L(A, w.__wbindgen_export_0, w.__wbindgen_export_1)
                  , D = h
                  , i = L(g, w.__wbindgen_export_0, w.__wbindgen_export_1)
                  , o = h
                  , Y = L(I, w.__wbindgen_export_0, w.__wbindgen_export_1)
                  , N = h
                  , J = L(B, w.__wbindgen_export_0, w.__wbindgen_export_1)
                  , k = h
                  , K = L(Q, w.__wbindgen_export_0, w.__wbindgen_export_1)
                  , y = h;
                return G(w.a(E, D, i, o, Y, N, J, k, K, y, function(A) {
                    if (1 == H)
                        throw new Error("out of js stack");
                    return M[--H] = A,
                    H
                }(C)))
            } finally {
                M[H++] = void 0
            }
        }
```

代码里面用到wasm，所以要读取并且执行方法。WebAssembly使用`WebAssembly.instantiate(wasmBuffer, importObject)`初始化，第一个参数是wasm的内容，第二个参数是为了可以让wasm获取浏览器的一些对象，并且执行一些动态js代码。

```js
const dataUrl = "data:application/wasm;base64,AGFzb省略...";

function O(A, g) {
  return w = A.exports,
  //r.__wbindgen_wasm_module = g,
  c = null,
  J = null,
  w
}

const url = "https://****-api.**tv.cn/api/tvColumn/v1/tvColumn/43";
fetch(dataUrl).then(response => {
    return response.arrayBuffer();
}).then(wasmBuffer => {
    delete global; // 里面会检测global
    WebAssembly.instantiate(wasmBuffer, importObject).then((obj) => {
        O(obj.instance, obj.module);
        var header = B.a(
            "GET",
            url,
            "WEB_aa55cd50-3be4-11ef-2323-c127ac36c210",
            "WEB_PC",
            "",
            undefined
          );
          console.log(JSON.stringify(Object.fromEntries(header.entries())));
    })

})
```

wasm除了生成header外，还会做额外的环境验证，确认是浏览器执行的，如果环境验证不正确，会报错unreachable，错误信息很有限，补环境非常困难。

## 补环境

由于wasm不能直接操控浏览器，都是通过ImportObject来通信的，wasm会通过ImportObject获取一些对象。

### 第一种：获取标准对象，如window, document, location等

验证是否正确，也有可能验证对象的原型，使用proxy的方式，能发现哪些对象被调用了。但是像原型判断（typeof）这种判断暂时不清楚怎么发现，我目前只能从代码判断。

```js
function myProxy(obj,name){
    return new Proxy(obj,{
        get(target, propKey, receiver)
        {
            let temp =Reflect.get(target,propKey,receiver);
            if  (typeof temp == 'object'){
                temp=myProxy(temp,name+'=>'+propKey.toString())
            }
            console.log(`${name}->get ${propKey.toString()}  return ->${temp}`)
            return temp;
        },
        set(target, propKey, value, receiver)
        {
            let temp = Reflect.set(target,propKey,value);
            console.log(`${name}->set ${propKey.toString()}  value ->${value}`)
            return temp;
        }
    })
}

window = myProxy(global, 'window');
XMLHttpRequest = myProxy({}, 'XMLHttpRequest');
document = myProxy({}, 'document');
```

### 第二种：检测nodejs存在的，但浏览器不存在的

例如像global、process、require等，在使用完之后可以delete掉这些对象

### 第三种：wasm执行检测js

代码中是`g.wbg.__wbg_newnoargs_xxxx`把js内容存储到map里，然后再调用`g.wbg.__wbg_call_xxxx`执行js函数，执行完之后和预期的结果对比，结果有时候是true，有时候是false，或者是具体的值，这些里面也有检测代码。

执行的代码是混淆过的，可以用一些反混淆的工具或者AI把代码还原。

这里的技巧是要阅读清楚代码逻辑（还好代码比较短），看看做了哪些检测，有针对性的补全环境。其中有些恶心的是里面判断如果不是nodejs，会执行一些nodejs比较慢，但浏览器很快的代码，其中有一个填充数组的，会导致nodejs内存溢出。

如果不确定哪个条件检查不通过，还有个技巧是判断代码内容，替换回还原后的内容，然后进行单步调试。如果实在不清楚怎么绕过，就直接把要执行的代码改了，跳过检测部分。

# 尝试使用python调用

试了几个lib使用python来调用js代码，但是用起来不理想。首先global对象是nodejs独有的，那就要自己模拟window对象了。其次有些函数是浏览器/nodejs实现的（如fetch、atob等），哪些lib都没有实现这些，所以会执行失败。所以还是直接调用node命令执行，或者使用nodejs实现一个httpserver来给python调用了。



# 总结

难点主要在于补环境，wasm里面有不少检测点，后面也可能会更新。而且因为环境的问题，出错也没有具体错误信息。不过好在检测的手段主要都是在ImportObject的方法里面，虽然增加了一些隐藏的js，但是还是可以获取到分析的。尝试使用一个补环境框架，也不是用上了就行的。



# 参考

[nodejs项目，已失效](https://github.com/claviering/gdtv)

[某视频解析网站js逆向分析——学会wasm文件类型逆向](https://www.52pojie.cn/thread-1900845-1-1.html)
