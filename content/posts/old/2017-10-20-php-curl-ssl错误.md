---
title: php curl ssl错误
author: fatkun
type: post
date: 2017-10-20T07:10:07+00:00
url: /2017/10/php-curl-ssl错误.html
categories:
  - 未分类
tags:
  - curl
  - php
  - SSL

---
可以使用 echo curl_error($ch); 打印错误信息
如果是 SSL certificate problem, verify that the CA cert is OK 这种错误
在php.ini搜索curl.cainfo，改成这个值  
curl.cainfo=&#8221;/etc/ssl/certs/ca-bundle.crt&#8221;
https://stackoverflow.com/questions/8227909/curl-exec-always-returns-false  
https://stackoverflow.com/questions/6400300/https-and-ssl3-get-server-certificatecertificate-verify-failed-ca-is-ok