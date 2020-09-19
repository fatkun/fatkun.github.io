---
title: Jquery的ajax在IE提交数据乱码解决方法
author: fatkun
type: post
date: 2010-12-02T06:14:09+00:00
url: /2010/12/jquery-ajax.html
duoshuo_thread_id:
  - 6300408788524466945
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:390:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="js" style="font-family:monospace;">$.ajaxSetup({
    	contentType: &quot;application/x-www-form-urlencoded; charset=utf-8&quot;
    });</pre></td></tr></table><p class="theCode" style="display:none;">$.ajaxSetup({
    	contentType: &quot;application/x-www-form-urlencoded; charset=utf-8&quot;
    });</p></div>
    ";}
categories:
  - 网页前端
tags:
  - ajax
  - get
  - jquery
  - post
  - 乱码

---
乱码是因为编码不同而造成的。在ajax post 或 get时都有可能出现乱码。
为了避免乱码，可以做到以下几步
## 解决方法

### 1，保持编码的统一，包括文件编码，数据库编码，网页content-type编码

检查一下<meta http-equiv=&#8221;content-type&#8221; content=&#8221;text/html; charset=UTF-8&#8243; />
建议中文都是用UTF-8，使用gbk/gb2312有可能会出现乱码
### 2，使用post来发送而不是get

get方法是会通过链接来传递参数，而且会自动urlEncode(编码)，而各个浏览器编码的方式可能不太一样。使用post可以避免这种情况。
### 3，通过在js前端escape编码再发送，然后后台解码取得数据

这些可以在网上搜索
### 4，在全局设定contentType，指定编码

因为jquery ajax是使用utf-8来编码发送数据的，ie在发送时却没加上<span style="font-family: Consolas, Monaco, 'Courier New', Courier, monospace; line-height: 18px; font-size: 12px; white-space: pre;">charset=utf-8，从而导致乱码(IE默认使用iso-8859-1编码)</span>
<pre escaped="true" lang="js">$.ajaxSetup({
	contentType: "application/x-www-form-urlencoded; charset=utf-8"
});</pre>