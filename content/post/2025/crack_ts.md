---
title: "WEB前端逆向TS NALU解密"
date: 2025-07-28T10:55:33+08:00
tags: [逆向]
categories: [逆向]
author: "fatkun"
draft: false
typora-root-url: ./..\..\..\static
---

# 背景

使用浏览器可以找到m3u8链接，把ts文件下载下来播放，发现有声音但是花屏。

这里面可能是对TS帧加密。

上网搜索找到这篇文章，[WEB前端逆向TS PES NALU解密](https://www.52pojie.cn/forum.php?mod=viewthread&tid=1957747&extra=page%3D1&page=1)，但这篇文章是针对视频的，我是想对直播解密，使用[上述的脚本](https://www.initialsky.com/archives/104)，解密出来，底下有一点花屏。

# 分析

从其他文章知道这个网站是使用wasm加密，所以可以先找到wasm，然后找到对应的js文件，js文件比较重要的有

```
h5.worker%3Fv=220805
wasm文件，会构造一个对象 CNTVModule，这个js有一点点混淆，反混淆就好。可以在chrome浏览器里面Override反混淆后的代码。

liveplayer.js
可以根据CNTVModule找到CNTVH5PlayerModule = CNTVModule();

liveplayer_controls.js
根据CNTVH5PlayerModule找到，解密代码调用位置
```

先来到liveplayer_controls.js这个文件，主要的解密方法是在x.prototype._parseAVCPES里。

```js
   x.prototype._parseAVCPES = function (h, e) {
        var g;
        var y;
        var m;
        var v = this;
        var E = this._avcTrack;
        var t = this._parseAVCNALu(h.data);
        var _ = this.avcSample;
        var T = false;
        var S = false;
        var b = this.pushAccesUnit.bind(this);
        h.data = null;
        if (_ && t.length && !E.audFound) {
          b(_, E);
          _ = this.avcSample = p(false, h.pts, h.dts, "");
        }
...

function uint8ToHex(uint8Array) {
    // 确保输入是 Uint8Array 或类数组
    if (!ArrayBuffer.isView(uint8Array) && !Array.isArray(uint8Array)) {
        throw new Error('Input must be a Uint8Array or an array of numbers');
    }

    return Array.from(uint8Array)
        .map(byte => byte.toString(16).padStart(2, '0')) // 转为两位小写 hex
        .join(' '); // 用空格分隔每个字节
}
        
        t.forEach(function (e) {
          y = L = false;
            // 可以插入一些代码测试
          console.log("e.type", e.type, uint8ToHex(e.data));
          if (!(e.type !== 5 && e.type !== 1)) {
            if (F && CNTVH5PlayerModule) {
              e.data = A(e.data, 0);
            } else if (M && CNTVH5PlayerModule) {
              e.data = A(e.data, 1);
            }
          }
          ...
        return S;
      };
```

从代码看到 `t = this._parseAVCNALu(h.data);`先把NALu解析出来，然后调用 `t.forEach` 遍历，如果类型是1或5才做解密。其中直播是调用 `A(e.data, 0)`。

来到看解密方法

```js
        function A(e, t) {
          var r = 0;
          var i = 0;
          var a = 0;
          var n = new Uint8Array(0);
          try {
            
            r = CNTVH5PlayerModule._jsmalloc(e.byteLength + 1024);
            for (var o = 0; o < e.byteLength; o++) {
              CNTVH5PlayerModule.HEAP8[r + o] = e[o];
            }
            if (!v.signalUrlSend) {
              a = v.rootURL.length;
              for (var s = 0; s < a; s++) {
                CNTVH5PlayerModule.HEAP8[r + e.byteLength + s] = v.rootURL.charCodeAt(s);
              }
              v.signalUrlSend = true;
            }
            if (t == 0) {
              i = CNTVH5PlayerModule._nalplay2(r, e.byteLength, a);
            } else if (t == 1) {
              i = CNTVH5PlayerModule._vodplay(r, e.byteLength, a);
            }
            n = new Uint8Array(i);
            for (var l = 0; l < n.byteLength; l++) {
              n[l] = CNTVH5PlayerModule.HEAP8[r + l];
            }
          } catch (e) {}
          CNTVH5PlayerModule._jsfree(r);
          r = null;
          return n;
        }
```

解密方法看到前面把地址放到CNTVH5PlayerModule.HEAP8[r + e.byteLength]之后，直播调用 `i = CNTVH5PlayerModule._nalplay2(r, e.byteLength, a);` 解密，视频是调用 `_vodplay`，实际上调用wasm里面的方法。

根据文档 [ts帧加密案例(一)](https://www.52pojie.cn/thread-1875225-1-1.html) 我们知道如果直接调用这个方法的话，wasm里面会有很多env import，会针对浏览器很多检查，他第一次调用的时候发现还是有一些花屏，在第二篇文章里 [ts帧加密案例(二)](https://www.52pojie.cn/thread-1882587-1-1.html) 发现是环境没补全。

但是作者跟踪代码可以绕过这个方法调用，跳过这些检查，这里不清楚作者是如何发现这个内部调用的。

如果想要分析，可以使用[wabt工具](https://github.com/WebAssembly/wabt)来反编译，可以编译成c或者wat格式。跟踪代码可以看到，直播调用的是func58_tea，和视频调用的func60_tea不一样。

根据文章我们可以把内部方法暴露出来，wasm是base64格式的文本，可以让AI写一个方法保存为文件

先转为wat格式

```bash
wasm2wat xxx.wasm -o xxx.wat
```

修改wat，在导出表里增加两行(搜索export)

```
(export "func58_TEA" (func 58))
(export "func60_TEA" (func 60))
```

最后再转回wasm，然后再转回base64的格式填回代码里面

```bash
wat2wasm xxx.wat -o xxx_out.wasm
```



# TS 格式分析

分析一下 [WEB前端逆向TS PES NALU解密](https://www.52pojie.cn/forum.php?mod=viewthread&tid=1957747&extra=page%3D1&page=1) 文章里面的代码之前，先来简单理解一下TS格式，我也不太懂，根据自己理解描述一下。

TS每个Frame 188个字节，第一个字节固定是0x47，每个Frame包含Header和数据，里面可能是一些属性数据或者视频流、音频流，我们可以用010Editor来辅助分析。

在010Editor里面我们可以下载模板，在Templates > Templates Repository 里面下载 TS/H264 的模板，然后再选择Templates > Video > TS 就可以看到解析后的格式了。如果选择H264也可以找到H264的解析。

<img src="/img/crack_ts/image-20250728181702806.png" alt="image-20250728181702806" style="zoom: 67%;" />

TSHeader里面有一个PID，表示一个编号，也是一个类型，我们需要根据PID找到哪个是视频流，我们只对视频流解密。文章作者说通过软件看到视频流的PID是0x100，在代码中也做了这个过滤，那这个是怎么看出来的呢？

可以先找到PAT，PAT是在PID=0的Frame里面，可以找到PMT的PID。

<img src="/img/crack_ts/image-20250728182603674.png" alt="image-20250728182603674" style="zoom:67%;" />

如果你的Value不是按16进制显示，可以在标题栏右键，选择Value > Hex。可以看到PMT的PID在0x1001，文件我看是在第二个Frame里面。

<img src="/img/crack_ts/image-20250728182859581.png" alt="image-20250728182859581" style="zoom:67%;" />

这里看到PMTElementary有多个，这里是定义stream_type对应的PID是什么，这里第一个stream_type是 0x1B ，这个是h264类型，我们可以看到PID是 0x100。但我实际运行下来，这个一般是0x100，但实际有时候会变的，所以需要动态的读取这个值。原作者是固定使用了这个值，会导致有部分时候花屏。

然后我们就可以根据前面得到的PID得到视频流，解析里面的NALu。

回到代码，代码Parse_TS_Packet里面会涉及到一些合并Frame，没了解很多TS结构，我不懂。然后再在这里面找NALu的开头，它是以`0x 00 00 01` 或者 `0x 00 00 00 01` 开头，FindNalUnitStart方法就是找这些开头。

但代码里面有种情况没有处理，就是如果payload里面有`0x000003`  ，需要替换成 `0x0000`，它是为了避免分隔符和数据混淆做了替换（H264的 Encapsulated Byte Sequence Payload编码），对数据做了替换。不过这种情况可能很少，偶尔出错一次应该也不太影响。

``````
0x000000-->0x00000300
0x000001-->0x00000301
0x000002-->0x00000302
0x000003-->0x00000303
``````

原有代码调用的是FUNC60，是针对视频的，如果是直播，内部调用的是FUNC58，可以断点进入wasm里面看到。

参考原有js代码实现，另外func58_TEA的参数和原代码有点不一样，可以断点调试对比对应的值是什么，也可以把xx.wat发给AI，让它给你分析，才发现第二个和第三个参数是一样的。

```js
function XOR(e) {
    let r = 0;
    let i = 0;
    let a = 0;
    let n = new Uint8Array(0);
    try {
        
    r = CNTVH5PlayerModule._jsmalloc( e.byteLength + 1024);
    for (var o = 0; o < e.byteLength; o++) {
        CNTVH5PlayerModule.HEAP8[r + o] = e[o];
    }
    i = CNTVH5PlayerModule.asm.func58_TEA( r, e.byteLength, e.byteLength);
    n = new Uint8Array(i);
    for (var l = 0; l < n.byteLength; l++) {
        n[l] = CNTVH5PlayerModule.HEAP8[r + l];
    }
    } catch (e) {
        console.log("err", e);
    }
    CNTVH5PlayerModule._jsfree(r);
    r = null;
    return n;
}
```

# 排查问题

改完这个发现可以直播观看了，但是后台还是时不时会报错，画面有部分花屏。

这时可以在network找到ts文件的下载，在后面找到调用的js地址，下断点，每次下载ts的时候，我们可以暂停，在解析的地方可以增加一些日志调试，也可以把对应的ts文件下载下来本地分析。

有一些报错是 `RuntimeError: memory access out of bounds` ，解密失败了，发现问题是原代码写死视频的PID是0x100，但实际上还是偶尔有不一样的。

我们可以从PMT里面找到视频流的PID，让AI帮我写了一些方法。这里吐槽一下qwen3 coder，让它改了好几次才正确。不过对于这个文件位运算的代码，我还真不保证我能写明白，当前AI还是牛的。

```js
function Parse_PAT ( buf, index ) {
    // PAT PID is always 0x0000
    let PID = ((buf[index + 1] & 0x1f) << 8) + buf[index + 2];
    // console.log("Parsing PAT at index:", index, "PID:", PID.toString(16));
    if (PID !== 0x0000) {
        return null;
    }
    
    // Skip TS header (4 bytes) + adaptation field (if exists)
    let AdaptationFieldControl = (buf[index + 3] & 0x30) >>> 4;
    let payload_index = index + 4;
    
    if (AdaptationFieldControl === 2 || AdaptationFieldControl === 3) {
        let AdaptationFieldLength = buf[index + 4];
        payload_index += 1 + AdaptationFieldLength;
    }
    
    // Skip pointer_field
    let pointer_field = buf[payload_index];
    payload_index += 1 + pointer_field;
    
    // Check table_id
    let table_id = buf[payload_index];
    // console.log("PAT table_id:", table_id);
    if (table_id !== 0x00) {
        console.log("Invalid PAT table_id:", table_id);
        return null;
    }
    
    // Skip table_id
    payload_index += 1;
    
    // Get section_length (first 2 bits are reserved)
    let section_length = ((buf[payload_index] & 0x0f) << 8) | buf[payload_index + 1];
    // console.log("PAT section_length:", section_length);
    payload_index += 2;
    
    // Skip reserved, version_number, current_next_indicator, section_number, last_section_number
    payload_index += 5;
    
    // Get program_number and PMT PID
    // program_number is 2 bytes
    // PMT PID is in the next 2 bytes (with first 3 bits as reserved)
    let program_number = (buf[payload_index] << 8) | buf[payload_index + 1];
    let pmt_pid = ((buf[payload_index + 2] & 0x1f) << 8) | buf[payload_index + 3];
    // console.log("PAT program_number:", program_number, "PMT PID:", pmt_pid.toString(16));
    
    return pmt_pid;
}
```

```js
function Parse_PMT ( buf, index ) {
    // Parse PMT to find video stream PID
    let PID = ((buf[index + 1] & 0x1f) << 8) + buf[index + 2];
    // console.log("Parsing PMT at index:", index, "PID:", PID.toString(16));

    
    // Skip TS header (4 bytes) + adaptation field (if exists)
    let AdaptationFieldControl = (buf[index + 3] & 0x30) >>> 4;
    let payload_index = index + 4;
    
    if (AdaptationFieldControl === 2 || AdaptationFieldControl === 3) {
        let AdaptationFieldLength = buf[index + 4];
        payload_index += 1 + AdaptationFieldLength;
    }
    
    // Skip pointer_field
    let pointer_field = buf[payload_index];
    payload_index += 1 + pointer_field;
    
    // Check table_id
    let table_id = buf[payload_index];
    // console.log("PMT table_id:", table_id);
    if (table_id !== 0x02) {
        console.log("Invalid PMT table_id:", table_id);
        return null;
    }
    
    // Skip table_id
    payload_index += 1;
    
    // Get section_length (first 2 bits are reserved)
    let section_length = ((buf[payload_index] & 0x0f) << 8) | buf[payload_index + 1];
    // console.log("PMT section_length:", section_length);
    payload_index += 2;
    
    // Skip program_number (2 bytes)
    payload_index += 2;
    
    // Skip reserved (2 bits) + version_number (5 bits) + current_next_indicator (1 bit) = 1 byte
    payload_index += 1;
    
    // Skip section_number (1 byte) + last_section_number (1 byte) = 2 bytes
    payload_index += 2;
    
    // Skip reserved (3 bits) + PCR_PID (13 bits) = 2 bytes
    payload_index += 2;
    
    // Skip program_info_length (first 4 bits are reserved)
    let program_info_length = ((buf[payload_index] & 0x0f) << 8) | buf[payload_index + 1];
    // console.log("PMT program_info_length:", program_info_length);
    payload_index += 2;
    
    // Skip program descriptors
    payload_index += program_info_length;
    
    // Parse elementary streams
    let video_pid = null;
    let end_position = index + 4 + section_length; // 4 bytes for TS header + section_length
    // console.log("PMT end_position:", end_position, "payload_index:", payload_index);
    
    while (payload_index < end_position - 4) { // -4 to ensure we have enough bytes for stream_type and PID
        // Ensure we have enough bytes for stream_type and PID
        if (payload_index + 2 >= buf.length) {
            console.log("Not enough bytes for stream_type and PID");
            break;
        }
        
        let stream_type = buf[payload_index];
        let stream_pid = ((buf[payload_index + 1] & 0x1f) << 8) | buf[payload_index + 2];
        // console.log("Stream type:", stream_type, "PID:", stream_pid.toString(16));
        
        // H.264 stream type is 0x1b
        if (stream_type === 0x1b) {
            video_pid = stream_pid;
            // console.log("Found H.264 video stream PID:", video_pid.toString(16));
            break;
        }
        
        // Check if we have enough bytes for ES_info_length
        if (payload_index + 4 >= buf.length) {
            console.log("Not enough bytes for ES_info_length");
            break;
        }
        
        // Skip ES_info_length (first 2 bits are reserved)
        let es_info_length = ((buf[payload_index + 3] & 0x0f) << 8) | buf[payload_index + 4];
        // console.log("ES info length:", es_info_length);
        payload_index += 5 + es_info_length;
    }
    
    return video_pid;
}
```

拿到视频PID之后，就可以在里面过滤了。



# 总结

最终测试下来，虽然还是偶尔有报错，但总体基本可用了。



# 参考

[WEB前端逆向TS PES NALU解密](https://www.52pojie.cn/forum.php?mod=viewthread&tid=1957747&extra=page%3D1&page=1)

[ts帧加密案例(一)](https://www.52pojie.cn/thread-1875225-1-1.html)

[ts帧加密案例(二)](https://www.52pojie.cn/thread-1882587-1-1.html)
