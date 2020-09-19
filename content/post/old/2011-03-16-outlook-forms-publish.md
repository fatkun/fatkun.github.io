---
title: Outlook自定义窗体自动发布
author: fatkun
type: post
date: 2011-03-16T01:20:42+00:00
url: /2011/03/outlook-forms-publish.html
duoshuo_thread_id:
  - 6300408803099673346
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:2636:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="vbs" style="font-family:monospace;">Sub PublishForm(objOL, olns, strPath, trueName, displayName, folderId)
        Dim objItem     ' As Outlook.ContactItem
        Dim objFD       ' As Outlook.FormDescription
        Dim MyFolder
        Const olPersonalRegistry = 2
        Const olFolderRegistry = 3
        Const olDiscard = 1
    &nbsp;
        Set objItem = objOL.CreateItemFromTemplate(strPath)
        Set objFD = objItem.FormDescription
        Set MyFolder = olns.GetDefaultFolder(folderId)
        With objFD
        	.Name = trueName
            .DisplayName = displayName
            .PublishForm olFolderRegistry, MyFolder '请参考msdn，olPersonalRegistry 是发布到personal文件夹
        End With
        objItem.Close olDiscard
    &nbsp;
        Set objFD = Nothing
        Set objItem = Nothing
    End Sub
    &nbsp;
    Const olFolderCalendar = 9
    Const olFolderTasks = 13
    Dim path
    '取得当前位置
    path = createobject(&quot;Scripting.FileSystemObject&quot;).GetFolder(&quot;.&quot;).Path+&quot;\&quot;
    Dim objOL,olns
    Set objOL = CreateObject(&quot;Outlook.Application&quot;)
    Set olns = objOL.GetNameSpace(&quot;MAPI&quot;)
    &nbsp;
    Call PublishForm(objOL, olns, path+&quot;Activity.oft&quot;,&quot;命名&quot;,&quot;显示名称&quot;,olFolderTasks)
    &nbsp;
    Set objOL = Nothing
    Set olns = Nothing</pre></td></tr></table><p class="theCode" style="display:none;">Sub PublishForm(objOL, olns, strPath, trueName, displayName, folderId)
        Dim objItem     ' As Outlook.ContactItem
        Dim objFD       ' As Outlook.FormDescription
        Dim MyFolder
        Const olPersonalRegistry = 2
        Const olFolderRegistry = 3
        Const olDiscard = 1
    
        Set objItem = objOL.CreateItemFromTemplate(strPath)
        Set objFD = objItem.FormDescription
        Set MyFolder = olns.GetDefaultFolder(folderId)
        With objFD
        	.Name = trueName
            .DisplayName = displayName
            .PublishForm olFolderRegistry, MyFolder '请参考msdn，olPersonalRegistry 是发布到personal文件夹
        End With
        objItem.Close olDiscard
    
        Set objFD = Nothing
        Set objItem = Nothing
    End Sub
    
    Const olFolderCalendar = 9
    Const olFolderTasks = 13
    Dim path
    '取得当前位置
    path = createobject(&quot;Scripting.FileSystemObject&quot;).GetFolder(&quot;.&quot;).Path+&quot;\&quot;
    Dim objOL,olns
    Set objOL = CreateObject(&quot;Outlook.Application&quot;)
    Set olns = objOL.GetNameSpace(&quot;MAPI&quot;)
    
    Call PublishForm(objOL, olns, path+&quot;Activity.oft&quot;,&quot;命名&quot;,&quot;显示名称&quot;,olFolderTasks)
    
    Set objOL = Nothing
    Set olns = Nothing</p></div>
    ";}
categories:
  - 未分类
tags:
  - forms
  - outlook
  - 窗体
  - 自定义窗体

---
一般来说，我们都是把窗体“另存为”一个.oft的文件，然后如果要发布给很多人，一个是发布到exchange server上大家共用，一个是只发布到自己。
通常是使用“工具->窗体->发布窗体”来进行发布，但是如果窗体很多。。而且每个人都要发布。。那就挺麻烦的。
## 实现代码

把下面的代码保存为xxx.vbs文件，放到.oft同一个目录就可以自动发布了。当然，你可以要相应修改一下
<pre escaped="true" lang="vbs">Sub PublishForm(objOL, olns, strPath, trueName, displayName, folderId)
    Dim objItem     ' As Outlook.ContactItem
    Dim objFD       ' As Outlook.FormDescription
    Dim MyFolder
    Const olPersonalRegistry = 2
    Const olFolderRegistry = 3
    Const olDiscard = 1

    Set objItem = objOL.CreateItemFromTemplate(strPath)
    Set objFD = objItem.FormDescription
    Set MyFolder = olns.GetDefaultFolder(folderId)
    With objFD
    	.Name = trueName
        .DisplayName = displayName
        .PublishForm olFolderRegistry, MyFolder '请参考msdn，olPersonalRegistry 是发布到personal文件夹
    End With
    objItem.Close olDiscard

    Set objFD = Nothing
    Set objItem = Nothing
End Sub

Const olFolderCalendar = 9
Const olFolderTasks = 13
Dim path
'取得当前位置
path = createobject("Scripting.FileSystemObject").GetFolder(".").Path+"\"
Dim objOL,olns
Set objOL = CreateObject("Outlook.Application")
Set olns = objOL.GetNameSpace("MAPI")

Call PublishForm(objOL, olns, path+"Activity.oft","命名","显示名称",olFolderTasks)

Set objOL = Nothing
Set olns = Nothing</pre>
## 参考文章

[To distribute Microsoft Outlook forms to other users][1]
<span style="font-family: Verdana, Arial, Helvetica; font-size: small;"><a href="http://www.outlookexchange.com/articles/home/wisniewski01.asp">Automating the Installation of Outlook Forms for off-line users</a></span>
<span style="font-family: Verdana, Arial, Helvetica; font-size: small;"><a href="http://www.txsz.net/xs/delphi/3/Outlook%20TypeLib%28MSOUTL9.OLB%29.htm">http://www.txsz.net/xs/delphi/3/Outlook%20TypeLib%28MSOUTL9.OLB%29.htm</a><br /> </span>  
[FormDescription.PublishForm Method][2]

 [1]: http://www.outlookcode.com/article.aspx?id=27
 [2]: http://msdn.microsoft.com/zh-cn/library/microsoft.office.interop.outlook.formdescription.publishform.aspx