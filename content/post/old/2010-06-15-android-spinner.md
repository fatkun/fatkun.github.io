---
title: Android下拉列表(Spinner)例子
author: fatkun
type: post
date: 2010-06-15T11:32:06+00:00
url: /2010/06/android-spinner.html
views:
  - 43
duoshuo_thread_id:
  - 6300408732404679426
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:1300:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;Spinner</span> <span style="color: #000066;">android:layout_height</span>=<span style="color: #ff0000;">&quot;wrap_content&quot;</span> <span style="color: #000066;">android:layout_width</span>=<span style="color: #ff0000;">&quot;wrap_content&quot;</span> <span style="color: #000066;">android:layout_y</span>=<span style="color: #ff0000;">&quot;132dip&quot;</span> <span style="color: #000066;">android:layout_x</span>=<span style="color: #ff0000;">&quot;97dip&quot;</span> <span style="color: #000066;">android:id</span>=<span style="color: #ff0000;">&quot;@+id/Spinner01&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span><span style="color: #000000; font-weight: bold;">&lt;/Spinner<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">&lt;Spinner android:layout_height=&quot;wrap_content&quot; android:layout_width=&quot;wrap_content&quot; android:layout_y=&quot;132dip&quot; android:layout_x=&quot;97dip&quot; android:id=&quot;@+id/Spinner01&quot;&gt;&lt;/Spinner&gt;</p></div>
    ";i:2;s:6798:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #666666; font-style: italic;">/*
     	ArrayAdapter.createFromResource参数解析：
     	第一个是Context，
     	第二个(R.array.colors)是数据来源，在values.xml，内容为
    		&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot;?&gt;
    		&lt;resources&gt;
    			&lt;string-array name=&quot;colors&quot;&gt;
    				&lt;item&gt;red&lt;/item&gt;
    				&lt;item&gt;blue&lt;/item&gt;
    				&lt;item&gt;green&lt;/item&gt;
    				&lt;item&gt;yellow&lt;/item&gt;
    				&lt;item&gt;black&lt;/item&gt;
    			&lt;/string-array&gt;
    		&lt;/resources&gt;
    		第三个（android.R.layout.simple_spinner_item）为显示的样式
     */</span>
    Spinner spinner <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span>Spinner<span style="color: #009900;">&#41;</span> findViewById<span style="color: #009900;">&#40;</span>R.<span style="color: #006633;">id</span>.<span style="color: #006633;">Spinner01</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">//建立方法有两种</span>
    <span style="color: #666666; font-style: italic;">//方法一,从xml读取</span>
    <span style="color: #666666; font-style: italic;">//ArrayAdapter&lt;CharSequence&gt; adapter = ArrayAdapter.createFromResource(this, R.array.colors, android.R.layout.simple_spinner_item);</span>
    &nbsp;
    <span style="color: #666666; font-style: italic;">//方法二,使用数组</span>
    CharSequence<span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> seq <span style="color: #339933;">=</span> <span style="color: #009900;">&#123;</span><span style="color: #0000ff;">&quot;test11&quot;</span>,<span style="color: #0000ff;">&quot;test12&quot;</span>,<span style="color: #0000ff;">&quot;test13&quot;</span>,<span style="color: #0000ff;">&quot;test14&quot;</span>,<span style="color: #0000ff;">&quot;test15&quot;</span><span style="color: #009900;">&#125;</span><span style="color: #339933;">;</span>
    ArrayAdapter<span style="color: #339933;">&lt;</span>CharSequence<span style="color: #339933;">&gt;</span> adapter <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> ArrayAdapter<span style="color: #339933;">&lt;</span>CharSequence<span style="color: #339933;">&gt;</span><span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">this</span>, android.<span style="color: #006633;">R</span>.<span style="color: #006633;">layout</span>.<span style="color: #006633;">simple_spinner_item</span>, seq<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    adapter.<span style="color: #006633;">setDropDownViewResource</span><span style="color: #009900;">&#40;</span>android.<span style="color: #006633;">R</span>.<span style="color: #006633;">layout</span>.<span style="color: #006633;">simple_spinner_dropdown_item</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    spinner.<span style="color: #006633;">setAdapter</span><span style="color: #009900;">&#40;</span>adapter<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    spinner.<span style="color: #006633;">setOnItemSelectedListener</span><span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">new</span> OnItemSelectedListener<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    		<span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> onItemSelected<span style="color: #009900;">&#40;</span>AdapterView<span style="color: #339933;">&lt;?&gt;</span> parent, <span style="color: #003399;">View</span> view, <span style="color: #000066; font-weight: bold;">int</span> position, <span style="color: #000066; font-weight: bold;">long</span> id<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    			<span style="color: #666666; font-style: italic;">//showToast(&quot;Spinner1: position=&quot; + position + &quot; id=&quot; + id);</span>
    			<span style="color: #666666; font-style: italic;">//选择后</span>
    		<span style="color: #009900;">&#125;</span>
    		<span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> onNothingSelected<span style="color: #009900;">&#40;</span>AdapterView<span style="color: #339933;">&lt;?&gt;</span> arg0<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    			<span style="color: #666666; font-style: italic;">//showToast(&quot;没有选择&quot;);</span>
    			<span style="color: #666666; font-style: italic;">//没有选择</span>
    		<span style="color: #009900;">&#125;</span>
    	<span style="color: #009900;">&#125;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span></pre></td></tr></table><p class="theCode" style="display:none;">/*
     	ArrayAdapter.createFromResource参数解析：
     	第一个是Context，
     	第二个(R.array.colors)是数据来源，在values.xml，内容为
    		&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot;?&gt;
    		&lt;resources&gt;
    			&lt;string-array name=&quot;colors&quot;&gt;
    				&lt;item&gt;red&lt;/item&gt;
    				&lt;item&gt;blue&lt;/item&gt;
    				&lt;item&gt;green&lt;/item&gt;
    				&lt;item&gt;yellow&lt;/item&gt;
    				&lt;item&gt;black&lt;/item&gt;
    			&lt;/string-array&gt;
    		&lt;/resources&gt;
    		第三个（android.R.layout.simple_spinner_item）为显示的样式
     */
    Spinner spinner = (Spinner) findViewById(R.id.Spinner01);
    //建立方法有两种
    //方法一,从xml读取
    //ArrayAdapter&lt;CharSequence&gt; adapter = ArrayAdapter.createFromResource(this, R.array.colors, android.R.layout.simple_spinner_item);
    
    //方法二,使用数组
    CharSequence[] seq = {&quot;test11&quot;,&quot;test12&quot;,&quot;test13&quot;,&quot;test14&quot;,&quot;test15&quot;};
    ArrayAdapter&lt;CharSequence&gt; adapter = new ArrayAdapter&lt;CharSequence&gt;(this, android.R.layout.simple_spinner_item, seq);
    adapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item);
    spinner.setAdapter(adapter);
    spinner.setOnItemSelectedListener(new OnItemSelectedListener() {
    		public void onItemSelected(AdapterView&lt;?&gt; parent, View view, int position, long id) {
    			//showToast(&quot;Spinner1: position=&quot; + position + &quot; id=&quot; + id);
    			//选择后
    		}
    		public void onNothingSelected(AdapterView&lt;?&gt; arg0) {
    			//showToast(&quot;没有选择&quot;);
    			//没有选择
    		}
    	});</p></div>
    ";}
categories:
  - Android
  - J2EE
tags:
  - Android
  - 界面

---
下拉列表(Spinner)的例子，首先要在layout中拖放一个Spinner，例子中的ID为Spinner01
<pre escaped="true" lang="xml">&lt;Spinner android:layout_height="wrap_content" android:layout_width="wrap_content" android:layout_y="132dip" android:layout_x="97dip" android:id="@+id/Spinner01"&gt;&lt;/Spinner&gt;</pre>
代码：
<pre escaped="true" lang="java">/*
 	ArrayAdapter.createFromResource参数解析：
 	第一个是Context，
 	第二个(R.array.colors)是数据来源，在values.xml，内容为
		&lt;?xml version="1.0" encoding="utf-8"?&gt;
		&lt;resources&gt;
			&lt;string-array name="colors"&gt;
				&lt;item&gt;red&lt;/item&gt;
				&lt;item&gt;blue&lt;/item&gt;
				&lt;item&gt;green&lt;/item&gt;
				&lt;item&gt;yellow&lt;/item&gt;
				&lt;item&gt;black&lt;/item&gt;
			&lt;/string-array&gt;
		&lt;/resources&gt;
		第三个（android.R.layout.simple_spinner_item）为显示的样式
 */
Spinner spinner = (Spinner) findViewById(R.id.Spinner01);
//建立方法有两种
//方法一,从xml读取
//ArrayAdapter&lt;CharSequence&gt; adapter = ArrayAdapter.createFromResource(this, R.array.colors, android.R.layout.simple_spinner_item);

//方法二,使用数组
CharSequence[] seq = {"test11","test12","test13","test14","test15"};
ArrayAdapter&lt;CharSequence&gt; adapter = new ArrayAdapter&lt;CharSequence&gt;(this, android.R.layout.simple_spinner_item, seq);
adapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item);
spinner.setAdapter(adapter);
spinner.setOnItemSelectedListener(new OnItemSelectedListener() {
		public void onItemSelected(AdapterView&lt;?&gt; parent, View view, int position, long id) {
			//showToast("Spinner1: position=" + position + " id=" + id);
			//选择后
		}
		public void onNothingSelected(AdapterView&lt;?&gt; arg0) {
			//showToast("没有选择");
			//没有选择
		}
	});</pre>