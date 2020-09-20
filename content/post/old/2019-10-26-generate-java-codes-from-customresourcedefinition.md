---
title: 从CustomResourceDefinition生成k8s java模型代码
author: fatkun
type: post
date: 2019-10-26T10:41:26+00:00
url: /2019/10/generate-java-codes-from-customresourcedefinition.html
wp-syntax-cache-content:
  - |
    a:6:{i:1;s:564:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">kubectl get <span style="color: #660033;">--raw</span>=<span style="color: #ff0000;">&quot;/openapi/v2&quot;</span> <span style="color: #000000; font-weight: bold;">&gt;</span> <span style="color: #000000; font-weight: bold;">/</span>tmp<span style="color: #000000; font-weight: bold;">/</span>swagger</pre></td></tr></table><p class="theCode" style="display:none;">kubectl get --raw=&quot;/openapi/v2&quot; &gt; /tmp/swagger</p></div>
    ";i:2;s:1062:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">docker run <span style="color: #660033;">-i</span> <span style="color: #660033;">--rm</span> dockerhub.azk8s.cn<span style="color: #000000; font-weight: bold;">/</span>yue9944882<span style="color: #000000; font-weight: bold;">/</span>java-model-gen <span style="color: #000000; font-weight: bold;">&lt;</span> <span style="color: #000000; font-weight: bold;">/</span>tmp<span style="color: #000000; font-weight: bold;">/</span>swagger <span style="color: #000000; font-weight: bold;">|</span> <span style="color: #c20cb9; font-weight: bold;">tar</span> <span style="color: #660033;">-xzf</span> - <span style="color: #660033;">-C</span> <span style="color: #000000; font-weight: bold;">/</span>tmp<span style="color: #000000; font-weight: bold;">/</span></pre></td></tr></table><p class="theCode" style="display:none;">docker run -i --rm dockerhub.azk8s.cn/yue9944882/java-model-gen &lt; /tmp/swagger | tar -xzf - -C /tmp/</p></div>
    ";i:3;s:424:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="other" style="font-family:monospace;">FROM dockerhub.azk8s.cn/yue9944882/java-model-gen
    &nbsp;
    COPY ./settings.xml /usr/share/maven/conf/settings.xml</pre></td></tr></table><p class="theCode" style="display:none;">FROM dockerhub.azk8s.cn/yue9944882/java-model-gen
    
    COPY ./settings.xml /usr/share/maven/conf/settings.xml</p></div>
    ";i:4;s:1327:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="other" style="font-family:monospace;">&lt;settings xmlns=&quot;http://maven.apache.org/SETTINGS/1.0.0&quot;
              xmlns:xsi=&quot;http://www.w3.org/2001/XMLSchema-instance&quot;
              xsi:schemaLocation=&quot;http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd&quot;&gt;
    &lt;mirrors&gt;
    &lt;mirror&gt;
        &lt;id&gt;aliyun-central&lt;/id&gt;
        &lt;mirrorOf&gt;*&lt;/mirrorOf&gt;
        &lt;name&gt;aliyun central&lt;/name&gt;
        &lt;url&gt;https://maven.aliyun.com/repository/central&lt;/url&gt;
    &lt;/mirror&gt;
    &lt;/mirrors&gt;
    &lt;/settings&gt;</pre></td></tr></table><p class="theCode" style="display:none;">&lt;settings xmlns=&quot;http://maven.apache.org/SETTINGS/1.0.0&quot;
              xmlns:xsi=&quot;http://www.w3.org/2001/XMLSchema-instance&quot;
              xsi:schemaLocation=&quot;http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd&quot;&gt;
    &lt;mirrors&gt;
    &lt;mirror&gt;
        &lt;id&gt;aliyun-central&lt;/id&gt;
        &lt;mirrorOf&gt;*&lt;/mirrorOf&gt;
        &lt;name&gt;aliyun central&lt;/name&gt;
        &lt;url&gt;https://maven.aliyun.com/repository/central&lt;/url&gt;
    &lt;/mirror&gt;
    &lt;/mirrors&gt;
    &lt;/settings&gt;</p></div>
    ";i:5;s:319:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">kubectl explain my_crd_name <span style="color: #660033;">--recursive</span></pre></td></tr></table><p class="theCode" style="display:none;">kubectl explain my_crd_name --recursive</p></div>
    ";i:6;s:509:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;">spec:
      preserveUnknownFields: false # 需要添加这个，这个值默认为true
      validation:
        openAPIV3Schema:
          type: object # 这里也要</pre></td></tr></table><p class="theCode" style="display:none;">spec:
      preserveUnknownFields: false # 需要添加这个，这个值默认为true
      validation:
        openAPIV3Schema:
          type: object # 这里也要</p></div>
    ";}
categories:
  - docker
tags:
  - client-java
  - k8s
  - kubenetes
  - open api

---
## 目标

已经有了go版本的模型定义，需要生成java版本
看了下官方介绍的文档 <a href="https://github.com/kubernetes-client/java/blob/master/docs/generate-model-from-third-party-resources.md" rel="noopener" target="_blank">generate-model-from-third-party-resources.md</a> 感觉不会太难，照着尝试一下。
## 开始干活

首先看到要k8s 1.15以上的版本，我只有1.14，只好使用minikube重新装了1.16的版本，具体安装不细说了。  
然后把CRD apply进集群里面，注意CRD得带有openAPIV3Schema的validation（我的是kubebuilder生成的）  
执行这个命令生成swagger json文件

```bash
kubectl get --raw="/openapi/v2" > /tmp/swagger
```

然后执行这个命令生成代码

```bash
docker run -i --rm dockerhub.azk8s.cn/yue9944882/java-model-gen < /tmp/swagger | tar -xzf - -C /tmp/
```

这里我添加了dockerhub.azk8s.cn镜像加速，这个镜像应该是别人构建好的，如果想自己构建，要用首页介绍的项目kubernetes-client/gen ，里面还会用到maven下载也是比较慢的，可以加一下mirrors
我写了个简单的Dockerfile

```Dockerfile
FROM dockerhub.azk8s.cn/yue9944882/java-model-gen
COPY ./settings.xml /usr/share/maven/conf/settings.xml
```

把settings.xml放到同一个目录，内容大概这样，可以加更多一些mirror
```xml
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd">
<mirrors>
<mirror>
    <id>aliyun-central</id>
    <mirrorOf>*</mirrorOf>
    <name>aliyun central</name>
    <url>https://maven.aliyun.com/repository/central</url>
</mirror>
</mirrors>
</settings>
```
执行完成后，生成的文件在/tmp/java里面，找一下自己要的文件在哪里。？？？文件呢？为什么只有个*List文件？？
试了下文档给出的CRD文件，确实可以生成，但为什么我的不行？  
试了执行一下explain, 发现字段没有显示出来。

```bash
kubectl explain my_crd_name --recursive
```

最终使用排除法的方式，对比例子和我crd的差异，找出了这里的差异

```yaml
spec:
  preserveUnknownFields: false # 需要添加这个，这个值默认为true
  validation:
    openAPIV3Schema:
      type: object # 这里也要
```
修改后使用 kubectl explain 可以正确识别字段