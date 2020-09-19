---
title: '[备忘]java指定一个目录加入classpath'
author: fatkun
type: post
date: 2013-04-22T02:08:15+00:00
url: /2013/04/java-dir-classpath.html
duoshuo_thread_id:
  - 6300410014905402114
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:477:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #c20cb9; font-weight: bold;">java</span> <span style="color: #660033;">-classpath</span> test.jar -Djava.ext.dirs=.<span style="color: #000000; font-weight: bold;">/</span>lib com.fatkun.Test</pre></td></tr></table><p class="theCode" style="display:none;">java -classpath test.jar -Djava.ext.dirs=./lib com.fatkun.Test</p></div>
    ";}
categories:
  - J2EE

---
<pre lang="bash" escaped="true">java -classpath test.jar -Djava.ext.dirs=./lib com.fatkun.Test</pre>