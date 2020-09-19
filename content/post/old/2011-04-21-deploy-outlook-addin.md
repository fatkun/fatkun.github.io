---
title: 部署outlook2003插件
author: fatkun
type: post
date: 2011-04-21T03:53:29+00:00
url: /2011/04/deploy-outlook-addin.html
duoshuo_thread_id:
  - 6300408813023396610
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:3614:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="csharp" style="font-family:monospace;"><span style="color: #008080; font-style: italic;">//找到这句</span>
    <span style="color: #6666cc; font-weight: bold;">string</span> arguments <span style="color: #008000;">=</span> policyLevel <span style="color: #008000;">+</span> <span style="color: #666666;">&quot; -q -ag &quot;</span> <span style="color: #008000;">+</span> parentCodeGroup <span style="color: #008000;">+</span> <span style="color: #666666;">&quot; -url <span style="color: #008080; font-weight: bold;">\&quot;</span>&quot;</span> <span style="color: #008000;">+</span> solutionInstallationUrl <span style="color: #008000;">+</span> <span style="color: #666666;">&quot;<span style="color: #008080; font-weight: bold;">\&quot;</span> Nothing -n <span style="color: #008080; font-weight: bold;">\&quot;</span>&quot;</span> <span style="color: #008000;">+</span> solutionCodeGroupName <span style="color: #008000;">+</span> <span style="color: #666666;">&quot;<span style="color: #008080; font-weight: bold;">\&quot;</span> -d <span style="color: #008080; font-weight: bold;">\&quot;</span>&quot;</span> <span style="color: #008000;">+</span> solutionCodeGroupDescription <span style="color: #008000;">+</span> <span style="color: #666666;">&quot;<span style="color: #008080; font-weight: bold;">\&quot;</span>&quot;</span><span style="color: #008000;">;</span>
    &nbsp;
    <span style="color: #008080; font-style: italic;">//把Nothing改为FullTrust，其实就是把这个目录的所有文件都信任了</span>
    <span style="color: #6666cc; font-weight: bold;">string</span> arguments <span style="color: #008000;">=</span> policyLevel <span style="color: #008000;">+</span> <span style="color: #666666;">&quot; -q -ag &quot;</span> <span style="color: #008000;">+</span> parentCodeGroup <span style="color: #008000;">+</span> <span style="color: #666666;">&quot; -url <span style="color: #008080; font-weight: bold;">\&quot;</span>&quot;</span> <span style="color: #008000;">+</span> solutionInstallationUrl <span style="color: #008000;">+</span> <span style="color: #666666;">&quot;<span style="color: #008080; font-weight: bold;">\&quot;</span> FullTrust -n <span style="color: #008080; font-weight: bold;">\&quot;</span>&quot;</span> <span style="color: #008000;">+</span> solutionCodeGroupName <span style="color: #008000;">+</span> <span style="color: #666666;">&quot;<span style="color: #008080; font-weight: bold;">\&quot;</span> -d <span style="color: #008080; font-weight: bold;">\&quot;</span>&quot;</span> <span style="color: #008000;">+</span> solutionCodeGroupDescription <span style="color: #008000;">+</span> <span style="color: #666666;">&quot;<span style="color: #008080; font-weight: bold;">\&quot;</span>&quot;</span><span style="color: #008000;">;</span></pre></td></tr></table><p class="theCode" style="display:none;">//找到这句
    string arguments = policyLevel + &quot; -q -ag &quot; + parentCodeGroup + &quot; -url \&quot;&quot; + solutionInstallationUrl + &quot;\&quot; Nothing -n \&quot;&quot; + solutionCodeGroupName + &quot;\&quot; -d \&quot;&quot; + solutionCodeGroupDescription + &quot;\&quot;&quot;;
    
    //把Nothing改为FullTrust，其实就是把这个目录的所有文件都信任了
    string arguments = policyLevel + &quot; -q -ag &quot; + parentCodeGroup + &quot; -url \&quot;&quot; + solutionInstallationUrl + &quot;\&quot; FullTrust -n \&quot;&quot; + solutionCodeGroupName + &quot;\&quot; -d \&quot;&quot; + solutionCodeGroupDescription + &quot;\&quot;&quot;;</p></div>
    ";}
categories:
  - ASP.NET
tags:
  - deploy
  - outlook
  - outlook addin
  - 部署插件

---
如果你的插件部署失败，很可能是没有信任的原因，请参考下面的文章吧。
## 问题

outlook addin 部署成功了，但打死不能切换语言，无论切换哪个都是英文。（多语言是通过ResourceManager读取的）
## 解决方法

原因是资源文件是放在子目录下的dll文件，例如&#8221;zh-CN\xxx.resource.dll&#8221;，这些dll并没有授权。  
你可以在 VS的命令行中输入 “caspol -lg” 列出所有授权的组。  
如果你是按照MSDN的文章进行部署，你应该会有个CaspolSecurityPolicyCreator.cs的文件用于授权。
<pre escaped="true" lang="csharp">//找到这句
string arguments = policyLevel + " -q -ag " + parentCodeGroup + " -url \"" + solutionInstallationUrl + "\" Nothing -n \"" + solutionCodeGroupName + "\" -d \"" + solutionCodeGroupDescription + "\"";

//把Nothing改为FullTrust，其实就是把这个目录的所有文件都信任了
string arguments = policyLevel + " -q -ag " + parentCodeGroup + " -url \"" + solutionInstallationUrl + "\" FullTrust -n \"" + solutionCodeGroupName + "\" -d \"" + solutionCodeGroupDescription + "\"";
</pre>
如果你没有上面这个文件（其实这个文件也是调用caspol.exe来授权的），可以尝试自己来运行caspol.exe -m -ag &#8230;来授权。
## 参考文章

[Outlook 2003 Add in 部署笔记][1]  
[Deploying Visual Studio 2005 Tools for the Office System SE Solutions Using Windows Installer (Part 1 of 2)][2]

 [1]: http://www.cnblogs.com/bluewelkin/archive/2008/09/03/1283231.html
 [2]: http://msdn.microsoft.com/zh-cn/library/bb332051(v=office.12).aspx