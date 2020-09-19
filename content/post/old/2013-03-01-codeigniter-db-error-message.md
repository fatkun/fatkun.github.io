---
title: codeigniter数据库错误信息获取
author: fatkun
type: post
date: 2013-03-01T07:37:35+00:00
url: /2013/03/codeigniter-db-error-message.html
duoshuo_thread_id:
  - 6300409442038973185
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:1305:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="php" style="font-family:monospace;">Yes<span style="color: #339933;">,</span> this is the <span style="color: #990000;">mysql_error</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> wrapper<span style="color: #339933;">.</span>
    &nbsp;
    <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">db</span><span style="color: #339933;">-&gt;</span>_error_message<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    And the <span style="color: #990000;">mysql_errno</span> wrapper is<span style="color: #339933;">:</span>
    &nbsp;
    <span style="color: #000088;">$this</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">db</span><span style="color: #339933;">-&gt;</span>_error_number<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span></pre></td></tr></table><p class="theCode" style="display:none;">Yes, this is the mysql_error() wrapper.
    
    $this-&gt;db-&gt;_error_message();
    And the mysql_errno wrapper is:
    
    $this-&gt;db-&gt;_error_number();</p></div>
    ";}
categories:
  - 网页前端
tags:
  - codeigniter
  - php

---
db_debug &#8211; TRUE/FALSE (boolean) &#8211; Whether database errors should be displayed.  
需要设置db_debug = false
<pre escaped="true" lang="php">Yes, this is the mysql_error() wrapper.

$this-&gt;db-&gt;_error_message();
And the mysql_errno wrapper is:

$this-&gt;db-&gt;_error_number();</pre>
via:  
http://stackoverflow.com/questions/3234564/under-codeigniter-is-it-possible-to-see-mysql-error