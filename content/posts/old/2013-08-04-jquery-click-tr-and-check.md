---
title: jquery选择行(tr)勾选checkbox（避免冲突）
author: fatkun
type: post
date: 2013-08-04T08:01:54+00:00
url: /2013/08/jquery-click-tr-and-check.html
duoshuo_thread_id:
  - 6300410024426472193
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:1457:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="js" style="font-family:monospace;">    $(&quot;#album_list input.checkall&quot;).click(function(event) {
            //prop 需要jquery1.6+才支持
            $(&quot;#album_list input.chk_album&quot;).prop(&quot;checked&quot;, $(this).prop(&quot;checked&quot;));
        });
    &nbsp;
        $(&quot;#album_list tr&quot;).click(function(event) {
            var isCheckbox = $(event.target).is(&quot;:checkbox&quot;); // 判断是否是checkbox本身
            if (!isCheckbox) {
                var chk = $(this).find(&quot;.chk_album&quot;);
                if (chk) {
                    chk.prop(&quot;checked&quot;, !chk.prop(&quot;checked&quot;));
                }
            }
        });</pre></td></tr></table><p class="theCode" style="display:none;">    $(&quot;#album_list input.checkall&quot;).click(function(event) {
            //prop 需要jquery1.6+才支持
            $(&quot;#album_list input.chk_album&quot;).prop(&quot;checked&quot;, $(this).prop(&quot;checked&quot;));
        });
    
        $(&quot;#album_list tr&quot;).click(function(event) {
            var isCheckbox = $(event.target).is(&quot;:checkbox&quot;); // 判断是否是checkbox本身
            if (!isCheckbox) {
                var chk = $(this).find(&quot;.chk_album&quot;);
                if (chk) {
                    chk.prop(&quot;checked&quot;, !chk.prop(&quot;checked&quot;));
                }
            }
        });</p></div>
    ";}
categories:
  - jquery
tags:
  - jquery
  - 多选框

---
一般情况下点击行可以勾选多选框，但直接点勾选框会因为事件的冒泡导致再点击了一次。。  
解决方法是判断最初点击的是不是checkbox
来源是：http://stackoverflow.com/, 找不回网址了。。
<pre escaped="true" lang="js">$("#album_list input.checkall").click(function(event) {
        //prop 需要jquery1.6+才支持
        $("#album_list input.chk_album").prop("checked", $(this).prop("checked"));
    });

    $("#album_list tr").click(function(event) {
        var isCheckbox = $(event.target).is(":checkbox"); // 判断是否是checkbox本身
        if (!isCheckbox) {
            var chk = $(this).find(".chk_album");
            if (chk) {
                chk.prop("checked", !chk.prop("checked"));
            }
        }
    });</pre>