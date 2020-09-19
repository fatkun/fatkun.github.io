---
title: 找不到管理网页和文件夹对处理方法
author: fatkun
type: post
date: 2012-01-04T14:33:23+00:00
url: /2012/01/manager-web-page.html
duoshuo_thread_id:
  - 6300408827476968194
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:4242:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="other" style="font-family:monospace;">Windows Registry Editor Version 5.00
    &nbsp;
    [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced\Folder\Thickets]
    &quot;Text&quot;=&quot;管理网页和文件夹对&quot;
    &quot;HelpID&quot;=&quot;TBD&quot;
    &quot;Type&quot;=&quot;group&quot;
    &quot;Bitmap&quot;=&quot;C:\\Windows\\system32\\\\SHELL32.DLL,4&quot;
    &nbsp;
    [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced\Folder\Thickets\AUTO]
    &quot;CheckedValue&quot;=dword:00000000
    &quot;Type&quot;=&quot;radio&quot;
    &quot;ValueName&quot;=&quot;NoFileFolderConnection&quot;
    &quot;HelpID&quot;=&quot;TBD&quot;
    &quot;Text&quot;=&quot;作为单一文件显示和管理对&quot;
    &quot;DefaultValue&quot;=dword:00000000
    &quot;RegPath&quot;=&quot;Software\\Microsoft\\Windows\\CurrentVersion\\Explorer&quot;
    &quot;HKeyRoot&quot;=dword:80000001
    &nbsp;
    [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced\Folder\Thickets\NOHIDE]
    &quot;ValueName&quot;=&quot;NoFileFolderConnection&quot;
    &quot;DefaultValue&quot;=dword:00000000
    &quot;Text&quot;=&quot;显示两部分但是作为单一文件进行管理&quot;
    &quot;RegPath&quot;=&quot;Software\\Microsoft\\Windows\\CurrentVersion\\Explorer&quot;
    &quot;HelpID&quot;=&quot;TBD&quot;
    &quot;Type&quot;=&quot;radio&quot;
    &quot;CheckedValue&quot;=dword:00000002
    &quot;HKeyRoot&quot;=dword:80000001
    &nbsp;
    [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced\Folder\Thickets\NONE]
    &quot;CheckedValue&quot;=dword:00000001
    &quot;Type&quot;=&quot;radio&quot;
    &quot;HKeyRoot&quot;=dword:80000001
    &quot;RegPath&quot;=&quot;Software\\Microsoft\\Windows\\CurrentVersion\\Explorer&quot;
    &quot;HelpID&quot;=&quot;TBD&quot;
    &quot;ValueName&quot;=&quot;NoFileFolderConnection&quot;
    &quot;DefaultValue&quot;=dword:00000000
    &quot;Text&quot;=&quot;显示两部分并分别进行管理&quot;
    &nbsp;
    [HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer]
    &quot;NoFileFolderConnection&quot;=dword:00000001</pre></td></tr></table><p class="theCode" style="display:none;">Windows Registry Editor Version 5.00
    
    [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced\Folder\Thickets]
    &quot;Text&quot;=&quot;管理网页和文件夹对&quot;
    &quot;HelpID&quot;=&quot;TBD&quot;
    &quot;Type&quot;=&quot;group&quot;
    &quot;Bitmap&quot;=&quot;C:\\Windows\\system32\\\\SHELL32.DLL,4&quot;
    
    [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced\Folder\Thickets\AUTO]
    &quot;CheckedValue&quot;=dword:00000000
    &quot;Type&quot;=&quot;radio&quot;
    &quot;ValueName&quot;=&quot;NoFileFolderConnection&quot;
    &quot;HelpID&quot;=&quot;TBD&quot;
    &quot;Text&quot;=&quot;作为单一文件显示和管理对&quot;
    &quot;DefaultValue&quot;=dword:00000000
    &quot;RegPath&quot;=&quot;Software\\Microsoft\\Windows\\CurrentVersion\\Explorer&quot;
    &quot;HKeyRoot&quot;=dword:80000001
    
    [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced\Folder\Thickets\NOHIDE]
    &quot;ValueName&quot;=&quot;NoFileFolderConnection&quot;
    &quot;DefaultValue&quot;=dword:00000000
    &quot;Text&quot;=&quot;显示两部分但是作为单一文件进行管理&quot;
    &quot;RegPath&quot;=&quot;Software\\Microsoft\\Windows\\CurrentVersion\\Explorer&quot;
    &quot;HelpID&quot;=&quot;TBD&quot;
    &quot;Type&quot;=&quot;radio&quot;
    &quot;CheckedValue&quot;=dword:00000002
    &quot;HKeyRoot&quot;=dword:80000001
    
    [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced\Folder\Thickets\NONE]
    &quot;CheckedValue&quot;=dword:00000001
    &quot;Type&quot;=&quot;radio&quot;
    &quot;HKeyRoot&quot;=dword:80000001
    &quot;RegPath&quot;=&quot;Software\\Microsoft\\Windows\\CurrentVersion\\Explorer&quot;
    &quot;HelpID&quot;=&quot;TBD&quot;
    &quot;ValueName&quot;=&quot;NoFileFolderConnection&quot;
    &quot;DefaultValue&quot;=dword:00000000
    &quot;Text&quot;=&quot;显示两部分并分别进行管理&quot;
    
    [HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer]
    &quot;NoFileFolderConnection&quot;=dword:00000001</p></div>
    ";}
categories:
  - 电脑知识
tags:
  - windows

---
把下面内容保存为aa.reg文件，双击运行导入  
（未测试是否成功，注册表从我电脑导出的,WIN7和XP应该是一样可以用的）
<pre escaped="true" lang="other">Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced\Folder\Thickets]
"Text"="管理网页和文件夹对"
"HelpID"="TBD"
"Type"="group"
"Bitmap"="C:\\Windows\\system32\\\\SHELL32.DLL,4"

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced\Folder\Thickets\AUTO]
"CheckedValue"=dword:00000000
"Type"="radio"
"ValueName"="NoFileFolderConnection"
"HelpID"="TBD"
"Text"="作为单一文件显示和管理对"
"DefaultValue"=dword:00000000
"RegPath"="Software\\Microsoft\\Windows\\CurrentVersion\\Explorer"
"HKeyRoot"=dword:80000001

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced\Folder\Thickets\NOHIDE]
"ValueName"="NoFileFolderConnection"
"DefaultValue"=dword:00000000
"Text"="显示两部分但是作为单一文件进行管理"
"RegPath"="Software\\Microsoft\\Windows\\CurrentVersion\\Explorer"
"HelpID"="TBD"
"Type"="radio"
"CheckedValue"=dword:00000002
"HKeyRoot"=dword:80000001

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced\Folder\Thickets\NONE]
"CheckedValue"=dword:00000001
"Type"="radio"
"HKeyRoot"=dword:80000001
"RegPath"="Software\\Microsoft\\Windows\\CurrentVersion\\Explorer"
"HelpID"="TBD"
"ValueName"="NoFileFolderConnection"
"DefaultValue"=dword:00000000
"Text"="显示两部分并分别进行管理"

[HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer]
"NoFileFolderConnection"=dword:00000001
</pre>