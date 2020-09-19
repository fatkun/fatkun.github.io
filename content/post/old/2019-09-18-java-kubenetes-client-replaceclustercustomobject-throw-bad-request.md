---
title: 使用java kubenetes client replaceClusterCustomObject报错Bad Request
author: fatkun
type: post
date: 2019-09-18T02:18:15+00:00
url: /2019/09/java-kubenetes-client-replaceclustercustomobject-throw-bad-request.html
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:1845:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="html" style="font-family:monospace;">    public RequestBody serialize(Object obj, String contentType) throws ApiException {
            if (obj instanceof byte[]) {
                return RequestBody.create(MediaType.parse(contentType), (byte[])((byte[])obj));
            } else if (obj instanceof File) {
                return RequestBody.create(MediaType.parse(contentType), (File)obj);
            } else if (this.isJsonMime(contentType)) {
                String content;
                if (obj != null) {
                    content = this.json.serialize(obj);
                } else {
                    content = null;
                }
    &nbsp;
                return RequestBody.create(MediaType.parse(contentType), content);
            } else {
                throw new ApiException(&quot;Content type \&quot;&quot; + contentType + &quot;\&quot; is not supported&quot;);
            }
        }</pre></td></tr></table><p class="theCode" style="display:none;">    public RequestBody serialize(Object obj, String contentType) throws ApiException {
            if (obj instanceof byte[]) {
                return RequestBody.create(MediaType.parse(contentType), (byte[])((byte[])obj));
            } else if (obj instanceof File) {
                return RequestBody.create(MediaType.parse(contentType), (File)obj);
            } else if (this.isJsonMime(contentType)) {
                String content;
                if (obj != null) {
                    content = this.json.serialize(obj);
                } else {
                    content = null;
                }
    
                return RequestBody.create(MediaType.parse(contentType), content);
            } else {
                throw new ApiException(&quot;Content type \&quot;&quot; + contentType + &quot;\&quot; is not supported&quot;);
            }
        }</p></div>
    ";}
categories:
  - docker
  - go
tags:
  - client
  - JAVA
  - k8s
  - kubenetes

---
## 报错

报错Bad Request只是显式的错误，在ApiException里面有个resp返回的内容，在里面可以看到实际的错误，报错如下
couldn&#8217;t get version/kind; json parse error: json: cannot unmarshal string into Go value of type struct
## 原因

我在replaceClusterCustomObject最后一个参数里填了字符串（通过gson.toJson(obj)来返回），实际上不能传递字符串，直接传obj就好了，或者传bytes，就是不要传字符串。。
<pre escaped="true" lang="html">public RequestBody serialize(Object obj, String contentType) throws ApiException {
        if (obj instanceof byte[]) {
            return RequestBody.create(MediaType.parse(contentType), (byte[])((byte[])obj));
        } else if (obj instanceof File) {
            return RequestBody.create(MediaType.parse(contentType), (File)obj);
        } else if (this.isJsonMime(contentType)) {
            String content;
            if (obj != null) {
                content = this.json.serialize(obj);
            } else {
                content = null;
            }

            return RequestBody.create(MediaType.parse(contentType), content);
        } else {
            throw new ApiException("Content type \"" + contentType + "\" is not supported");
        }
    }</pre>