---
title: docker pull 访问registry过程
author: fatkun
type: post
date: 2018-01-28T03:01:28+00:00
url: /2018/01/docker-pull.html
categories:
  - docker
tags:
  - docker
  - Registry

---
执行 docker pull daocloud.io/busybox 之后
&nbsp;
<table>  <tr>    <td style="width: 16px;">      步骤    </td>
    <td>      请求    </td>
    <td style="width: 1113px;">      返回    </td>  </tr>
  <tr>    <td style="width: 16px;">      1    </td>
    <td style="width: 1113px;">      GET https://daocloud.io/v2/ HTTP/1.1    </td>
    <td style="width: 1113px;">      HTTP/1.1 401 Unauthorized<br /> Server: nginx/1.11.13<br /> Date: Sun, 28 Jan 2018 02:35:17 GMT<br /> Content-Type: application/json; charset=utf-8<br /> Content-Length: 87<br /> Connection: close<br /> Docker-Distribution-Api-Version: registry/2.0<br /> Www-Authenticate: Bearer realm=&#8221;https://daohub-auth.daocloud.io/auth&#8221;,service=&#8221;daocloud.io&#8221;<br /> X-Content-Type-Options: nosniff{&#8220;errors&#8221;:[{&#8220;code&#8221;:&#8221;UNAUTHORIZED&#8221;,&#8221;message&#8221;:&#8221;authentication required&#8221;,&#8221;detail&#8221;:null}]}    </td>  </tr>
  <tr>    <td style="width: 16px;">      2    </td>
    <td style="width: 1113px;">      GET https://daohub-auth.daocloud.io/auth?scope=repository%3Abusybox%3Apull&service=daocloud.io HTTP/1.1    </td>
    <td style="width: 1113px;">      HTTP/1.1 200 OK<br /> Server: nginx/1.11.6<br /> Date: Sun, 28 Jan 2018 02:35:17 GMT<br /> Content-Type: application/json<br /> Content-Length: 570<br /> Connection: close<br /> X-Qequest-Time: 0.025{&#8220;token&#8221;:&#8221;eyJ0eXAiOiJKV1QiL省略_J0Mzfs&#8221;}    </td>  </tr>
  <tr>    <td style="width: 16px;">      3    </td>
    <td style="width: 1113px;">      GET https://daocloud.io/v2/busybox/manifests/latest HTTP/1.1</p> 
      
      <p>        Authorization: Bearer eyJ0eXAiOiJKV1QiL省略_J0Mzfs</td> 
        
        <td style="width: 1113px;">          HTTP/1.1 200 OK<br /> Server: nginx/1.11.13<br /> Date: Sun, 28 Jan 2018 02:35:18 GMT<br /> Content-Type: application/vnd.docker.distribution.manifest.v2+json<br /> Content-Length: 527<br /> Connection: close<br /> Docker-Content-Digest: sha256:4cee1979ba0bf7db9fc5d28fb7b798ca69ae95a47c5fecf46327720df4ff352d<br /> Docker-Distribution-Api-Version: registry/2.0<br /> Etag: &#8220;sha256:4cee1979ba0bf7db9fc5d28fb7b798ca69ae95a47c5fecf46327720df4ff352d&#8221;<br /> X-Content-Type-Options: nosniff{<br /> &#8220;schemaVersion&#8221;: 2,<br /> &#8220;mediaType&#8221;: &#8220;application/vnd.docker.distribution.manifest.v2+json&#8221;,<br /> &#8220;config&#8221;: {<br /> &#8220;mediaType&#8221;: &#8220;application/vnd.docker.container.image.v1+json&#8221;,<br /> &#8220;size&#8221;: 1497,<br /> &#8220;digest&#8221;: &#8220;sha256:5b0d59026729b68570d99bc4f3f7c31a2e4f2a5736435641565d93e7c25bd2c3&#8221;<br /> },<br /> &#8220;layers&#8221;: [<br /> {<br /> &#8220;mediaType&#8221;: &#8220;application/vnd.docker.image.rootfs.diff.tar.gzip&#8221;,<br /> &#8220;size&#8221;: 723070,<br /> &#8220;digest&#8221;: &#8220;sha256:57310166fe88e0dc63a80ca5c219283a932db0f3969712e2f8a86ada143bf566&#8221;<br /> }<br /> ]<br /> }        </td></tr> 
        
        <tr>          <td style="width: 16px;">            4          </td>
          <td style="width: 1113px;">            GET https://daocloud.io/v2/busybox/blobs/<br /> sha256:5b0d59026729b68570d99bc4f3f7c31a2e4f2a5736435641565d93e7c25bd2c3 HTTP/1.1</p> 
            
            <p>              Authorization: Bearer eyJ省略</td> 
              
              <td style="width: 1113px;">                HTTP/1.1 307 Temporary Redirect<br /> Server: nginx/1.11.13<br /> Date: Sun, 28 Jan 2018 02:35:18 GMT<br /> Content-Type: application/octet-stream<br /> Content-Length: 311<br /> Connection: close<br /> Docker-Distribution-Api-Version: registry/2.0<br /> Location: http://daohub.ufile.ucloud.com.cn/docker/registry/v2/blobs/<br /> sha256/5b/5b0d59026729b68570d99bc4f3f7c31a2e4f2a5736435641565d93e7c25bd2c3/data?Expires=1517107218&Signature=Q72RCd%省略%3D&UCloudPublicKey=mhEYuIyt6tZwLlE省略Blg%2Bc<br /> X-Content-Type-Options: nosniff&nbsp;              </td></tr> 
              
              <tr>                <td style="width: 16px;">                  5                </td>
                <td style="width: 1113px;">                  GET http://daohub.ufile.ucloud.com.cn/docker/registry/v2/blobs/<br /> sha256/5b/5b0d59026729b68570d99bc4f3f7c31a2e4f2a5736435641565d93e7c25bd2c3/data?Expires=1517107218&Signature=Q72RCd%省略%3D&UCloudPublicKey=mhEYuIyt6tZwLlE省略Blg%2Bc HTTP/1.1                </td>
                <td style="width: 1113px;">                  返回具体文件内容                </td>              </tr></tbody> </table>