---
title: 编译hive cdh5.4.0
author: fatkun
type: post
date: 2015-07-23T03:17:06+00:00
url: /2015/07/compile-hive-cdh5-4-0.html
duoshuo_thread_id:
  - 6300410896057369346
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:296:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="html" style="font-family:monospace;">mvn clean install -Phadoop-2,dist  -DskipTests</pre></td></tr></table><p class="theCode" style="display:none;">mvn clean install -Phadoop-2,dist  -DskipTests</p></div>
    ";}
categories:
  - 未分类

---
编译命令
<pre escaped="true" lang="html">mvn clean install -Phadoop-2,dist  -DskipTests</pre>
https://cwiki.apache.org/confluence/display/Hive/GettingStarted#GettingStarted-BuildingHivefromSource