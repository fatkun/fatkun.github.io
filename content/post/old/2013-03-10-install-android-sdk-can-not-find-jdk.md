---
title: 安装android sdk提示找不到JDK解决方法
author: fatkun
type: post
date: 2013-03-10T05:29:01+00:00
url: /2013/03/install-android-sdk-can-not-find-jdk.html
duoshuo_thread_id:
  - 6300410013970072322
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:825:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">Can also create symbolic <span style="color: #c20cb9; font-weight: bold;">link</span> <span style="color: #000000; font-weight: bold;">if</span> you don<span style="color: #ff0000;">'t want to copy the files. (requires administrator privileges):
    mklink C:\Windows\SysWOW64\java.exe C:\Windows\System32\java.exe
    mklink C:\Windows\SysWOW64\javaw.exe C:\Windows\System32\javaw.exe</span></pre></td></tr></table><p class="theCode" style="display:none;">Can also create symbolic link if you don't want to copy the files. (requires administrator privileges):
    mklink C:\Windows\SysWOW64\java.exe C:\Windows\System32\java.exe
    mklink C:\Windows\SysWOW64\javaw.exe C:\Windows\System32\javaw.exe</p></div>
    ";}
categories:
  - Android
tags:
  - Android
  - sdk

---
我的环境WIN7 64bit
win7可以使用mklink做软链
<pre escaped="true" lang="bash">Can also create symbolic link if you don't want to copy the files. (requires administrator privileges):
mklink C:\Windows\SysWOW64\java.exe C:\Windows\System32\java.exe
mklink C:\Windows\SysWOW64\javaw.exe C:\Windows\System32\javaw.exe</pre>
## 参考

http://stackoverflow.com/questions/4382178/android-sdk-installation-doesnt-find-jdk  
http://android-er.blogspot.com/2011/02/android-sdk-cannot-detect-jdk.html