---
title: "逆向某TV 6.5.0(原某电新闻)"
date: 2025-12-29T00:22:01+08:00
tags: [android, 逆向]
categories: [android]
author: "fatkun"
draft: false
typora-root-url: ./..\..\..\static
---
# 背景
应用：57KkVFY=  版本：6.5.0
本文只用于学习研究，请勿作为非法用途，关键信息已隐藏。

这个APP使用某数字加固，发现这个东西居然检测frida了，如果后台启动了frida-server，启动APP就会直接退出，就算使用魔改版都被检测出来。

# 分析
我的目标主要是查看代码，而不是为了修改应用，所以主要是想办法获得真实的dex，并不想要脱壳。但是不脱壳，如何dump dex呢？
首先尝试使用frida，如果使用新启动程序，发现进程马上退出
```bash
    frida -U -f com.*****tv.*****tv -l .\DumpDex.js
```

当然也尝试一下网上的方法，替换创建线程的方法，但我并没有成功阻止进程退出。
```js
function hook_dlopen() {
    let Func_sleep = new NativeFunction(Process.getModuleByName('libc.so').getExportByName('sleep'), 'uint', ['uint'])

    // 安卓高版本使用android_dlopen_ext
    Interceptor.attach(Module.findGlobalExportByName("android_dlopen_ext"),
        {
            onEnter: function (args) {
                this.fileName = args[0].readCString()
                console.log(`Current PID: ${Process.id}`)
                console.log(`dlopen onEnter: ${this.fileName}`)
                // if(this.fileName != null && this.fileName.indexOf("libjiagu_64.so") >= 0){
                //     Func_sleep(10);
                // }

            }, onLeave: function(retval){
                console.log(`dlopen onLeave fileName: ${this.fileName}`)
            }
        }
    );
}
setImmediate(hook_dlopen)
```

尝试hook android_dlopen_ext，发现在加载libjiagu_64.so后，APP退出。

在继续搜寻隐藏Frida中，发现了这个项目 [ZygiskFrida](https://github.com/lico-n/ZygiskFrida)。

这个项目要求你的手机已ROOT，并且安装Magisk，开启Zygisk。
使用方法是下载 ZygiskFrida-v1.9.0-release.zip，上传到手机，使用Magisk安装模块，并重启手机。

重启后，需要做一些配置。
```bash
adb shell
su

cp /data/local/tmp/re.zyg.fri/config.json.example /data/local/tmp/re.zyg.fri/config.json
sed -i s/com.example.package/目标应用的包名/ /data/local/tmp/re.zyg.fri/config.json
```
改完之后，启动应用，会卡在首屏，不用怕。
然后可以通过两种命令attach。
`frida -U -N your.target.application` 或 `frida -U -n Gadget`

我使用的是
```bash
frida -U -N com.*****tv.*****tv -l DumpDex.js
```
注意我用的frida的版本是17.x，和16.x和之前的版本API有不兼容变更，具体变化可以看[这里](https://stackoverflow.com/questions/79700740/frida-17-module-getexportbyname-typeerror-not-a-function)。

其中DumpDex.js的内容是，记得改你自己的包名，否则会报错。
DumpDex代码来自：https://github.com/Alexjr2/Android_Dump_Dex

```
/*
Hook fork to prevent child processes from interrupting Frida
Returns -1 with errno EPERM
*/
(() => {
    const forkSymbol = Module.findGlobalExportByName("fork");
    if (!forkSymbol) {
        console.warn("[-] fork() not found");
        return;
    }
    const errnoPtr = (() => {
        const errnoLocation = Module.findGlobalExportByName("__errno_location");
        return errnoLocation ? new NativeFunction(errnoLocation, "pointer", [])() : null;
    })();

    const safeForkHandler = new NativeCallback(() => {
        console.warn("[!] Fork intercepted - returning -1 (EPERM)");
        if (errnoPtr) errnoPtr.writeS32(1);
        return -1;
    }, 'int', []);

    Interceptor.replace(forkSymbol, safeForkHandler);
    console.warn("[+] Fork hook: ACTIVE");
})();

/* 要改你的应用包名！！！ */
const TARGET_PKG = "com.*****tv.*****tv";
const SAFE_DIR = `/data/data/${TARGET_PKG}/`;

const DETECTION_LIBRARIES = [
    { pattern: "libdexprotector", message: "DexProtector: https://licelus.com" },
    { pattern: "libjiagu", message: "Jiagu360: https://jiagu.360.cn" },
    { pattern: "libAppGuard", message: "AppGuard: http://appguard.nprotect.com" },
    { pattern: "libDexHelper", message: "Secneo: http://www.secneo.com" },
    { pattern: "libsecexe|libsecmain|libSecShell", message: "Bangcle: https://github.com/woxihuannisja/Bangcle" },
    { pattern: "libprotectt|libapp-protectt", message: "Protectt: https://www.protectt.ai" },
    { pattern: "libkonyjsvm", message: "Kony: http://www.kony.com/" },
    { pattern: "libnesec", message: "Yidun: https://dun.163.com/product/app-protect" },
    { pattern: "libcovault", message: "AppSealing: https://www.appsealing.com/" },
    { pattern: "libpairipcore", message: "Pairip: https://github.com/rednaga/APKiD/issues/329" }
];

function hookDlopen() {
    return new Promise((resolve, reject) => {
        try {
            const isArm = Process.arch === "arm" ? "linker" : "linker64";
            const reg = Process.arch === "arm" ? "r0" : "x0";
            const linker = Process.findModuleByName(isArm);

            if (!linker) {
                reject(new Error("Linker module not found"));
                return;
            }

            let resolved = false;
            const resolveOnce = () => {
                if (!resolved) {
                    resolved = true;
                    resolve();
                }
            };

            const sym = linker.enumerateExports().find(e => e.name.includes('android_dlopen_ext'));
            Interceptor.attach(sym.address, {
                onEnter(args) {
                    const libPath = this.context[reg].readUtf8String();
                    if (!libPath) return;

                    for (const { pattern, message } of DETECTION_LIBRARIES) {
                        if (new RegExp(pattern).test(libPath)) {
                            console.warn(`\n[*] Packer Detected: ${message}`);
                            resolveOnce();
                            return;
                        }
                    }
                }
            });
            setTimeout(resolveOnce, 3000);
        } catch (e) {
            reject(new Error("Unsupported architecture/emulator"));
        }
    });
}

function processDex(Buf, C, Path) {
    // Ensure the buffer is valid
    if (!Buf || Buf.byteLength < 8) {
        console.error(`[!] Invalid buffer for classes${C - 1}.dex`);
        return;
    }
    const DumpDex = Buf instanceof Uint8Array ? Buf : new Uint8Array(Buf);
    const Count = C - 1;
    // Signatures for detecting CDEX, Empty Header, and Wiped Header
    const CDEX_SIGNATURE = [0x63, 0x64, 0x65, 0x78, 0x30, 0x30, 0x31];
    const EMPTY_HEADER = [0x00, 0x00, 0x00, 0x00];
    const WIPED_HEADER = [0x64];
    // Detect CDEX
    if (CDEX_SIGNATURE.every((val, i) => DumpDex[i] == val)) {
        console.warn(`[*] classes${Count}.dex is a Compact Dex (CDEX). Ignoring.`);
        return;
    }
    // Detect Empty Header (DexProtector)
    if (EMPTY_HEADER.every((val, i) => DumpDex[i] == val) && DumpDex[7] == 0x00) {
        console.warn(`[*] 00000 Header detected in classes${Count}.dex, possible DexProtector.`);
        writeDexFile(Count, Buf, Path, 0);
        return;
    }
    // Detect Wiped Header (Obfuscation/Tampered)
    if (DumpDex[0] == 0x00 || WIPED_HEADER.every((val, i) => DumpDex[i] != val)) {
        console.warn(`[*] Wiped Header detected, classes${Count}.dex might be interesting.`);
        writeDexFile(Count, Buf, Path, 0);
        return;
    }
    // Default: Consider it as a normal Dex file
    writeDexFile(Count, Buf, Path, 1);
}

function writeDexFile(count, buffer, path, isValid) {
    try {
        const file = new File(path, "wb");
        file.write(buffer);
        file.close();
        console.log(`[Dex${count}] Saved to: ${path} ${isValid ? '(valid)' : '(modified)'}`);
    } catch (error) {
        console.error(`[!] Failed to save Dex${count} to ${path}: ${error.message}`);
    }
}

function findDefineClass(libart) {
    const matcher = /ClassLinker.*DefineClass.*Thread.*DexFile/;
    const search = (items, type) => items.find(item => matcher.test(item.name))?.address;

    return search(libart.enumerateSymbols(), 'symbols') ||
           search(libart.enumerateImports(), 'imports') ||
           search(libart.enumerateExports(), 'exports');
}

function dumpDex() {
    const libart = Process.findModuleByName("libart.so");
    if (!libart) return console.error("[!] libart.so not found");
    const defineClassAddr = findDefineClass(libart);
    console.warn("[*] DefineClass found at : ", defineClassAddr);
    if (!defineClassAddr) return console.error("[!] DefineClass not found");
    const seenDex = new Set();
    let dexCount = 1;

    Interceptor.attach(defineClassAddr, {
        onEnter(args) {
            const dexFilePtr = args[5];
            const base = dexFilePtr.add(Process.pointerSize).readPointer();
            const size = dexFilePtr.add(Process.pointerSize * 2).readUInt();
            if (seenDex.has(base.toString())) return;
            seenDex.add(base.toString());
            const dexBuffer = base.readByteArray(size);
            if (!dexBuffer || dexBuffer.byteLength !== size) return;
            const path = `${SAFE_DIR}classes${dexCount}.dex`;
            processDex(dexBuffer, dexCount++, path);
        }
    });
}

async function main() {
    try {
        await hookDlopen();
        console.warn("[*] Hooking Finished. Starting dex dump...");
        dumpDex();
    } catch (e) {
        console.error(`[!] Error: ${e.message}`);
    }
}

setImmediate(main);

```

dump出dex文件在上面的/data/data/{应用包名}目录下，把文件下载下来，拖入jadx，直接就看到源码了。

有了源码，分析就简单了，先抓包看看有什么变化。大概看了下，加密都没怎么变。
只有这个请求`v3/tvChannelList`变为`v5/tvChannelList`，另外APP也需要登录才能使用，那对应的接口也增加了两个Header验证。
分别是
```
X-*****TV-USER-ID
Authorization
```
补上就可以用了，其他参数和之前一样。
但是还不清楚这个验证能用多久，需要长时间验证看看能用多久。