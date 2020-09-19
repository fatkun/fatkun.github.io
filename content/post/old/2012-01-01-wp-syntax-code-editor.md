---
title: WP-Syntax代码编辑器插件
author: fatkun
type: post
date: 2012-01-01T07:54:49+00:00
url: /2012/01/wp-syntax-code-editor.html
duoshuo_thread_id:
  - 6300408827359527682
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:7049:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="js" style="font-family:monospace;">&lt;?php
    /*
    Plugin Name: WP-Syntax Code Editor
    Plugin URI: http://fatkun.com/2012/01/wp-syntax-code-editor.html
    Description: 在编辑框加入一个插入wp-syntax代码的按钮，修改自syntax-highlighter-with-add-button-in-editor（原作者leo108）
    Version: 1.0.0
    Original Author: leo108
    Author URI: http://fatkun.com/
    */
    function codebox_init(){
    ?&gt;
    &lt;div id=&quot;codebox&quot; class=&quot;meta-box-sortables ui-sortable&quot; style=&quot;position: relative;&quot;&gt;&lt;div class=&quot;postbox&quot;&gt;
    &lt;div class=&quot;handlediv&quot; title=&quot;Click to toggle&quot;&gt;&lt;/div&gt;
    &lt;h3 class=&quot;hndle&quot;&gt;&lt;span&gt;WP-Syntax&lt;/span&gt;&lt;/h3&gt;
    &lt;div class=&quot;inside&quot;&gt;
    Language:
    &lt;select id=&quot;language&quot;&gt;
    	&lt;option value=&quot;other&quot;&gt;Other&lt;/option&gt;
    	&lt;option value=&quot;bash&quot;&gt;Bash&lt;/option&gt;
    	&lt;option value=&quot;c&quot;&gt;C&lt;/option&gt;
    	&lt;option value=&quot;cpp&quot;&gt;C++&lt;/option&gt;
    	&lt;option value=&quot;csharp&quot;&gt;C#&lt;/option&gt;
    	&lt;option value=&quot;css&quot;&gt;CSS&lt;/option&gt;
    	&lt;option value=&quot;delphi&quot;&gt;Delphi&lt;/option&gt;
    	&lt;option value=&quot;diff&quot;&gt;Diff&lt;/option&gt;
    	&lt;option value=&quot;erl&quot;&gt;Erlang&lt;/option&gt;
    	&lt;option value=&quot;groovy&quot;&gt;Groovy&lt;/option&gt;
    	&lt;option value=&quot;html&quot;&gt;HTML&lt;/option&gt;
    	&lt;option value=&quot;java&quot;&gt;Java&lt;/option&gt;
    	&lt;option value=&quot;js&quot;&gt;Javascript&lt;/option&gt;
    	&lt;option value=&quot;perl&quot;&gt;Perl&lt;/option&gt;
    	&lt;option value=&quot;php&quot;&gt;PHP&lt;/option&gt;
        &lt;option value=&quot;ps&quot;&gt;PowerShell&lt;/option&gt;
    	&lt;option value=&quot;python&quot;&gt;Python&lt;/option&gt;
    	&lt;option value=&quot;ruby&quot;&gt;Ruby&lt;/option&gt;
    	&lt;option value=&quot;sql&quot;&gt;SQL&lt;/option&gt;
    	&lt;option value=&quot;vb&quot;&gt;VisualBasic&lt;/option&gt;
    	&lt;option value=&quot;vb&quot;&gt;VB.NET&lt;/option&gt;
    	&lt;option value=&quot;xml&quot;&gt;XML&lt;/option&gt;
    &lt;/select&gt;
    &lt;br&gt;
    Code:&lt;br&gt;&lt;textarea id=&quot;code&quot; rows=&quot;8&quot; cols=&quot;70&quot; style=&quot;width:97%;&quot;&gt;&lt;/textarea&gt;&lt;br&gt;
    &lt;input type=&quot;button&quot; value=&quot;INSERT&quot; onclick=&quot;javascript:settext();&quot;&gt;
    &nbsp;
    &lt;script&gt;
    function settext()
    { 
    	var str='&lt;pre escaped=&quot;true&quot; lang=&quot;';
    	var lang=document.getElementById(&quot;language&quot;).value;
    	var code=document.getElementById(&quot;code&quot;).value;
    	str=str+lang;
    	str=str+'&quot;&gt;';
    	str=str+filter(code)+&quot;&lt;/pre&gt;&quot;;
    	var win = window.dialogArguments ¦¦ opener ¦¦ parent ¦¦ top;
    	win.send_to_editor(str);
    	document.getElementById(&quot;code&quot;).value=&quot;&quot;;
    }
    function filter (str) {
    	str = str.replace(/&amp;/g, '&amp;amp;');
    	str = str.replace(/&lt;/g, '&amp;lt;');
    	str = str.replace(/&gt;/g, '&amp;gt;');
    	str = str.replace(/'/g, '&amp;#39;');
    	str = str.replace(/&quot;/g, '&amp;quot;');
    	str = str.replace(/\¦/g, '&amp;brvbar;');
    	return str;
    }
    &lt;/script&gt;
    &lt;/div&gt;&lt;/div&gt;&lt;/div&gt;
    &lt;script&gt;document.getElementById(&quot;postdivrich&quot;).appendChild(document.getElementById(&quot;codebox&quot;));&lt;/script&gt;
    &lt;?php
    }
    add_action('dbx_post_sidebar','codebox_init');
    ?&gt;</pre></td></tr></table><p class="theCode" style="display:none;">&lt;?php
    /*
    Plugin Name: WP-Syntax Code Editor
    Plugin URI: http://fatkun.com/2012/01/wp-syntax-code-editor.html
    Description: 在编辑框加入一个插入wp-syntax代码的按钮，修改自syntax-highlighter-with-add-button-in-editor（原作者leo108）
    Version: 1.0.0
    Original Author: leo108
    Author URI: http://fatkun.com/
    */
    function codebox_init(){
    ?&gt;
    &lt;div id=&quot;codebox&quot; class=&quot;meta-box-sortables ui-sortable&quot; style=&quot;position: relative;&quot;&gt;&lt;div class=&quot;postbox&quot;&gt;
    &lt;div class=&quot;handlediv&quot; title=&quot;Click to toggle&quot;&gt;&lt;/div&gt;
    &lt;h3 class=&quot;hndle&quot;&gt;&lt;span&gt;WP-Syntax&lt;/span&gt;&lt;/h3&gt;
    &lt;div class=&quot;inside&quot;&gt;
    Language:
    &lt;select id=&quot;language&quot;&gt;
    	&lt;option value=&quot;other&quot;&gt;Other&lt;/option&gt;
    	&lt;option value=&quot;bash&quot;&gt;Bash&lt;/option&gt;
    	&lt;option value=&quot;c&quot;&gt;C&lt;/option&gt;
    	&lt;option value=&quot;cpp&quot;&gt;C++&lt;/option&gt;
    	&lt;option value=&quot;csharp&quot;&gt;C#&lt;/option&gt;
    	&lt;option value=&quot;css&quot;&gt;CSS&lt;/option&gt;
    	&lt;option value=&quot;delphi&quot;&gt;Delphi&lt;/option&gt;
    	&lt;option value=&quot;diff&quot;&gt;Diff&lt;/option&gt;
    	&lt;option value=&quot;erl&quot;&gt;Erlang&lt;/option&gt;
    	&lt;option value=&quot;groovy&quot;&gt;Groovy&lt;/option&gt;
    	&lt;option value=&quot;html&quot;&gt;HTML&lt;/option&gt;
    	&lt;option value=&quot;java&quot;&gt;Java&lt;/option&gt;
    	&lt;option value=&quot;js&quot;&gt;Javascript&lt;/option&gt;
    	&lt;option value=&quot;perl&quot;&gt;Perl&lt;/option&gt;
    	&lt;option value=&quot;php&quot;&gt;PHP&lt;/option&gt;
        &lt;option value=&quot;ps&quot;&gt;PowerShell&lt;/option&gt;
    	&lt;option value=&quot;python&quot;&gt;Python&lt;/option&gt;
    	&lt;option value=&quot;ruby&quot;&gt;Ruby&lt;/option&gt;
    	&lt;option value=&quot;sql&quot;&gt;SQL&lt;/option&gt;
    	&lt;option value=&quot;vb&quot;&gt;VisualBasic&lt;/option&gt;
    	&lt;option value=&quot;vb&quot;&gt;VB.NET&lt;/option&gt;
    	&lt;option value=&quot;xml&quot;&gt;XML&lt;/option&gt;
    &lt;/select&gt;
    &lt;br&gt;
    Code:&lt;br&gt;&lt;textarea id=&quot;code&quot; rows=&quot;8&quot; cols=&quot;70&quot; style=&quot;width:97%;&quot;&gt;&lt;/textarea&gt;&lt;br&gt;
    &lt;input type=&quot;button&quot; value=&quot;INSERT&quot; onclick=&quot;javascript:settext();&quot;&gt;
    
    &lt;script&gt;
    function settext()
    { 
    	var str='&lt;pre escaped=&quot;true&quot; lang=&quot;';
    	var lang=document.getElementById(&quot;language&quot;).value;
    	var code=document.getElementById(&quot;code&quot;).value;
    	str=str+lang;
    	str=str+'&quot;&gt;';
    	str=str+filter(code)+&quot;&lt;/pre&gt;&quot;;
    	var win = window.dialogArguments ¦¦ opener ¦¦ parent ¦¦ top;
    	win.send_to_editor(str);
    	document.getElementById(&quot;code&quot;).value=&quot;&quot;;
    }
    function filter (str) {
    	str = str.replace(/&amp;/g, '&amp;amp;');
    	str = str.replace(/&lt;/g, '&amp;lt;');
    	str = str.replace(/&gt;/g, '&amp;gt;');
    	str = str.replace(/'/g, '&amp;#39;');
    	str = str.replace(/&quot;/g, '&amp;quot;');
    	str = str.replace(/\¦/g, '&amp;brvbar;');
    	return str;
    }
    &lt;/script&gt;
    &lt;/div&gt;&lt;/div&gt;&lt;/div&gt;
    &lt;script&gt;document.getElementById(&quot;postdivrich&quot;).appendChild(document.getElementById(&quot;codebox&quot;));&lt;/script&gt;
    &lt;?php
    }
    add_action('dbx_post_sidebar','codebox_init');
    ?&gt;</p></div>
    ";}
categories:
  - 网页前端
tags:
  - plugin
  - wordpress
  - wp-syntax

---
升级到WP3.3后，之前的那些插入代码按钮都没有用啦。。上去找插件没找到，自己改了一个syntanx-highlighter的。  
感谢原作者leo108，http://leo108.com/
把下面的代码保存下来，放在一个文件夹里，打包成zip文件，然后就可以在插件处上传安装了。  
或者下载这个文件：<a href="http://fatkun.googlecode.com/files/wp-syntax-editor.zip" title="http://fatkun.googlecode.com/files/wp-syntax-editor.zip" target="_blank">http://fatkun.googlecode.com/files/wp-syntax-editor.zip</a>
<pre escaped="true" lang="js">&lt;?php
/*
Plugin Name: WP-Syntax Code Editor
Plugin URI: http://fatkun.com/2012/01/wp-syntax-code-editor.html
Description: 在编辑框加入一个插入wp-syntax代码的按钮，修改自syntax-highlighter-with-add-button-in-editor（原作者leo108）
Version: 1.0.0
Original Author: leo108
Author URI: http://fatkun.com/
*/
function codebox_init(){
?&gt;
&lt;div id="codebox" class="meta-box-sortables ui-sortable" style="position: relative;"&gt;&lt;div class="postbox"&gt;
&lt;div class="handlediv" title="Click to toggle"&gt;&lt;/div&gt;
&lt;h3 class="hndle"&gt;&lt;span&gt;WP-Syntax&lt;/span&gt;&lt;/h3&gt;
&lt;div class="inside"&gt;
Language:
&lt;select id="language"&gt;
	&lt;option value="other"&gt;Other&lt;/option&gt;
	&lt;option value="bash"&gt;Bash&lt;/option&gt;
	&lt;option value="c"&gt;C&lt;/option&gt;
	&lt;option value="cpp"&gt;C++&lt;/option&gt;
	&lt;option value="csharp"&gt;C#&lt;/option&gt;
	&lt;option value="css"&gt;CSS&lt;/option&gt;
	&lt;option value="delphi"&gt;Delphi&lt;/option&gt;
	&lt;option value="diff"&gt;Diff&lt;/option&gt;
	&lt;option value="erl"&gt;Erlang&lt;/option&gt;
	&lt;option value="groovy"&gt;Groovy&lt;/option&gt;
	&lt;option value="html"&gt;HTML&lt;/option&gt;
	&lt;option value="java"&gt;Java&lt;/option&gt;
	&lt;option value="js"&gt;Javascript&lt;/option&gt;
	&lt;option value="perl"&gt;Perl&lt;/option&gt;
	&lt;option value="php"&gt;PHP&lt;/option&gt;
    &lt;option value="ps"&gt;PowerShell&lt;/option&gt;
	&lt;option value="python"&gt;Python&lt;/option&gt;
	&lt;option value="ruby"&gt;Ruby&lt;/option&gt;
	&lt;option value="sql"&gt;SQL&lt;/option&gt;
	&lt;option value="vb"&gt;VisualBasic&lt;/option&gt;
	&lt;option value="vb"&gt;VB.NET&lt;/option&gt;
	&lt;option value="xml"&gt;XML&lt;/option&gt;
&lt;/select&gt;
&lt;br&gt;
Code:&lt;br&gt;&lt;textarea id="code" rows="8" cols="70" style="width:97%;"&gt;&lt;/textarea&gt;&lt;br&gt;
&lt;input type="button" value="INSERT" onclick="javascript:settext();"&gt;

&lt;script&gt;
function settext()
{ 
	var str='&lt;pre escaped="true" lang="';
	var lang=document.getElementById("language").value;
	var code=document.getElementById("code").value;
	str=str+lang;
	str=str+'"&gt;';
	str=str+filter(code)+"&lt;/pre&gt;";
	var win = window.dialogArguments ¦¦ opener ¦¦ parent ¦¦ top;
	win.send_to_editor(str);
	document.getElementById("code").value="";
}
function filter (str) {
	str = str.replace(/&/g, '&amp;');
	str = str.replace(/&lt;/g, '&lt;');
	str = str.replace(/&gt;/g, '&gt;');
	str = str.replace(/'/g, '&#39;');
	str = str.replace(/"/g, '&quot;');
	str = str.replace(/\¦/g, '&brvbar;');
	return str;
}
&lt;/script&gt;
&lt;/div&gt;&lt;/div&gt;&lt;/div&gt;
&lt;script&gt;document.getElementById("postdivrich").appendChild(document.getElementById("codebox"));&lt;/script&gt;
&lt;?php
}
add_action('dbx_post_sidebar','codebox_init');
?&gt;</pre>