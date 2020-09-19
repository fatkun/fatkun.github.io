---
title: Android选项卡(TabWidget)例子
author: fatkun
type: post
date: 2010-06-17T02:10:52+00:00
url: /2010/06/android-tabwidget.html
views:
  - 296
duoshuo_thread_id:
  - 6300408737404289793
wp-syntax-cache-content:
  - |
    a:4:{i:1;s:2130:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> OneActivity <span style="color: #000000; font-weight: bold;">extends</span> Activity <span style="color: #009900;">&#123;</span>
        <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> onCreate<span style="color: #009900;">&#40;</span>Bundle savedInstanceState<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">super</span>.<span style="color: #006633;">onCreate</span><span style="color: #009900;">&#40;</span>savedInstanceState<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
            TextView textview <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> TextView<span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">this</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            textview.<span style="color: #006633;">setText</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;This is the Artists tab&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            setContentView<span style="color: #009900;">&#40;</span>textview<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">public class OneActivity extends Activity {
        public void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
    
            TextView textview = new TextView(this);
            textview.setText(&quot;This is the Artists tab&quot;);
            setContentView(textview);
        }
    }</p></div>
    ";i:2;s:4730:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;?xml</span> <span style="color: #000066;">version</span>=<span style="color: #ff0000;">&quot;1.0&quot;</span> <span style="color: #000066;">encoding</span>=<span style="color: #ff0000;">&quot;utf-8&quot;</span><span style="color: #000000; font-weight: bold;">?&gt;</span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;TabHost</span> <span style="color: #000066;">android:id</span>=<span style="color: #ff0000;">&quot;@android:id/tabhost&quot;</span> <span style="color: #000066;">android:layout_width</span>=<span style="color: #ff0000;">&quot;fill_parent&quot;</span></span>
    <span style="color: #009900;">	<span style="color: #000066;">android:layout_height</span>=<span style="color: #ff0000;">&quot;fill_parent&quot;</span> <span style="color: #000066;">xmlns:android</span>=<span style="color: #ff0000;">&quot;http://schemas.android.com/apk/res/android&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
    	<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;LinearLayout</span></span>
    <span style="color: #009900;">		<span style="color: #000066;">android:orientation</span>=<span style="color: #ff0000;">&quot;vertical&quot;</span></span>
    <span style="color: #009900;">		<span style="color: #000066;">android:layout_width</span>=<span style="color: #ff0000;">&quot;fill_parent&quot;</span></span>
    <span style="color: #009900;">		<span style="color: #000066;">android:layout_height</span>=<span style="color: #ff0000;">&quot;fill_parent&quot;</span></span>
    <span style="color: #009900;">		<span style="color: #000000; font-weight: bold;">&gt;</span></span>
    		<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;TabWidget</span> <span style="color: #000066;">android:id</span>=<span style="color: #ff0000;">&quot;@android:id/tabs&quot;</span></span>
    <span style="color: #009900;">			<span style="color: #000066;">android:layout_width</span>=<span style="color: #ff0000;">&quot;fill_parent&quot;</span> <span style="color: #000066;">android:layout_height</span>=<span style="color: #ff0000;">&quot;wrap_content&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span><span style="color: #000000; font-weight: bold;">&lt;/TabWidget<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    		<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;FrameLayout</span></span>
    <span style="color: #009900;">            <span style="color: #000066;">android:id</span>=<span style="color: #ff0000;">&quot;@android:id/tabcontent&quot;</span></span>
    <span style="color: #009900;">            <span style="color: #000066;">android:layout_width</span>=<span style="color: #ff0000;">&quot;fill_parent&quot;</span></span>
    <span style="color: #009900;">            <span style="color: #000066;">android:layout_height</span>=<span style="color: #ff0000;">&quot;fill_parent&quot;</span></span>
    <span style="color: #009900;">            <span style="color: #000066;">android:padding</span>=<span style="color: #ff0000;">&quot;5dp&quot;</span> <span style="color: #000000; font-weight: bold;">/&gt;</span></span>
    	<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/LinearLayout<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/TabHost<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot;?&gt;
    &lt;TabHost android:id=&quot;@android:id/tabhost&quot; android:layout_width=&quot;fill_parent&quot;
    	android:layout_height=&quot;fill_parent&quot; xmlns:android=&quot;http://schemas.android.com/apk/res/android&quot;&gt;
    	&lt;LinearLayout
    		android:orientation=&quot;vertical&quot;
    		android:layout_width=&quot;fill_parent&quot;
    		android:layout_height=&quot;fill_parent&quot;
    		&gt;
    		&lt;TabWidget android:id=&quot;@android:id/tabs&quot;
    			android:layout_width=&quot;fill_parent&quot; android:layout_height=&quot;wrap_content&quot;&gt;&lt;/TabWidget&gt;
    		&lt;FrameLayout
                android:id=&quot;@android:id/tabcontent&quot;
                android:layout_width=&quot;fill_parent&quot;
                android:layout_height=&quot;fill_parent&quot;
                android:padding=&quot;5dp&quot; /&gt;
    	&lt;/LinearLayout&gt;
    &lt;/TabHost&gt;</p></div>
    ";i:3;s:9362:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">package</span> <span style="color: #006699;">com.fatkun</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">android.app.TabActivity</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">android.content.Intent</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">android.content.res.Resources</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">android.os.Bundle</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">android.widget.TabHost</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">android.widget.TabHost.TabSpec</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> TabWidget <span style="color: #000000; font-weight: bold;">extends</span> TabActivity <span style="color: #009900;">&#123;</span>
    &nbsp;
    	<span style="color: #008000; font-style: italic; font-weight: bold;">/** Called when the activity is first created. */</span>
    	@Override
    	<span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> onCreate<span style="color: #009900;">&#40;</span>Bundle savedInstanceState<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    	    <span style="color: #000000; font-weight: bold;">super</span>.<span style="color: #006633;">onCreate</span><span style="color: #009900;">&#40;</span>savedInstanceState<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	    setContentView<span style="color: #009900;">&#40;</span>R.<span style="color: #006633;">layout</span>.<span style="color: #006633;">tab</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//这里使用了上面创建的xml文件（Tab页面的布局）</span>
    	    Resources res <span style="color: #339933;">=</span> getResources<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">// Resource object to get Drawables</span>
    	    TabHost tabHost <span style="color: #339933;">=</span> getTabHost<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>  <span style="color: #666666; font-style: italic;">// The activity TabHost</span>
    	    TabSpec spec<span style="color: #339933;">;</span>
    	    Intent intent<span style="color: #339933;">;</span>  <span style="color: #666666; font-style: italic;">// Reusable Intent for each tab</span>
    &nbsp;
    	  <span style="color: #666666; font-style: italic;">//第一个TAB</span>
    	    intent <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> Intent<span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">this</span>,OneActivity.<span style="color: #000000; font-weight: bold;">class</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//新建一个Intent用作Tab1显示的内容</span>
    	    spec <span style="color: #339933;">=</span> tabHost.<span style="color: #006633;">newTabSpec</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;tab1&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #666666; font-style: italic;">//新建一个 Tab</span>
    	    .<span style="color: #006633;">setIndicator</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Tab1&quot;</span>, res.<span style="color: #006633;">getDrawable</span><span style="color: #009900;">&#40;</span>android.<span style="color: #006633;">R</span>.<span style="color: #006633;">drawable</span>.<span style="color: #006633;">ic_media_play</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #666666; font-style: italic;">//设置名称以及图标</span>
    	    .<span style="color: #006633;">setContent</span><span style="color: #009900;">&#40;</span>intent<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//设置显示的intent，这里的参数也可以是R.id.xxx</span>
    	    tabHost.<span style="color: #006633;">addTab</span><span style="color: #009900;">&#40;</span>spec<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//添加进tabHost</span>
    &nbsp;
    	    <span style="color: #666666; font-style: italic;">//第二个TAB</span>
    	    intent <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> Intent<span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">this</span>,TestActivity.<span style="color: #000000; font-weight: bold;">class</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//第二个Intent用作Tab1显示的内容</span>
    	    spec <span style="color: #339933;">=</span> tabHost.<span style="color: #006633;">newTabSpec</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;tab2&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #666666; font-style: italic;">//新建一个 Tab</span>
    	    .<span style="color: #006633;">setIndicator</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Tab2&quot;</span>, res.<span style="color: #006633;">getDrawable</span><span style="color: #009900;">&#40;</span>android.<span style="color: #006633;">R</span>.<span style="color: #006633;">drawable</span>.<span style="color: #006633;">ic_menu_camera</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #666666; font-style: italic;">//设置名称以及图标</span>
    	    .<span style="color: #006633;">setContent</span><span style="color: #009900;">&#40;</span>intent<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//设置显示的intent，这里的参数也可以是R.id.xxx</span>
    	    tabHost.<span style="color: #006633;">addTab</span><span style="color: #009900;">&#40;</span>spec<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">//添加进tabHost</span>
    &nbsp;
    	    tabHost.<span style="color: #006633;">setCurrentTab</span><span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">1</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">package com.fatkun;
    
    import android.app.TabActivity;
    import android.content.Intent;
    import android.content.res.Resources;
    import android.os.Bundle;
    import android.widget.TabHost;
    import android.widget.TabHost.TabSpec;
    
    public class TabWidget extends TabActivity {
    
    	/** Called when the activity is first created. */
    	@Override
    	public void onCreate(Bundle savedInstanceState) {
    	    super.onCreate(savedInstanceState);
    	    setContentView(R.layout.tab);//这里使用了上面创建的xml文件（Tab页面的布局）
    	    Resources res = getResources(); // Resource object to get Drawables
    	    TabHost tabHost = getTabHost();  // The activity TabHost
    	    TabSpec spec;
    	    Intent intent;  // Reusable Intent for each tab
    
    	  //第一个TAB
    	    intent = new Intent(this,OneActivity.class);//新建一个Intent用作Tab1显示的内容
    	    spec = tabHost.newTabSpec(&quot;tab1&quot;)//新建一个 Tab
    	    .setIndicator(&quot;Tab1&quot;, res.getDrawable(android.R.drawable.ic_media_play))//设置名称以及图标
    	    .setContent(intent);//设置显示的intent，这里的参数也可以是R.id.xxx
    	    tabHost.addTab(spec);//添加进tabHost
    
    	    //第二个TAB
    	    intent = new Intent(this,TestActivity.class);//第二个Intent用作Tab1显示的内容
    	    spec = tabHost.newTabSpec(&quot;tab2&quot;)//新建一个 Tab
    	    .setIndicator(&quot;Tab2&quot;, res.getDrawable(android.R.drawable.ic_menu_camera))//设置名称以及图标
    	    .setContent(intent);//设置显示的intent，这里的参数也可以是R.id.xxx
    	    tabHost.addTab(spec);//添加进tabHost
    
    	    tabHost.setCurrentTab(1);
    	}
    
    }</p></div>
    ";i:4;s:1846:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;">    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;activity</span> <span style="color: #000066;">android:name</span>=<span style="color: #ff0000;">&quot;TabWidget&quot;</span> <span style="color: #000066;">android:theme</span>=<span style="color: #ff0000;">&quot;@android:style/Theme.NoTitleBar&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span><span style="color: #000000; font-weight: bold;">&lt;/activity<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;activity</span> <span style="color: #000066;">android:name</span>=<span style="color: #ff0000;">&quot;OneActivity&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span><span style="color: #000000; font-weight: bold;">&lt;/activity<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;activity</span> <span style="color: #000066;">android:name</span>=<span style="color: #ff0000;">&quot;TestActivity&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span><span style="color: #000000; font-weight: bold;">&lt;/activity<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">    &lt;activity android:name=&quot;TabWidget&quot; android:theme=&quot;@android:style/Theme.NoTitleBar&quot;&gt;&lt;/activity&gt;
        &lt;activity android:name=&quot;OneActivity&quot;&gt;&lt;/activity&gt;
        &lt;activity android:name=&quot;TestActivity&quot;&gt;&lt;/activity&gt;</p></div>
    ";}
categories:
  - Android
tags:
  - Android

---
首届Google暑期大学生博客分享大赛——2010 Andriod篇
Android选项卡的一个例子，这个例子是照着SDK 文档做的（resources/tutorials/views/hello-tabwidget.html），为了省事少做了一些图标类的东西。
[![tab][1]][2]{.flickr-image.alignnone}
## <!--more-->步骤

### 1.建立两个Activity，作为tab内容 （我这里是OneActivity、TestActivity)

<pre escaped="true" lang="java">public class OneActivity extends Activity {
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        TextView textview = new TextView(this);
        textview.setText("This is the Artists tab");
        setContentView(textview);
    }
}</pre>
### 2.在layout文件夹中建立tab.xml用于怎样显示tab页面

<span style="color: #ff0000;">注意：TabHost ，TabWidget ，FrameLayout的ID必须分别为@android:id/tabhost，@android:id/tabs，@android:id/tabcontent</span>  
另外还要注意一下android:layout\_width宽度和android:layout\_height高度的取值，还要LinearLayout的android:orientation=&#8221;vertical&#8221;（LinearLayout默认是横向的）当你看到布局和我不一样时你就要考虑一下这里是不是错了。（= =！因为我错过）
<pre escaped="true" lang="xml">&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;TabHost android:id="@android:id/tabhost" android:layout_width="fill_parent"
	android:layout_height="fill_parent" xmlns:android="http://schemas.android.com/apk/res/android"&gt;
	&lt;LinearLayout
		android:orientation="vertical"
		android:layout_width="fill_parent"
		android:layout_height="fill_parent"
		&gt;
		&lt;TabWidget android:id="@android:id/tabs"
			android:layout_width="fill_parent" android:layout_height="wrap_content"&gt;&lt;/TabWidget&gt;
		&lt;FrameLayout
            android:id="@android:id/tabcontent"
            android:layout_width="fill_parent"
            android:layout_height="fill_parent"
            android:padding="5dp" /&gt;
	&lt;/LinearLayout&gt;
&lt;/TabHost&gt;</pre>
## 3.新建一个类TabWidget.java，继承TabActivity类

<pre escaped="true" lang="java">package com.fatkun;

import android.app.TabActivity;
import android.content.Intent;
import android.content.res.Resources;
import android.os.Bundle;
import android.widget.TabHost;
import android.widget.TabHost.TabSpec;

public class TabWidget extends TabActivity {

	/** Called when the activity is first created. */
	@Override
	public void onCreate(Bundle savedInstanceState) {
	    super.onCreate(savedInstanceState);
	    setContentView(R.layout.tab);//这里使用了上面创建的xml文件（Tab页面的布局）
	    Resources res = getResources(); // Resource object to get Drawables
	    TabHost tabHost = getTabHost();  // The activity TabHost
	    TabSpec spec;
	    Intent intent;  // Reusable Intent for each tab

	  //第一个TAB
	    intent = new Intent(this,OneActivity.class);//新建一个Intent用作Tab1显示的内容
	    spec = tabHost.newTabSpec("tab1")//新建一个 Tab
	    .setIndicator("Tab1", res.getDrawable(android.R.drawable.ic_media_play))//设置名称以及图标
	    .setContent(intent);//设置显示的intent，这里的参数也可以是R.id.xxx
	    tabHost.addTab(spec);//添加进tabHost

	    //第二个TAB
	    intent = new Intent(this,TestActivity.class);//第二个Intent用作Tab1显示的内容
	    spec = tabHost.newTabSpec("tab2")//新建一个 Tab
	    .setIndicator("Tab2", res.getDrawable(android.R.drawable.ic_menu_camera))//设置名称以及图标
	    .setContent(intent);//设置显示的intent，这里的参数也可以是R.id.xxx
	    tabHost.addTab(spec);//添加进tabHost

	    tabHost.setCurrentTab(1);
	}

}</pre>
## 4.最后一步，在AndroidManifest.xml加入你的Activity

android:theme=&#8221;@android:style/Theme.NoTitleBar&#8221;是可以使得TabWidget窗口没有标题，多点空间显示
<pre escaped="true" lang="xml">&lt;activity android:name="TabWidget" android:theme="@android:style/Theme.NoTitleBar"&gt;&lt;/activity&gt;
    &lt;activity android:name="OneActivity"&gt;&lt;/activity&gt;
    &lt;activity android:name="TestActivity"&gt;&lt;/activity&gt;</pre>

 [1]: http://farm5.static.flickr.com/4008/4706942050_b50ddd0478_b.jpg
 [2]: http://www.flickr.com/photos/fatkun/4706942050/ "tab"