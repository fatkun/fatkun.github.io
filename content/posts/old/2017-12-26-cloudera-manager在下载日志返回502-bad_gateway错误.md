---
title: cloudera manager在下载日志返回502 BAD_GATEWAY错误
author: fatkun
type: post
date: 2017-12-26T10:00:52+00:00
url: /2017/12/cloudera-manager在下载日志返回502-bad_gateway错误.html
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:2666:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;">    <span style="color: #808080; font-style: italic;"># Simple blacklist of path prefixes that are not reasonable for log locations</span>
        path_blacklist <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span> <span style="color: #483d8b;">&quot;/boot/&quot;</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">&quot;/etc/&quot;</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">&quot;/usr/&quot;</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">&quot;/lib/&quot;</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">&quot;/lib64/&quot;</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">&quot;/home/&quot;</span><span style="color: #66cc66;">,</span>
                           <span style="color: #483d8b;">&quot;/root/&quot;</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">&quot;/sys/&quot;</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">&quot;/proc/&quot;</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">&quot;/dev/&quot;</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">&quot;/bin/&quot;</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">&quot;/sbin/&quot;</span> <span style="color: black;">&#93;</span>
    &nbsp;
        fd <span style="color: #66cc66;">=</span> <span style="color: #008000;">self</span>._validate_and_open<span style="color: black;">&#40;</span>new_log_file_path<span style="color: #66cc66;">,</span>
                                     restrict_to_parent_path<span style="color: #66cc66;">=</span><span style="color: #008000;">False</span><span style="color: #66cc66;">,</span>
                                     path_blacklist<span style="color: #66cc66;">=</span>path_blacklist<span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">    # Simple blacklist of path prefixes that are not reasonable for log locations
        path_blacklist = [ &quot;/boot/&quot;, &quot;/etc/&quot;, &quot;/usr/&quot;, &quot;/lib/&quot;, &quot;/lib64/&quot;, &quot;/home/&quot;,
                           &quot;/root/&quot;, &quot;/sys/&quot;, &quot;/proc/&quot;, &quot;/dev/&quot;, &quot;/bin/&quot;, &quot;/sbin/&quot; ]
    
        fd = self._validate_and_open(new_log_file_path,
                                     restrict_to_parent_path=False,
                                     path_blacklist=path_blacklist)</p></div>
    ";}
categories:
  - hadoop
tags:
  - cloudera

---
下载日志是通过status\_server.py的download\_log方法进行的
/usr/lib64/cmf/agent/build/env/lib/python2.6/site-packages/cmf-5.13.1-py2.6.egg/cmf/status_server.py
如果日志目录包含以下开头就禁止下载
<pre escaped="true" lang="python"># Simple blacklist of path prefixes that are not reasonable for log locations
    path_blacklist = [ "/boot/", "/etc/", "/usr/", "/lib/", "/lib64/", "/home/",
                       "/root/", "/sys/", "/proc/", "/dev/", "/bin/", "/sbin/" ]

    fd = self._validate_and_open(new_log_file_path,
                                 restrict_to_parent_path=False,
                                 path_blacklist=path_blacklist)</pre>