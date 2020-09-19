---
title: Activity startActivityForResult
author: fatkun
type: post
date: 2012-01-01T14:24:32+00:00
url: /2012/01/activity-startactivityforresult.html
duoshuo_thread_id:
  - 6300408827426636545
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:684:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;activity</span> <span style="color: #000066;">android:name</span>=<span style="color: #ff0000;">&quot;.OtherActivity&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span><span style="color: #000000; font-weight: bold;">&lt;/activity<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">&lt;activity android:name=&quot;.OtherActivity&quot;&gt;&lt;/activity&gt;</p></div>
    ";i:2;s:8887:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">package</span> <span style="color: #006699;">com.fatkun</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">android.app.Activity</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">android.content.Intent</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">android.os.Bundle</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">android.view.View</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">android.view.View.OnClickListener</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">android.widget.Button</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">android.widget.Toast</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> OneActivity <span style="color: #000000; font-weight: bold;">extends</span> Activity <span style="color: #009900;">&#123;</span>
    	<span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000000; font-weight: bold;">final</span> <span style="color: #000066; font-weight: bold;">int</span> myRequestCode <span style="color: #339933;">=</span> <span style="color: #cc66cc;">1</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">//请求码</span>
    &nbsp;
        <span style="color: #008000; font-style: italic; font-weight: bold;">/** Called when the activity is first created. */</span>
        @Override
        <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> onCreate<span style="color: #009900;">&#40;</span>Bundle savedInstanceState<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">super</span>.<span style="color: #006633;">onCreate</span><span style="color: #009900;">&#40;</span>savedInstanceState<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            setContentView<span style="color: #009900;">&#40;</span>R.<span style="color: #006633;">layout</span>.<span style="color: #006633;">main</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #003399;">Button</span> btn <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">Button</span><span style="color: #009900;">&#41;</span>findViewById<span style="color: #009900;">&#40;</span>R.<span style="color: #006633;">id</span>.<span style="color: #006633;">button1</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            btn.<span style="color: #006633;">setOnClickListener</span><span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">new</span> OnClickListener<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    &nbsp;
    			<span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> onClick<span style="color: #009900;">&#40;</span><span style="color: #003399;">View</span> v<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    				Intent intent <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> Intent<span style="color: #009900;">&#40;</span>OneActivity.<span style="color: #000000; font-weight: bold;">this</span>, OtherActivity.<span style="color: #000000; font-weight: bold;">class</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    				<span style="color: #666666; font-style: italic;">//第二个参数是请求码，会在onActivityResult返回</span>
    				startActivityForResult<span style="color: #009900;">&#40;</span>intent, myRequestCode<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    			<span style="color: #009900;">&#125;</span>
    		<span style="color: #009900;">&#125;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
    	@Override
    	<span style="color: #000000; font-weight: bold;">protected</span> <span style="color: #000066; font-weight: bold;">void</span> onActivityResult<span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> requestCode, <span style="color: #000066; font-weight: bold;">int</span> resultCode, Intent data<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    		<span style="color: #000000; font-weight: bold;">super</span>.<span style="color: #006633;">onActivityResult</span><span style="color: #009900;">&#40;</span>requestCode, resultCode, data<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #000000; font-weight: bold;">switch</span> <span style="color: #009900;">&#40;</span>requestCode<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    		<span style="color: #000000; font-weight: bold;">case</span> myRequestCode<span style="color: #339933;">:</span>
    			<span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>resultCode <span style="color: #339933;">==</span> Activity.<span style="color: #006633;">RESULT_OK</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    				<span style="color: #666666; font-style: italic;">//如果resultCode是RESULT_OK的话，就把内容显示出来。</span>
    				Toast.<span style="color: #006633;">makeText</span><span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">this</span>, data.<span style="color: #006633;">getExtras</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getString</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;info&quot;</span><span style="color: #009900;">&#41;</span>, Toast.<span style="color: #006633;">LENGTH_SHORT</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">show</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    			<span style="color: #009900;">&#125;</span>
    			<span style="color: #000000; font-weight: bold;">break</span><span style="color: #339933;">;</span>
    		<span style="color: #009900;">&#125;</span>
    	<span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">package com.fatkun;
    
    import android.app.Activity;
    import android.content.Intent;
    import android.os.Bundle;
    import android.view.View;
    import android.view.View.OnClickListener;
    import android.widget.Button;
    import android.widget.Toast;
    
    public class OneActivity extends Activity {
    	private final int myRequestCode = 1; //请求码
    	
        /** Called when the activity is first created. */
        @Override
        public void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.main);
            Button btn = (Button)findViewById(R.id.button1);
            btn.setOnClickListener(new OnClickListener() {
    			
    			public void onClick(View v) {
    				Intent intent = new Intent(OneActivity.this, OtherActivity.class);
    				//第二个参数是请求码，会在onActivityResult返回
    				startActivityForResult(intent, myRequestCode);
    			}
    		});
        }
    
    	@Override
    	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    		super.onActivityResult(requestCode, resultCode, data);
    		switch (requestCode) {
    		case myRequestCode:
    			if (resultCode == Activity.RESULT_OK) {
    				//如果resultCode是RESULT_OK的话，就把内容显示出来。
    				Toast.makeText(this, data.getExtras().getString(&quot;info&quot;), Toast.LENGTH_SHORT).show();
    			}
    			break;
    		}
    	}
    }</p></div>
    ";i:3;s:6566:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">package</span> <span style="color: #006699;">com.fatkun</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">android.app.Activity</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">android.content.Intent</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">android.os.Bundle</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">android.view.View</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">android.view.View.OnClickListener</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">android.widget.Button</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> OtherActivity <span style="color: #000000; font-weight: bold;">extends</span> Activity <span style="color: #009900;">&#123;</span>
    &nbsp;
    	@Override
    	<span style="color: #000000; font-weight: bold;">protected</span> <span style="color: #000066; font-weight: bold;">void</span> onCreate<span style="color: #009900;">&#40;</span>Bundle savedInstanceState<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    		<span style="color: #666666; font-style: italic;">// TODO Auto-generated method stub</span>
    		<span style="color: #000000; font-weight: bold;">super</span>.<span style="color: #006633;">onCreate</span><span style="color: #009900;">&#40;</span>savedInstanceState<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		setContentView<span style="color: #009900;">&#40;</span>R.<span style="color: #006633;">layout</span>.<span style="color: #006633;">other</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #003399;">Button</span> btn <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">Button</span><span style="color: #009900;">&#41;</span> findViewById<span style="color: #009900;">&#40;</span>R.<span style="color: #006633;">id</span>.<span style="color: #006633;">button1</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		btn.<span style="color: #006633;">setOnClickListener</span><span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">new</span> OnClickListener<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    &nbsp;
    			<span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> onClick<span style="color: #009900;">&#40;</span><span style="color: #003399;">View</span> v<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    				Intent intent <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> Intent<span style="color: #009900;">&#40;</span>OtherActivity.<span style="color: #000000; font-weight: bold;">this</span>, OneActivity.<span style="color: #000000; font-weight: bold;">class</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    				intent.<span style="color: #006633;">putExtra</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;info&quot;</span>, <span style="color: #0000ff;">&quot;我是从OtherActivity返回的数据&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    				OnClickListener a <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">this</span><span style="color: #339933;">;</span>
    				<span style="color: #666666; font-style: italic;">// 这里的OtherActivity.this是为了得到OtherActivity类的对象，因为现在在button的内部类里面，this指向的是OnClickListener</span>
    				OtherActivity.<span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">setResult</span><span style="color: #009900;">&#40;</span>Activity.<span style="color: #006633;">RESULT_OK</span>, intent<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    				OtherActivity.<span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">finish</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">// 结束自己</span>
    			<span style="color: #009900;">&#125;</span>
    		<span style="color: #009900;">&#125;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">package com.fatkun;
    
    import android.app.Activity;
    import android.content.Intent;
    import android.os.Bundle;
    import android.view.View;
    import android.view.View.OnClickListener;
    import android.widget.Button;
    
    public class OtherActivity extends Activity {
    
    	@Override
    	protected void onCreate(Bundle savedInstanceState) {
    		// TODO Auto-generated method stub
    		super.onCreate(savedInstanceState);
    		setContentView(R.layout.other);
    		Button btn = (Button) findViewById(R.id.button1);
    		btn.setOnClickListener(new OnClickListener() {
    
    			public void onClick(View v) {
    				Intent intent = new Intent(OtherActivity.this, OneActivity.class);
    				intent.putExtra(&quot;info&quot;, &quot;我是从OtherActivity返回的数据&quot;);
    				OnClickListener a = this;
    				// 这里的OtherActivity.this是为了得到OtherActivity类的对象，因为现在在button的内部类里面，this指向的是OnClickListener
    				OtherActivity.this.setResult(Activity.RESULT_OK, intent);
    				OtherActivity.this.finish(); // 结束自己
    			}
    		});
    	}
    
    }</p></div>
    ";}
categories:
  - Android
tags:
  - Activity
  - Android
  - startActivityForResult

---
public void startActivityForResult (Intent intent, int requestCode)  
从一个Activity启动另一个activity，得到结果返回给前一个activity。
## 简单说

OneActivity实现onActivityResult (int requestCode, int resultCode, Intent data)方法，然后使用startActivityForResult启动另一个Activity  
另一个Activity取得结果后通过setResult (&#8230;)把结果传回。
## 代码如下

界面代码不提供了，两个都是一个简单的button  
注意要在AndroidManifest.xml定义你新增的Activity
<pre escaped="true" lang="xml">&lt;activity android:name=".OtherActivity"&gt;&lt;/activity&gt;</pre>
第一个Activity
<pre escaped="true" lang="java">package com.fatkun;

import android.app.Activity;
import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.view.View.OnClickListener;
import android.widget.Button;
import android.widget.Toast;

public class OneActivity extends Activity {
	private final int myRequestCode = 1; //请求码
	
    /** Called when the activity is first created. */
    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main);
        Button btn = (Button)findViewById(R.id.button1);
        btn.setOnClickListener(new OnClickListener() {
			
			public void onClick(View v) {
				Intent intent = new Intent(OneActivity.this, OtherActivity.class);
				//第二个参数是请求码，会在onActivityResult返回
				startActivityForResult(intent, myRequestCode);
			}
		});
    }

	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		switch (requestCode) {
		case myRequestCode:
			if (resultCode == Activity.RESULT_OK) {
				//如果resultCode是RESULT_OK的话，就把内容显示出来。
				Toast.makeText(this, data.getExtras().getString("info"), Toast.LENGTH_SHORT).show();
			}
			break;
		}
	}
}</pre>
第二个Activity
<pre escaped="true" lang="java">package com.fatkun;

import android.app.Activity;
import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.view.View.OnClickListener;
import android.widget.Button;

public class OtherActivity extends Activity {

	@Override
	protected void onCreate(Bundle savedInstanceState) {
		// TODO Auto-generated method stub
		super.onCreate(savedInstanceState);
		setContentView(R.layout.other);
		Button btn = (Button) findViewById(R.id.button1);
		btn.setOnClickListener(new OnClickListener() {

			public void onClick(View v) {
				Intent intent = new Intent(OtherActivity.this, OneActivity.class);
				intent.putExtra("info", "我是从OtherActivity返回的数据");
				OnClickListener a = this;
				// 这里的OtherActivity.this是为了得到OtherActivity类的对象，因为现在在button的内部类里面，this指向的是OnClickListener
				OtherActivity.this.setResult(Activity.RESULT_OK, intent);
				OtherActivity.this.finish(); // 结束自己
			}
		});
	}

}
</pre>