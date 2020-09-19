---
title: 000webhost开启gzip压缩(使用htaccess开启gzip)
author: fatkun
type: post
date: 2010-07-06T04:35:17+00:00
url: /2010/07/000webhost-htaccess-gzip.html
views:
  - 39
duoshuo_thread_id:
  - 6300408744241005313
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:360:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="html" style="font-family:monospace;">php_flag zlib.output_compression On
    php_value zlib.output_compression_level 8</pre></td></tr></table><p class="theCode" style="display:none;">php_flag zlib.output_compression On
    php_value zlib.output_compression_level 8</p></div>
    ";}
categories:
  - 胡言乱语
tags:
  - gzip
  - htaccess

---
对于<a style="text-decoration: none; color: #3d1466;" href="http://www.000webhost.com/">000webhost</a>空间，开启Gzip压缩功能会有网页打不开的现象，不管是通过插件开启还是其他方法，网页打不开，后台打不开始终是个大问题。
<p style="margin-top: 0px; margin-bottom: 15px;">  首先，看看你的根目录下有没有.htaccess文件，如果没有请在本地建立x.htaccess然后上传到你的根目录下，重命名为.htaccess。请注意，.htaccess文件的位置是在根目录下，比如我的是public_html/.htaccess。</p>
<p style="margin-top: 0px; margin-bottom: 15px;">  其次，打开.htaccess文件，添加以下语句</p>
<pre escaped="true" lang="html">php_flag zlib.output_compression On
php_value zlib.output_compression_level 8</pre>
检测你的博客，看看是否开启了Gzip压缩功能。  
<a href="http://tool.chinaz.com/Gzips/" target="_blank">http://tool.chinaz.com/Gzips/</a>  
<a href="http://gzip.zzbaike.com/" target="_blank">http://gzip.zzbaike.com/</a>  
上文来源：<http://www.indear.net/274.html>
&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-
我的首页压缩后的大小
<table style="border-collapse: collapse; font-size: 14px; line-height: 25px; color: #666666; width: 430px; font-family: Simsun; padding: 0px; margin: 0px;" border="0">  <tr style="background-color: #6fbee7; padding: 0px; margin: 0px;">    <td style="padding-top: 0px; padding-right: 10px; padding-bottom: 0px; padding-left: 10px; height: 25px; margin: 0px; border: 1px solid #6fbee7;" colspan="2">      <h2 style="font-size: 16px; font-weight: bold; color: #ffffff; padding: 0px; margin: 0px;">        检测结果      </h2>    </td>  </tr>
  <tr style="padding: 0px; margin: 0px;">    <td style="padding-top: 0px; padding-right: 10px; padding-bottom: 0px; padding-left: 10px; height: 25px; margin: 0px; border: 1px solid #6fbee7;">      是否压缩？    </td>
    <td style="padding-top: 0px; padding-right: 10px; padding-bottom: 0px; padding-left: 10px; height: 25px; margin: 0px; border: 1px solid #6fbee7;">      <span style="font-weight: bold; color: #009900; padding: 0px; margin: 0px;">是</span>    </td>  </tr>
  <tr style="padding: 0px; margin: 0px;">    <td style="padding-top: 0px; padding-right: 10px; padding-bottom: 0px; padding-left: 10px; height: 25px; margin: 0px; border: 1px solid #6fbee7;">      压缩类型：    </td>
    <td style="padding-top: 0px; padding-right: 10px; padding-bottom: 0px; padding-left: 10px; height: 25px; margin: 0px; border: 1px solid #6fbee7;">      <span style="font-weight: bold; color: #0000ff; padding: 0px; margin: 0px;">gzip</span>    </td>  </tr>
  <tr style="padding: 0px; margin: 0px;">    <td style="padding-top: 0px; padding-right: 10px; padding-bottom: 0px; padding-left: 10px; height: 25px; margin: 0px; border: 1px solid #6fbee7;">      源文件大小：    </td>
    <td style="padding-top: 0px; padding-right: 10px; padding-bottom: 0px; padding-left: 10px; height: 25px; margin: 0px; border: 1px solid #6fbee7;">      <span style="font-weight: bold; padding: 0px; margin: 0px;">40.64KB</span>    </td>  </tr>
  <tr style="padding: 0px; margin: 0px;">    <td style="padding-top: 0px; padding-right: 10px; padding-bottom: 0px; padding-left: 10px; height: 25px; margin: 0px; border: 1px solid #6fbee7;">      压缩后大小：    </td>
    <td style="padding-top: 0px; padding-right: 10px; padding-bottom: 0px; padding-left: 10px; height: 25px; margin: 0px; border: 1px solid #6fbee7;">      <span style="font-weight: bold; padding: 0px; margin: 0px;">9.98KB</span>    </td>  </tr>
  <tr style="padding: 0px; margin: 0px;">    <td style="padding-top: 0px; padding-right: 10px; padding-bottom: 0px; padding-left: 10px; height: 25px; margin: 0px; border: 1px solid #6fbee7;">      压缩率：    </td>
    <td style="padding-top: 0px; padding-right: 10px; padding-bottom: 0px; padding-left: 10px; height: 25px; margin: 0px; border: 1px solid #6fbee7;">      <span style="font-weight: bold; padding: 0px; margin: 0px;">75.4%</span>    </td>  </tr></table>
压缩得还不小吧，以前一直以为装了<span style="margin-top: 0px; margin-right: 0px; margin-bottom: 0.2em; margin-left: 0px; outline-width: 0px; outline-style: initial; outline-color: initial; background-image: initial; background-attachment: initial; background-origin: initial; background-clip: initial; background-color: transparent; word-wrap: break-word; display: block; background-position: initial initial; background-repeat: initial initial; padding: 0px; border: 0px initial initial;"><strong>WP Super Cache</strong>，并且启用了gzip就可以了，发现根本没有启用到，可能是000webhost本身的缘故吧，使用上文所写的方法就可以启用了。</span>
<span style="margin-top: 0px; margin-right: 0px; margin-bottom: 0.2em; margin-left: 0px; outline-width: 0px; outline-style: initial; outline-color: initial; background-image: initial; background-attachment: initial; background-origin: initial; background-clip: initial; background-color: transparent; word-wrap: break-word; display: block; background-position: initial initial; background-repeat: initial initial; padding: 0px; border: 0px initial initial;">开启后super cache会提示</span>
> <span style="margin-top: 0px; margin-right: 0px; margin-bottom: 0.2em; margin-left: 0px; outline-width: 0px; outline-style: initial; outline-color: initial; background-image: initial; background-attachment: initial; background-origin: initial; background-clip: initial; background-color: transparent; word-wrap: break-word; display: block; background-position: initial initial; background-repeat: initial initial; padding: 0px; border: 0px initial initial;">PHP 正在压缩发送给您网站访客的数据。建议停用此功能，因为插件会压缩一遍页面，而不是一遍又一遍压缩相同的页面。</span>
应该是说它已经一次性帮你压缩缓存成文件了，不需要每次都压缩页面（在htaccess改每访问一次都会压缩），可是插件根本没压缩啊。。没办法，只能这样了，反正效率差不了多少。