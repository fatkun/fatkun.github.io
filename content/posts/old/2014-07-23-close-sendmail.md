---
title: 关闭linux sendmail
author: fatkun
type: post
date: 2014-07-23T02:32:54+00:00
url: /2014/07/close-sendmail.html
duoshuo_thread_id:
  - 6300410318396850945
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:665:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">service <span style="color: #c20cb9; font-weight: bold;">sendmail</span> stop
    chkconfig <span style="color: #660033;">--level</span> <span style="color: #000000;">2345</span> <span style="color: #c20cb9; font-weight: bold;">sendmail</span> off
    &nbsp;
    &nbsp;
    chkconfig <span style="color: #660033;">--list</span> <span style="color: #c20cb9; font-weight: bold;">sendmail</span></pre></td></tr></table><p class="theCode" style="display:none;">service sendmail stop
    chkconfig --level 2345 sendmail off
    
    
    chkconfig --list sendmail</p></div>
    ";}
categories:
  - Linux

---
<pre escaped="true" lang="bash">service sendmail stop
chkconfig --level 2345 sendmail off


chkconfig --list sendmail </pre>
via: http://hi.baidu.com/chenhj_brenda/item/e46c6b3fdb8f03b9124b14f0