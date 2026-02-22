---
title: "使用AI编程你需要了解的东西"
date: 2026-02-22T10:22:01+08:00
tags: [编程, AI]
categories: [编程]
author: "fatkun"
draft: false
typora-root-url: ./..\..\..\static
---

# 概括
本文介绍使用AI编程相关内容，用于记录一些好用的提示词，MCP，Skills。不包含如何安装codex，claude code等。

# 好用的工具
## CC Switch，中转站切换
如果你有多个中转站，使用这个工具能够很方便帮你管理配置，这个工具本来是帮你保存多个配置，随时切换。如果开启代理方式，就可以无缝切换站点，不需要重启AI客户端。

## CliProxyAPI
如果需要反代一些官方服务，可以使用这个服务，例如OpenAI账号反代。

## NewAPI
目前很多中转站使用的AI网关，如果有多个中转站，可以使用它统一配置，避免每个终端都要配置很多站点。

## All API Hub（chrome扩展）
用于管理多个公益站，可以自动添加站点，也可以比较方便用它在其他软件配置KEY（包括NewAPI，CC Switch）

# 提示词
每个软件的提示词名字不一样，例如claude的是CLAUDE.md，可以放在全局的目录或者在项目内.claude目录里面。CC Switch可以管理全局提示词。

编写提示词可以让AI遵循你的规则，例如可以让它在开始编码之前，先说出他的计划，等待你确认后再开始编码。

# Skills
Skills是一些技能描述，其实也算是一种提示词，不过为了节省Token，避免把所有信息都塞进提示词里，所以推出了Skills。claude会搜索一些简单的技能描述，如果有需要调用，再读取完整的Skill能力，Skill里面包含描述和脚本(python之类)，这样就可以很精准的执行一些事情。
不过据说Skills可能不会调用，也可以在提示词里面告诉AI，或者直接用 "/xxxx" 指定某个Skill。

Skills也可以用CC Switch管理。可以在这里面找Skills https://skillsmp.com/zh

## ui-ux-pro-max-skill
https://github.com/nextlevelbuilder/ui-ux-pro-max-skill

这个是用于UI设计的技能

## collaborating-with-codex
https://github.com/GuDaStudio/collaborating-with-codex

这个是用于在claude里面调用codex

## frida-17
https://github.com/NeverSight/skills_feed/tree/main/data/skills-md/yfe404/frida-17-skill/frida-17

frida-17 的API变更了，很多AI还是生成旧的API，所以需要Skill纠正AI

## idapython
https://github.com/mrexodia/ida-pro-mcp/tree/main/skills/idapython

ida pro分析必用

# MCP
MCP是用于AI操作第三方软件的管道，MCP服务会返回一些tool的描述。我感觉MCP可以被Skills替代，但AI说两者有些不一样。

## fast-context
https://github.com/SammySnake-d/fast-context-mcp

这个是用于使用自然语言搜索代码，这个是逆向Windsurf的服务。理论上应该对比较大的项目搜寻代码简单一些。现在AI一般用grep找代码，需要阅读所有代码。

## chrome-mcp-server
操作chrome

## ida-pro-mcp
https://github.com/mrexodia/ida-pro-mcp

操作ida pro

## jadx
https://github.com/zinja-coder/jadx-ai-mcp

操作jadx，需要使用steamable-http的方式才能连接
```
{
  "startupTimeout": 30000,
  "toolTimeout": 300000,
  "type": "steamable-http",
  "url": "http://127.0.0.1:8651/mcp"
}
```