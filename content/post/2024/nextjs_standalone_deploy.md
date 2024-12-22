---
title: "nextjs v15.x独立部署"
date: 2024-12-23T14:51:54+08:00
tags: [前端, nextjs, react]
categories: [前端]
author: "fatkun"
draft: false
typora-root-url: ./..\..\..\static
---

# 概要

官方的[部署文档](https://github.com/vercel/next.js/blob/canary/examples/with-docker/Dockerfile)告诉我们用`npm run build`和`npm run start`启动，但是有时在服务器上不想安装一个很大的node_modules，在我开发环境都有1G左右了，所以要看怎么减少部署大小。

官方还有种方案是Docker部署，可以看[Dockerfile](https://github.com/vercel/next.js/blob/canary/examples/with-docker/Dockerfile)它是怎么构建的。

# 步骤

默认使用 `yarn run build`，在.next目录下是没有standalone这个目录的。需要参考[这个文档](https://nextjs.org/docs/pages/api-reference/config/next-config-js/output)的步骤做一个配置。

我使用mantine模板，我的配置文件为next.config.mjs，如果你的不同，可以参考文档的。

```
export default withBundleAnalyzer({
  ... 省略代码，加上以下这一行代码
  output: 'standalone',
});
```

加上配置之后，就可以执行`yarn run build`构建项目，构建完成后，需要把这几个目录拷贝一下，这里我用linux命令来表示拷贝过程。

```bash
cp .next/standalone/*  ./tmp/
cp .next/static ./tmp/.next/
cp public ./tmp/
```

拷贝完成之后，可以执行以下命令启动

```bash
node server.js
```



