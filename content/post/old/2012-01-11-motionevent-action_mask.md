---
title: 'event.getAction()&MotionEvent.ACTION_MASK的原因'
author: fatkun
type: post
date: 2012-01-10T17:36:45+00:00
url: /2012/01/motionevent-action_mask.html
duoshuo_thread_id:
  - 6300408827619574530
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:4080:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">	<span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">boolean</span> onTouchEvent<span style="color: #009900;">&#40;</span>MotionEvent event<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    		<span style="color: #000066; font-weight: bold;">int</span> action <span style="color: #339933;">=</span> event.<span style="color: #006633;">getAction</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #000000; font-weight: bold;">switch</span> <span style="color: #009900;">&#40;</span>action <span style="color: #339933;">&amp;</span> MotionEvent.<span style="color: #006633;">ACTION_MASK</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    		<span style="color: #000000; font-weight: bold;">case</span> MotionEvent.<span style="color: #006633;">ACTION_DOWN</span><span style="color: #339933;">:</span>
    			showMsg<span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;ACTION_DOWN&quot;</span> <span style="color: #339933;">+</span> action<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    			<span style="color: #000000; font-weight: bold;">break</span><span style="color: #339933;">;</span>
    		<span style="color: #000000; font-weight: bold;">case</span> MotionEvent.<span style="color: #006633;">ACTION_UP</span><span style="color: #339933;">:</span>
    			showMsg<span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;ACTION_UP&quot;</span> <span style="color: #339933;">+</span> action<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    			<span style="color: #000000; font-weight: bold;">break</span><span style="color: #339933;">;</span>
    		<span style="color: #000000; font-weight: bold;">case</span> MotionEvent.<span style="color: #006633;">ACTION_POINTER_UP</span><span style="color: #339933;">:</span>
    			showMsg<span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;ACTION_POINTER_UP&quot;</span> <span style="color: #339933;">+</span> action<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    			<span style="color: #000000; font-weight: bold;">break</span><span style="color: #339933;">;</span>
    		<span style="color: #000000; font-weight: bold;">case</span> MotionEvent.<span style="color: #006633;">ACTION_POINTER_DOWN</span><span style="color: #339933;">:</span>
    			showMsg<span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;ACTION_POINTER_DOWN&quot;</span> <span style="color: #339933;">+</span> action<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    			<span style="color: #000000; font-weight: bold;">break</span><span style="color: #339933;">;</span>
    		<span style="color: #009900;">&#125;</span>
    		<span style="color: #000000; font-weight: bold;">return</span> <span style="color: #000000; font-weight: bold;">super</span>.<span style="color: #006633;">onTouchEvent</span><span style="color: #009900;">&#40;</span>event<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">	public boolean onTouchEvent(MotionEvent event) {
    		int action = event.getAction();
    		switch (action &amp; MotionEvent.ACTION_MASK) {
    		case MotionEvent.ACTION_DOWN:
    			showMsg(&quot;ACTION_DOWN&quot; + action);
    			break;
    		case MotionEvent.ACTION_UP:
    			showMsg(&quot;ACTION_UP&quot; + action);
    			break;
    		case MotionEvent.ACTION_POINTER_UP:
    			showMsg(&quot;ACTION_POINTER_UP&quot; + action);
    			break;
    		case MotionEvent.ACTION_POINTER_DOWN:
    			showMsg(&quot;ACTION_POINTER_DOWN&quot; + action);
    			break;
    		}
    		return super.onTouchEvent(event);
    	}</p></div>
    ";i:2;s:1131:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="other" style="font-family:monospace;">ACTION_MASK     0x000000ff
    ACTION_DOWN     0x00000000         ACTION_UP      0x00000001        ACTION_MOVE      0x00000002
    ACTION_POINTER_DOWN       0x00000005            ACTION_POINTER_UP        0x00000006
    ACTION_POINTER_1_DOWN     0x00000005            ACTION_POINTER_1_UP      0x00000006
    ACTION_POINTER_2_DOWN     0x00000105            ACTION_POINTER_2_UP      0x00000106
    ACTION_POINTER_3_DOWN     0x00000205            ACTION_POINTER_3_UP      0x00000206</pre></td></tr></table><p class="theCode" style="display:none;">ACTION_MASK     0x000000ff
    ACTION_DOWN     0x00000000         ACTION_UP      0x00000001        ACTION_MOVE      0x00000002
    ACTION_POINTER_DOWN       0x00000005            ACTION_POINTER_UP        0x00000006
    ACTION_POINTER_1_DOWN     0x00000005            ACTION_POINTER_1_UP      0x00000006
    ACTION_POINTER_2_DOWN     0x00000105            ACTION_POINTER_2_UP      0x00000106
    ACTION_POINTER_3_DOWN     0x00000205            ACTION_POINTER_3_UP      0x00000206</p></div>
    ";}
categories:
  - Android
tags:
  - ACTION_MASK
  - Android
  - touch

---
看到下面代码中用了AND位运算是为了什么呢？
<pre lang="java" escaped="true">public boolean onTouchEvent(MotionEvent event) {
		int action = event.getAction();
		switch (action & MotionEvent.ACTION_MASK) {
		case MotionEvent.ACTION_DOWN:
			showMsg("ACTION_DOWN" + action);
			break;
		case MotionEvent.ACTION_UP:
			showMsg("ACTION_UP" + action);
			break;
		case MotionEvent.ACTION_POINTER_UP:
			showMsg("ACTION_POINTER_UP" + action);
			break;
		case MotionEvent.ACTION_POINTER_DOWN:
			showMsg("ACTION_POINTER_DOWN" + action);
			break;
		}
		return super.onTouchEvent(event);
	}</pre>
首先来看看这些常量的值
<pre lang="other" escaped="true">ACTION_MASK     0x000000ff
ACTION_DOWN     0x00000000         ACTION_UP      0x00000001        ACTION_MOVE      0x00000002
ACTION_POINTER_DOWN       0x00000005            ACTION_POINTER_UP        0x00000006
ACTION_POINTER_1_DOWN     0x00000005            ACTION_POINTER_1_UP      0x00000006
ACTION_POINTER_2_DOWN     0x00000105            ACTION_POINTER_2_UP      0x00000106
ACTION_POINTER_3_DOWN     0x00000205            ACTION_POINTER_3_UP      0x00000206</pre>
看到这么多16进制有没有怕呢。。。我数学不太好，看着有点怕呢~  
先做做十六进制AND运算  
来看看ACTION\_MASK & ACTION\_POINTER\_2\_DOWN 即 0x000000ff & 0x00000105  
<del>换成二进制 1111 1111(2) & 1 0000 0110(2) = 0110(2) = 0x00000006</del>
update：上面换算错了。。囧，应该是 1111 1111(2) & 1 0000 0101(2) = 0101(2) = 0x00000005  
如果不会换算，试试用计算器啦。。（掩面，我也是用计算器，快速计算的方法是把16进制的每一位扩展为4位的二进制）  
可以看到，and运算的结果总是小于等于0x000000ff，那就是说and之后，无论你多少根手指加进来，都是会ACTION\_POINTER\_DOWN或者ACTION\_POINTER\_UP
补充一下，当第二个手指触摸屏幕时，event.getAction()的值是0x00000105，第三个手指触摸是0x00000205，放开相应的手指数量会返回相应的值。