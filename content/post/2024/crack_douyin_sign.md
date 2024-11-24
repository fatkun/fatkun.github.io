---
title: "逆向某音弹幕签名"
date: 2024-11-25T00:25:08+08:00
tags: [逆向]
categories: [逆向]
author: "fatkun"
draft: false
typora-root-url: ./..\..\..\static
---

# 概要

基于学习的目的，根据[这个视频](https://www.bilibili.com/video/BV149D9YPELn?vd_source=62d2cb1e3ff62f323aa467f88c49d589&spm_id_from=333.788.videopod.episodes)学习逆向某音弹幕签名。

# 步骤

## 断点调试跟踪代码入口

首先，打开一个直播间，在web控制台`Network`里面，找到websocket，这里可以获取ws链接。可以用[ws在线工具](https://wstool.js.org/)确认这个ws链接可以正常使用。

在`Network`里面，链接的右边有一个Initiator列，可以找到对应的代码。

![image-20241125004545702](/img/crack_douyin_sign/image-20241125004545702.png)

然后可以使用断点调试，找到对应的代码。

可以看到是调用_getSocketParams获取ws地址，主要是下面的`V(s, i);`方法获取签名。

```js
        ee._getSocketParams = e => {
            let {app_name: t, routeParams: n, pushServer: r, websocket_key: i} = e
              , o = J(e, ["app_name", "routeParams", "pushServer", "websocket_key"])
              , s = $($({
                app_name: t,
                version_code: a.ry,
                webcast_sdk_version: ee.VERSION,
                update_version_code: ee.VERSION,
                compress: "gzip"
            }, n), o)
              , c = V(s, i);
            return `${r}?${_($($({}, s), c))}`
        }
```

再来看`V(s, i);`这个方法

```js
        let V = (e, t=[]) => {
            var n, r, i;
            let o = "";
            for (let {param_name: r} of t)
                o += `,${r}=${null != (n = e[r]) ? n : ""}`;
            let a = X()(o.substring(1))
              , s = {};
            return window.byted_acrawler && (s = null == (r = null == window ? void 0 : window.byted_acrawler) ? void 0 : r.frontierSign({
                "X-MS-STUB": a
            })),
            {
                signature: null != (i = s["X-Bogus"]) ? i : ""
            }
        }
```

这里主要有几个值，o、a和s。

o是传入的一堆参数拼接成一个字符串，o=",live_id=1,aid=6383..."，o参数拼接里面有一个roomId，可以访问直播链接里面提取，在源码里面搜索roomId。

X()方法根据视频这里是一个MD5算法，怎么判断是MD5?可以断点进去，复制代码给AI分析，也可以用md5验证一下。那么相当于 a = MD5(o.substring(1))

s的取值主要是 `s = r.frontierSign({"X-MS-STUB": a})`, 鼠标移上去可以找到代码位置。

<img src="/img/crack_douyin_sign/image-20241125010326187.png" alt="image-20241125010326187" style="zoom:50%;" />

所有签名的代码都在webmssdk.es5.js里面了，我分析的版本是`1.0.0.53`

```js
        function _0x5c2014(_0x1fa689) {
            return w_0x5c3140('484e4f4a403f5243...', {
                get 0x0() {
                    return _0x5dd467;
                },
                get 0x1() {
                    return _0x34c70a;
                },
                0x2: arguments,
                0x3: _0x1fa689
            }, this);
        }
```

这里第一个参数是一个字符串，第二个是一个字典，里面的get表示是只读，0x0是一个方法，在某个地方会调用这里的方法，可以提前先对这些方法加一个断点，第三个是window。

可以把webmssdk.es5.js复制到本地，写一个html引用这个js

```html
<script src="./webmssdk.js"></script>
```

在js的最后调用加密方法

```
window.sign = _0x5c2014;
sign = window.sign({
    "X-MS-STUB": "b7d22ba3f49ffd02ef417b3c6b8b1ca2"
});
console.log(sign);
```

在浏览器打开HTML，在控制台获取签名，先用这个签名拼接ws地址，试一下这个地址是否正确。我测试在浏览器下是正确的，但是我们需要在nodejs或其他环境里面运行，厂商为了对抗会对浏览器进行一些检测。

## 补环境

复制一份js，尝试一下在nodejs里面是否可以运行，先使用jsdom补充一下基础环境，在js文件前面加入以下内容。

```js
const jsdom = require("jsdom");  // 引入 jsdom
const { JSDOM } = jsdom;  // 引出 JSDOM 类， 等同于 JSDOM = jsdom.JSDOM
const userAgent = 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36'
const resourceLoader = new jsdom.ResourceLoader({
    userAgent: userAgent
});
const dom = new JSDOM(`<!DOCTYPE html><p>Hello world</p>`, {
    url: "https://www.douyin.com/",
    referrer: "https://www.douyin.com/",
    resources: resourceLoader,
});
window = global
document = dom.window.document
Object.assign(global, {
    location: {
        hash: "",
        host: "www.douyin.com",
        hostname: "www.douyin.com",
        href: "https://www.douyin.com/",
        origin: "https://www.douyin.com/",
        pathname: "/",
        port: "",
        protocol: "https:",
        search: "",
        assign: function() {},
        reload: function() {},
        replace: function() {}
    },
    navigator: {
        appCodeName: "Mozilla",
        appName: "Netscape",
        appVersion: userAgent,
        cookieEnabled: true,
        deviceMemory: 8,
        doNotTrack: null,
        hardwareConcurrency: 4,
        language: "zh-CN",
        languages: ["zh-CN"],
        maxTouchPoints: 0,
        onLine: true,
        platform: "MacIntel",
        plugins: [],
        product: "Gecko",
        productSub: "20100101",
        userAgent: userAgent,
        vendor: "Google Inc.",
        vendorSub: "",
        webdriver: false

    }
})
```

执行`node sdk2.js`能够生成，但是使用ws验证签名是错误的，厂商还做了其他的验证。

怎么找出厂商做的检测呢？只能单步调试，对比nodejs和浏览器执行的差异，如果有差异，要看是哪里造成的。这一步肯定是很枯燥的，代码非常长，要一步步调试。这里我也没有仔细跟踪，按着视频的方法调试。

## 反混淆

里面的代码有些被混淆了，可以先反混淆。视频教的方法是看到代码总会跳转到前面几十行代码，能判断前面几十行是做混淆还原的，他写了一个脚本去调用nodejs还原字符串，再替换回文本。

我找了一个取巧的方法，使用[在线反混淆的网站](https://js-deobfuscator.vercel.app/)处理，注意在设置里面不要更改变量名称，不然不太好和原来的代码对应看。尝试执行一下，发现nodejs执行失败，提示缺少方法，发现是缺少了混淆的方法，补回去就正常了。

剩下的步骤就是断点执行对比nodejs的差异了，可以一个个方法的比较两边的返回值是否一致，在nodejs里面可以用`console.log()`输出，也可以采用断点调试的方式。

在vscode的终端里面，在右边加号那里，添加一个JavaScript调试终端，然后在代码断点，执行node sdk2.js就可以断点调试了。

跟着视频分析是这里面做了一些检测

```js
        function _0x34c70a(_0xf6b3d0, _0x289075, _0x2c48ed) {
            return {
                "X-Bogus": _0x1633f2(1, _0x462335.initialized, _0xf6b3d0, null, _0x2c48ed)
            };
        }
```

```js
        function _0x1633f2(_0x48f290, _0x504655, _0x4fa808, _0x1a5c57, _0x3a4737) {
            _0x5863d1();
            _0x26d461(); // 这个方法有检测
```

```js
        function _0x26d461() {
            var _0x5e9ee6 = false;
            var _0x499168 = 0;
            // try {
            //     if (document && document.createEvent) {
            //         document.createEvent("TouchEvent");
            //         _0x5e9ee6 = true;
            //     }
            // } catch (_0x4b2baa) {}
            // 修改
            console.log("_0x5e9ee6", _0x5e9ee6);
```

我注释的这个地方，在浏览器上`_0x5e9ee6`返回false，但在nodejs返回true，所以保持和浏览器一致，直接把它注释了。改完这里可以试一下生成签名是否正确，可惜是还是不正确，继续找。

```js
        function _0x1633f2(_0x48f290, _0x504655, _0x4fa808, _0x1a5c57, _0x3a4737) {
            _0x5863d1();
            _0x26d461();
            if (_0x1a5c57 !== undefined && _0x1a5c57 !== "") {
                _0x1a5c57 = "";
            }
            var _0x21ca02 = _0x5dd467(_0x1a5c57);
            if (!_0x3a4737) {
                _0x3a4737 = "00000000000000000000000000000000";
            }
            var _0x1fb174 = new ArrayBuffer(9);
            var _0x1ffaa7 = new Uint8Array(_0x1fb174);
            var _0xeefda2 = _0x48f290 << 6 | 0 | _0x504655 << 5 | (Math.floor(Math.random() * 100) & 1) << 4 | 0;
            _0x6caf.bogusIndex++;
            
            _0x6caf.envcode = 513; // 修改
```

还有一个地方是`_0x6caf`这个变量，我不清楚视频作者是怎么定位到这里不一致的，不过可以从这个方法的返回值对比可以发现，返回的第二个参数是一个bytes数组对不上。对不上的话只能在这个方法里面断点对比那个对象不一样了。

我这里看到后面的计算主要是依赖这个envcode，我从浏览器的值复制了过来，也不知道后面会不会变。`_0x6caf`这个变量是一个局部变量，在哪个地方变更了这个变量的值，nodejs执行的值和浏览器的不一样。

最终，使用ws在线测试服务，验证生成的签名是有效的。

![image-20241125015103917](/img/crack_douyin_sign/image-20241125015103917.png)

# 总结

逆向非常的枯燥，如果没有跟着视频一步步操作，需要断点调试对比结果应该需要花费很多时间。这里面重点是怎么补环境，要找出代码的检测点，只能通过对比返回值一步步筛查。

如果不使用nodejs访问，估计使用headless浏览器也一样会被拦截。

