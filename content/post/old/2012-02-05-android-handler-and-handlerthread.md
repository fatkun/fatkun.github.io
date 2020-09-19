---
title: Android Handler和HandlerThread使用方法
author: fatkun
type: post
date: 2012-02-05T14:10:55+00:00
url: /2012/02/android-handler-and-handlerthread.html
duoshuo_thread_id:
  - 6300408827724432130
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:7215:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">        Handler handler <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> Handler<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    &nbsp;
    			@Override
    			<span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> handleMessage<span style="color: #009900;">&#40;</span>Message msg<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    				<span style="color: #666666; font-style: italic;">// 处理发送过来的消息</span>
    				Bundle b <span style="color: #339933;">=</span> msg.<span style="color: #006633;">getData</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    				<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;msg:&quot;</span> <span style="color: #339933;">+</span> msg.<span style="color: #006633;">arg1</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    				<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;msg:&quot;</span> <span style="color: #339933;">+</span> b.<span style="color: #006633;">getString</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;name&quot;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot; - age:&quot;</span> <span style="color: #339933;">+</span> b.<span style="color: #006633;">getInt</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;age&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    				<span style="color: #000000; font-weight: bold;">super</span>.<span style="color: #006633;">handleMessage</span><span style="color: #009900;">&#40;</span>msg<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    			<span style="color: #009900;">&#125;</span>
    &nbsp;
            <span style="color: #009900;">&#125;</span><span style="color: #339933;">;</span>
    &nbsp;
            Message msg <span style="color: #339933;">=</span> handler.<span style="color: #006633;">obtainMessage</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            msg.<span style="color: #006633;">arg1</span> <span style="color: #339933;">=</span> <span style="color: #cc66cc;">121</span><span style="color: #339933;">;</span>
            Bundle b <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> Bundle<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            b.<span style="color: #006633;">putInt</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;age&quot;</span>, <span style="color: #cc66cc;">24</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            b.<span style="color: #006633;">putString</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;name&quot;</span>, <span style="color: #0000ff;">&quot;Fatkun&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            msg.<span style="color: #006633;">setData</span><span style="color: #009900;">&#40;</span>b<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            msg.<span style="color: #006633;">sendToTarget</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
            handler.<span style="color: #006633;">post</span><span style="color: #009900;">&#40;</span>r<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        <span style="color: #003399;">Runnable</span> r <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">Runnable</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    &nbsp;
    		<span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> run<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    			<span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#123;</span>
                                    <span style="color: #666666; font-style: italic;">// 在这里只是睡一下</span>
    				<span style="color: #003399;">Thread</span>.<span style="color: #006633;">sleep</span><span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">10000</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    			<span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">InterruptedException</span> e<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    				e.<span style="color: #006633;">printStackTrace</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    			<span style="color: #009900;">&#125;</span>
    &nbsp;
    		<span style="color: #009900;">&#125;</span>
    	<span style="color: #009900;">&#125;</span><span style="color: #339933;">;</span></pre></td></tr></table><p class="theCode" style="display:none;">        Handler handler = new Handler() {
    
    			@Override
    			public void handleMessage(Message msg) {
    				// 处理发送过来的消息
    				Bundle b = msg.getData();
    				System.out.println(&quot;msg:&quot; + msg.arg1);
    				System.out.println(&quot;msg:&quot; + b.getString(&quot;name&quot;) + &quot; - age:&quot; + b.getInt(&quot;age&quot;));
    				super.handleMessage(msg);
    			}
    
            };
    
            Message msg = handler.obtainMessage();
            msg.arg1 = 121;
            Bundle b = new Bundle();
            b.putInt(&quot;age&quot;, 24);
            b.putString(&quot;name&quot;, &quot;Fatkun&quot;);
            msg.setData(b);
            msg.sendToTarget();
    
            handler.post(r);
    
        }
    
        Runnable r = new Runnable() {
    
    		public void run() {
    			try {
                                    // 在这里只是睡一下
    				Thread.sleep(10000);
    			} catch (InterruptedException e) {
    				e.printStackTrace();
    			}
    
    		}
    	};</p></div>
    ";i:2;s:1938:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #666666; font-style: italic;">//把上面创建Handler的代码</span>
    Handler handler <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> Handler<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    ...
    <span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #666666; font-style: italic;">//改为：</span>
    HandlerThread thread <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> HandlerThread<span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;athread&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    thread.<span style="color: #006633;">start</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">//要把线程启动</span>
    &nbsp;
    Handler handler <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> Handler<span style="color: #009900;">&#40;</span>thread.<span style="color: #006633;">getLooper</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    ...
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">//把上面创建Handler的代码
    Handler handler = new Handler() {
    ...
    }
    
    //改为：
    HandlerThread thread = new HandlerThread(&quot;athread&quot;);
    thread.start(); //要把线程启动
            
    Handler handler = new Handler(thread.getLooper()) {
    ...
    }</p></div>
    ";}
categories:
  - Android
tags:
  - Handler
  - HandlerThread

---
Handler的官方注释如下：
> A Handler allows you to send and process `<a href="file:///F:/android%E5%AD%A6%E4%B9%A0/docs-3.0_r01-linux/docs/reference/android/os/Message.html">Message</a>` and Runnable objects associated with a thread&#8217;s `<a href="file:///F:/android%E5%AD%A6%E4%B9%A0/docs-3.0_r01-linux/docs/reference/android/os/MessageQueue.html">MessageQueue</a>`. Each Handler instance is associated with a single thread and that thread&#8217;s message queue.
Handler会关联一个单独的线程和消息队列。Handler默认关联主线程，虽然要提供Runnable参数 ，但默认是直接调用Runnable中的run()方法。也就是默认下会在主线程执行，如果在这里面的操作会有阻塞，界面也会卡住。如果要在其他线程执行，可以使用HandlerThread。
## Handler使用方法：

<pre lang="java">Handler handler = new Handler() {

			@Override
			public void handleMessage(Message msg) {
				// 处理发送过来的消息
				Bundle b = msg.getData();
				System.out.println("msg:" + msg.arg1);
				System.out.println("msg:" + b.getString("name") + " - age:" + b.getInt("age"));
				super.handleMessage(msg);
			}

        };

        Message msg = handler.obtainMessage();
        msg.arg1 = 121;
        Bundle b = new Bundle();
        b.putInt("age", 24);
        b.putString("name", "Fatkun");
        msg.setData(b);
        msg.sendToTarget();

        handler.post(r);

    }

    Runnable r = new Runnable() {

		public void run() {
			try {
                                // 在这里只是睡一下
				Thread.sleep(10000);
			} catch (InterruptedException e) {
				e.printStackTrace();
			}

		}
	};</pre>
## HandlerThread使用方法：

<pre escaped="true" lang="java">//把上面创建Handler的代码
Handler handler = new Handler() {
...
}

//改为：
HandlerThread thread = new HandlerThread("athread");
thread.start(); //要把线程启动
        
Handler handler = new Handler(thread.getLooper()) {
...
}</pre>
## 参考：

<a href="http://www.cnblogs.com/xirihanlin/archive/2011/04/11/2012746.html" title="Android中的Handler, Looper, MessageQueue和Thread" target="_blank">Android中的Handler, Looper, MessageQueue和Thread的关系</a>