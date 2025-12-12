---
title: "逆向unity游戏myyx3，使用dump.cs还原ida方法名"
date: 2025-12-12T10:55:33+08:00
tags: [逆向]
categories: [逆向]
author: "fatkun"
draft: false
typora-root-url: ./..\..\..\static
---

# 声明
仅用于学习记录，关键信息隐藏。

# 背景
游戏是unity+windows平台，使用il2cpp。

# 分析
首先，先尝试使用Il2CppDumper反编译
```bash
Il2CppDumper GameAssembly.dll global-metadata.dat out
```
但是报错
```
System.IndexOutOfRangeException: Index was outside the bounds of the array.
   at Il2CppDumper.Metadata..ctor(Stream stream) in C:\projects\il2cppdumper\Il2CppDumper\Il2Cpp\Metadata.cs:line 41
```
应该是做了某种加密，查看了一下global-metadata.dat文件头，是正确的 AF 1B B1 FA。

那就从加载metadata的代码看起。打开IDA，Shift+F12打开Strings列表，查找global-metadata.dat，发现字符串有。
双击字符串，按下x找关联的代码，找到一个方法
```
  v4 = sub_xxxxx("global-metadata.dat");
```
那这个方法应该是il2cpp::vm::MetadataLoader::LoadMetadataFile
尝试把这个方法发给AI分析，写成python代码，但是解密没成功，还是报错。

换一个思路，发现使用frida-il2cpp-bridge是可以dump cs的。

```
import "frida-il2cpp-bridge";
Il2Cpp.perform(() => {
    Il2Cpp.dump("dump.cs", "./");
}
```

dump完之后，可以看一下里面的方法，里面的偏移地址看起来都没什么问题。那能不能利用dump.cs修改IDA的方法名呢？
把想法发给AI，让它生成一个python代码提取dump.cs的名字和偏移地址。AI生成了一个代码，实际地址是：ImageBase + RVA。

```py
import idautils
import idaapi
import idc
import ida_funcs 
import re
import os

# --- 用户配置 ---
# 文件路径
DUMP_FILE_PATH = r"E:/dump.cs" 
# ----------------

def auto_rename_from_dump(file_path):
    """
    解析 dump.cs 文件，自动在 IDA 中重命名函数。
    脚本会动态识别类名，并用 '类名::函数名' 的格式进行重命名。
    """
    if not os.path.exists(file_path):
        print(f"❌ 错误：文件未找到，请检查路径：{file_path}")
        return

    # 1. 获取 IDA 数据库的基地址 (ImageBase)
    image_base = idaapi.get_imagebase()
    if image_base == idaapi.BADADDR:
        print("❌ 错误：无法获取 ImageBase。请确保已加载有效的 IDA 数据库。")
        return

    print(f"🌟 当前 IDA 数据库 ImageBase: 0x{image_base:X}")
    print(f"🔬 正在解析文件: {file_path}")

    functions_to_rename = {}
    current_class_name = "" # 用于跟踪当前解析到的类名
    
    # 正则表达式
    # 匹配类定义行: class Name: Inherit...
    class_pattern = re.compile(r'^\s*class\s+([\w\.]+)\s*:')
    # 匹配函数定义行: 返回类型 函数名(参数); // 0xRVA
    func_pattern = re.compile(r'\s*System\.[\w\.<>\[\]]*\s+([\w\.]+)\(.*?\);\s*//\s*(0x[0-9a-fA-F]+)')

    try:
        with open(file_path, 'r', encoding='utf-8') as f:
            for line in f:
                # 尝试匹配类定义
                class_match = class_pattern.search(line)
                if class_match:
                    # 找到新的类定义，更新当前类名
                    current_class_name = class_match.group(1).strip()
                    print(f"-> 发现类: {current_class_name}")
                    continue
                
                # 尝试匹配函数定义
                func_match = func_pattern.search(line)
                if func_match and current_class_name:
                    func_name = func_match.group(1).strip()
                    rva_str = func_match.group(2).strip()
                    
                    # 格式化新函数名： 类名::函数名
                    full_name = f"{current_class_name}::{func_name}"
                    
                    # 转换 RVA 为 VA
                    try:
                        rva = int(rva_str, 16)
                        va = image_base + rva
                        functions_to_rename[va] = full_name
                    except ValueError:
                        print(f"⚠️ 警告：跳过无效 RVA 行: {line.strip()}")
                
    except Exception as e:
        print(f"❌ 读取或解析文件时发生错误: {e}")
        return

    # 2. 在 IDA 中重命名
    total_found = len(functions_to_rename)
    print(f"🔍 成功从 dump 文件中解析到 {total_found} 个待重命名地址。")
    renamed_count = 0

    for va, name in functions_to_rename.items():
        # 检查地址是否在可访问的段内
        if idc.get_full_flags(va) == 0:
            continue
            
        # 尝试将地址定义为函数（如果还没有）
        if not ida_funcs.get_func(va):
            ida_funcs.add_func(va)
            
        # 执行重命名操作
        if idc.set_name(va, name, idc.SN_NOWARN | idc.SN_NOCHECK):
            renamed_count += 1

    print("--- 重命名报告 ---")
    print(f"🎉 任务完成！")
    print(f"总计解析函数数: {total_found}")
    print(f"成功重命名函数数: {renamed_count}")
    print("------------------")

# 执行主函数
# 注意：现在调用时不需要传入 CLASS_NAME_PREFIX 参数了
auto_rename_from_dump(DUMP_FILE_PATH)
```

在IDA执行脚本之后，大部分方法名就改过来了。

使用Reqable抓包发现，有部分请求是加密的。从代码浏览，SteamWindowsAgent看起来和登录有关系

```ts
import "frida-il2cpp-bridge";


Il2Cpp.perform(() => {
  const CSharp = Il2Cpp.domain.assembly("Assembly-CSharp").image;
  Il2Cpp.trace(false).classes(CSharp.class("Script.***.SdkAgent.SteamWindowsAgent")).and().attach();
}
```

尝试trace代码，这里看起来是上层调用，具体底层调用了哪些方法，没有trace到。
想着换一种思路，Hook网络请求，然后再从backtrace看调用链路。一般游戏都通过UnityEngine.Networking.UnityWebRequest发送请求，但是发现根本没有。
既然上面的SteamWindowsAgent是上层调用，进入IDA，找到对应的方法，按F5切换到伪代码查看，找到了一些蛛丝马迹。
它和KarmaSDK有关，KarmaSDK有多个类，把多个类都加入trace里面来。
为了提取密钥，尝试trace改成`Il2Cpp.trace(true)`，发现可以获取参数（很多时候会报错）。那这里就可以拿到加解密了。

IDA进入加解密的方法，我找到的伪代码发给AI分析，让它帮我们实现解密方法。
发现这个游戏用两种加密方式
第一种是AES（AES-128-CBC），请求参数加密：`KarmaSDK.ex::Encrypt` trace这个方法获取key和IV。
第二种是RSA（PKCS1_v1_5），返回内容加密：`KarmaSDK.fb::Decrypt`，trace获取RSA key。

里面很多子方法调用，可以先把主方法发给AI，然后问它还需要提供哪些子方法，继续提供信息给AI就行。提供的信息越多，实现越准确。不过GROK有点奇怪，老会吹牛逼，分析DLL的时候让我上传文件给我解密，说它解密好了，给我一个下载链接，发现根本不存在这个链接。

到这里基本就结束了，使用解密方法尝试解密抓包的内容，发现都成功了。

自从有了AI之后，分析代码的活都给AI干了，不用一行行的盯着伪代码看，试错也简单，如果AI有验证能力的话更好一些，有时候就是乱说一通。

