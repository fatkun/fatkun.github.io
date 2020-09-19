---
title: Ext.util.DelayedTask很好用
author: fatkun
type: post
date: 2012-12-22T11:51:27+00:00
url: /2012/12/ext-util-delayedtask.html
duoshuo_thread_id:
  - 6300409441657291522
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:590:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="js" style="font-family:monospace;">var task = new Ext.util.DelayedTask(function(){
        alert(Ext.getDom('myInputField').value.length);
    });
    &nbsp;
    &nbsp;
    Ext.get('myInputField').on('keypress', function(){
        task.delay(500); 
    });</pre></td></tr></table><p class="theCode" style="display:none;">var task = new Ext.util.DelayedTask(function(){
        alert(Ext.getDom('myInputField').value.length);
    });
    
    
    Ext.get('myInputField').on('keypress', function(){
        task.delay(500); 
    });</p></div>
    ";}
categories:
  - jquery
tags:
  - extjs
  - extjs3.x

---
Ext3.x有个这个类Ext.util.DelayedTask，  
实现好简单。。做个定时器，如果还没执行又被触发就取消上一个定时器。。  
应用场景在于想要延迟搜索，触发了keyup事件，但如果连续输入了N个字母，可不希望过滤N次，只需要过滤一次就够了。  
可以在new的时候指定scope
<pre escaped="true" lang="js">var task = new Ext.util.DelayedTask(function(){
    alert(Ext.getDom('myInputField').value.length);
});


Ext.get('myInputField').on('keypress', function(){
    task.delay(500); 
});
</pre>