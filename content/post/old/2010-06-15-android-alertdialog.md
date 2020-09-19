---
title: Android-AlertDialog(警告窗口)例子
author: fatkun
type: post
date: 2010-06-15T11:14:29+00:00
url: /2010/06/android-alertdialog.html
views:
  - 8
duoshuo_thread_id:
  - 6300408732232712961
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:4035:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">new</span> AlertDialog.<span style="color: #006633;">Builder</span><span style="color: #009900;">&#40;</span>TestActivity.<span style="color: #000000; font-weight: bold;">this</span><span style="color: #009900;">&#41;</span><span style="color: #666666; font-style: italic;">//Context</span>
    .<span style="color: #006633;">setTitle</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;标题啊&quot;</span><span style="color: #009900;">&#41;</span>
    .<span style="color: #006633;">setIcon</span><span style="color: #009900;">&#40;</span>android.<span style="color: #006633;">R</span>.<span style="color: #006633;">drawable</span>.<span style="color: #006633;">ic_dialog_alert</span><span style="color: #009900;">&#41;</span><span style="color: #666666; font-style: italic;">//图标</span>
    .<span style="color: #006633;">setMessage</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;内容&quot;</span><span style="color: #009900;">&#41;</span>
    .<span style="color: #006633;">setNegativeButton</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;取消&quot;</span>,<span style="color: #000000; font-weight: bold;">new</span> DialogInterface.<span style="color: #006633;">OnClickListener</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span><span style="color: #666666; font-style: italic;">//按钮1</span>
    	<span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> onClick<span style="color: #009900;">&#40;</span>DialogInterface arg0, <span style="color: #000066; font-weight: bold;">int</span> arg1<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    	<span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span><span style="color: #009900;">&#41;</span>
    .<span style="color: #006633;">setPositiveButton</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;确定&quot;</span>, <span style="color: #000000; font-weight: bold;">new</span> DialogInterface.<span style="color: #006633;">OnClickListener</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span><span style="color: #666666; font-style: italic;">//按钮2</span>
    	<span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> onClick<span style="color: #009900;">&#40;</span>DialogInterface arg0, <span style="color: #000066; font-weight: bold;">int</span> arg1<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    		finish<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">show</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//显示</span></pre></td></tr></table><p class="theCode" style="display:none;">new AlertDialog.Builder(TestActivity.this)//Context
    .setTitle(&quot;标题啊&quot;)
    .setIcon(android.R.drawable.ic_dialog_alert)//图标
    .setMessage(&quot;内容&quot;)
    .setNegativeButton(&quot;取消&quot;,new DialogInterface.OnClickListener() {//按钮1
    	public void onClick(DialogInterface arg0, int arg1) {
    	}
    })
    .setPositiveButton(&quot;确定&quot;, new DialogInterface.OnClickListener() {//按钮2
    	public void onClick(DialogInterface arg0, int arg1) {
    		finish();
    	}
    }).show();//显示</p></div>
    ";}
categories:
  - Android
  - J2EE
tags:
  - Android

---
Android-AlertDialog(警告窗口)的一个例子  
[![php1DUUrR][1]][2]{.flickr-image.alignnone}
<pre escaped="true" lang="java">new AlertDialog.Builder(TestActivity.this)//Context
.setTitle("标题啊")
.setIcon(android.R.drawable.ic_dialog_alert)//图标
.setMessage("内容")
.setNegativeButton("取消",new DialogInterface.OnClickListener() {//按钮1
	public void onClick(DialogInterface arg0, int arg1) {
	}
})
.setPositiveButton("确定", new DialogInterface.OnClickListener() {//按钮2
	public void onClick(DialogInterface arg0, int arg1) {
		finish();
	}
}).show();//显示</pre>

 [1]: http://farm5.static.flickr.com/4021/4702425695_95c2d9a5cc.jpg
 [2]: http://www.flickr.com/photos/fatkun/4702425695/ "php1DUUrR"