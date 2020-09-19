---
title: VSTO获取邮件联系人邮箱
author: fatkun
type: post
date: 2011-03-15T01:23:56+00:00
url: /2011/03/vsto-get-mail-recipient.html
duoshuo_thread_id:
  - 6300408803049341697
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:960:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="csharp" style="font-family:monospace;">    <span style="color: #0600FF; font-weight: bold;">public</span> <span style="color: #6666cc; font-weight: bold;">enum</span> OlMailRecipientType
        <span style="color: #008000;">&#123;</span>
            olOriginator <span style="color: #008000;">=</span> <span style="color: #FF0000;">0</span>,
            olTo <span style="color: #008000;">=</span> <span style="color: #FF0000;">1</span>,
            olCC <span style="color: #008000;">=</span> <span style="color: #FF0000;">2</span>,
            olBCC <span style="color: #008000;">=</span> <span style="color: #FF0000;">3</span>,
        <span style="color: #008000;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">    public enum OlMailRecipientType
        {
            olOriginator = 0,
            olTo = 1,
            olCC = 2,
            olBCC = 3,
        }</p></div>
    ";i:2;s:6971:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="csharp" style="font-family:monospace;">        <span style="color: #0600FF; font-weight: bold;">public</span> <span style="color: #0600FF; font-weight: bold;">static</span> List<span style="color: #008000;">&lt;</span><span style="color: #6666cc; font-weight: bold;">string</span><span style="color: #008000;">&gt;</span> GetCCAddress<span style="color: #008000;">&#40;</span>Microsoft<span style="color: #008000;">.</span><span style="color: #0000FF;">Office</span><span style="color: #008000;">.</span><span style="color: #0000FF;">Interop</span><span style="color: #008000;">.</span><span style="color: #0000FF;">Outlook</span><span style="color: #008000;">.</span><span style="color: #0000FF;">MailItem</span> mailItem<span style="color: #008000;">&#41;</span>
            <span style="color: #008000;">&#123;</span>
                List<span style="color: #008000;">&lt;</span><span style="color: #6666cc; font-weight: bold;">string</span><span style="color: #008000;">&gt;</span> addressList <span style="color: #008000;">=</span> <span style="color: #008000;">new</span> List<span style="color: #008000;">&lt;</span><span style="color: #6666cc; font-weight: bold;">string</span><span style="color: #008000;">&gt;</span><span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">;</span>
    &nbsp;
                Outlook<span style="color: #008000;">.</span><span style="color: #0000FF;">Recipients</span> recipients <span style="color: #008000;">=</span> mailItem<span style="color: #008000;">.</span><span style="color: #0000FF;">Recipients</span><span style="color: #008000;">;</span>
    &nbsp;
                <span style="color: #0600FF; font-weight: bold;">foreach</span> <span style="color: #008000;">&#40;</span>Outlook<span style="color: #008000;">.</span><span style="color: #0000FF;">Recipient</span> recipient <span style="color: #0600FF; font-weight: bold;">in</span> recipients<span style="color: #008000;">&#41;</span>
                <span style="color: #008000;">&#123;</span>
                    <span style="color: #0600FF; font-weight: bold;">if</span> <span style="color: #008000;">&#40;</span>recipient<span style="color: #008000;">.</span><span style="color: #0000FF;">Type</span> <span style="color: #008000;">!=</span> <span style="color: #FF0000;">2</span><span style="color: #008000;">&#41;</span><span style="color: #008080; font-style: italic;">//OlMailRecipientType.olCC=2</span>
                    <span style="color: #008000;">&#123;</span>
                        <span style="color: #0600FF; font-weight: bold;">continue</span><span style="color: #008000;">;</span>
                    <span style="color: #008000;">&#125;</span>
                    <span style="color: #0600FF; font-weight: bold;">if</span> <span style="color: #008000;">&#40;</span>recipient<span style="color: #008000;">.</span><span style="color: #0000FF;">Address</span> <span style="color: #008000;">!=</span> <span style="color: #0600FF; font-weight: bold;">null</span><span style="color: #008000;">&#41;</span>
                    <span style="color: #008000;">&#123;</span>
                        <span style="color: #6666cc; font-weight: bold;">string</span> addType <span style="color: #008000;">=</span> recipient<span style="color: #008000;">.</span><span style="color: #0000FF;">AddressEntry</span><span style="color: #008000;">.</span><span style="color: #0000FF;">Type</span><span style="color: #008000;">;</span>
                        <span style="color: #0600FF; font-weight: bold;">if</span> <span style="color: #008000;">&#40;</span><span style="color: #666666;">&quot;SMTP&quot;</span><span style="color: #008000;">.</span><span style="color: #0000FF;">Equals</span><span style="color: #008000;">&#40;</span>addType<span style="color: #008000;">&#41;</span><span style="color: #008000;">&#41;</span>
                        <span style="color: #008000;">&#123;</span>
                            addressList<span style="color: #008000;">.</span><span style="color: #0600FF; font-weight: bold;">Add</span><span style="color: #008000;">&#40;</span>recipient<span style="color: #008000;">.</span><span style="color: #0000FF;">Address</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">;</span>
                        <span style="color: #008000;">&#125;</span>
                        <span style="color: #0600FF; font-weight: bold;">else</span> <span style="color: #0600FF; font-weight: bold;">if</span> <span style="color: #008000;">&#40;</span><span style="color: #666666;">&quot;EX&quot;</span><span style="color: #008000;">.</span><span style="color: #0000FF;">Equals</span><span style="color: #008000;">&#40;</span>addType<span style="color: #008000;">&#41;</span><span style="color: #008000;">&#41;</span>
                        <span style="color: #008000;">&#123;</span>
                            addressList<span style="color: #008000;">.</span><span style="color: #0000FF;">AddRange</span><span style="color: #008000;">&#40;</span>GetEmailAddressForExchangeServer<span style="color: #008000;">&#40;</span>mailItem<span style="color: #008000;">.</span><span style="color: #0000FF;">Application</span>, recipient<span style="color: #008000;">.</span><span style="color: #0000FF;">Name</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">;</span>
                        <span style="color: #008000;">&#125;</span>
                    <span style="color: #008000;">&#125;</span>
                <span style="color: #008000;">&#125;</span>
    &nbsp;
                <span style="color: #0600FF; font-weight: bold;">return</span> addressList<span style="color: #008000;">;</span>
            <span style="color: #008000;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">        public static List&lt;string&gt; GetCCAddress(Microsoft.Office.Interop.Outlook.MailItem mailItem)
            {
                List&lt;string&gt; addressList = new List&lt;string&gt;();
    
                Outlook.Recipients recipients = mailItem.Recipients;
    
                foreach (Outlook.Recipient recipient in recipients)
                {
                    if (recipient.Type != 2)//OlMailRecipientType.olCC=2
                    {
                        continue;
                    }
                    if (recipient.Address != null)
                    {
                        string addType = recipient.AddressEntry.Type;
                        if (&quot;SMTP&quot;.Equals(addType))
                        {
                            addressList.Add(recipient.Address);
                        }
                        else if (&quot;EX&quot;.Equals(addType))
                        {
                            addressList.AddRange(GetEmailAddressForExchangeServer(mailItem.Application, recipient.Name));
                        }
                    }
                }
    
                return addressList;
            }</p></div>
    ";}
categories:
  - ASP.NET
tags:
  - 'C#'
  - VSTO
  - 联系人

---
C# VSTO获取邮件联系人邮箱，包括获取To,CC等  
直接从mailItem.Recipients取得所有这封邮件的联系人，然后在根据Type来判断是属于哪个的。
<pre escaped="true" lang="csharp">public enum OlMailRecipientType
    {
        olOriginator = 0,
        olTo = 1,
        olCC = 2,
        olBCC = 3,
    }</pre>
## 举例，取得CC的联系人邮箱：

<pre escaped="true" lang="csharp">public static List&lt;string&gt; GetCCAddress(Microsoft.Office.Interop.Outlook.MailItem mailItem)
        {
            List&lt;string&gt; addressList = new List&lt;string&gt;();

            Outlook.Recipients recipients = mailItem.Recipients;

            foreach (Outlook.Recipient recipient in recipients)
            {
                if (recipient.Type != 2)//OlMailRecipientType.olCC=2
                {
                    continue;
                }
                if (recipient.Address != null)
                {
                    string addType = recipient.AddressEntry.Type;
                    if ("SMTP".Equals(addType))
                    {
                        addressList.Add(recipient.Address);
                    }
                    else if ("EX".Equals(addType))
                    {
                        addressList.AddRange(GetEmailAddressForExchangeServer(mailItem.Application, recipient.Name));
                    }
                }
            }

            return addressList;
        }</pre>
参考网址：
http://msdn.microsoft.com/en-us/library/aa210995%28v=office.11%29.aspx
http://msdn.microsoft.com/en-us/library/aa219371%28v=office.11%29.aspx