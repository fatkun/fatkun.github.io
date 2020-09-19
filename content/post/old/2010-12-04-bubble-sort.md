---
title: 冒泡排序算法(JAVA)
author: fatkun
type: post
date: 2010-12-03T16:00:18+00:00
url: /2010/12/bubble-sort.html
duoshuo_thread_id:
  - 6300408788688044802
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:4135:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">	<span style="color: #000066; font-weight: bold;">int</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> bubbleSort<span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> a<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    		<span style="color: #666666; font-style: italic;">//每个都进行冒泡(一个一个来)</span>
    		<span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> i <span style="color: #339933;">=</span> <span style="color: #cc66cc;">0</span><span style="color: #339933;">;</span> i <span style="color: #339933;">&lt;</span> a.<span style="color: #006633;">length</span><span style="color: #339933;">;</span> i<span style="color: #339933;">++</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    &nbsp;
    			<span style="color: #666666; font-style: italic;">//和前n-i个比较，把最大的数沉下去</span>
    			<span style="color: #000066; font-weight: bold;">int</span> temp<span style="color: #339933;">;</span>
    			<span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> j <span style="color: #339933;">=</span> <span style="color: #cc66cc;">0</span><span style="color: #339933;">;</span> j <span style="color: #339933;">&lt;</span> a.<span style="color: #006633;">length</span> <span style="color: #339933;">-</span> i <span style="color: #339933;">-</span> <span style="color: #cc66cc;">1</span><span style="color: #339933;">;</span> j<span style="color: #339933;">++</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    				<span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>a<span style="color: #009900;">&#91;</span>j<span style="color: #009900;">&#93;</span> <span style="color: #339933;">&gt;</span> a<span style="color: #009900;">&#91;</span>j <span style="color: #339933;">+</span> <span style="color: #cc66cc;">1</span><span style="color: #009900;">&#93;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    					<span style="color: #666666; font-style: italic;">//交换</span>
    					temp <span style="color: #339933;">=</span> a<span style="color: #009900;">&#91;</span>j<span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span>
    					a<span style="color: #009900;">&#91;</span>j<span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> a<span style="color: #009900;">&#91;</span>j <span style="color: #339933;">+</span> <span style="color: #cc66cc;">1</span><span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span>
    					a<span style="color: #009900;">&#91;</span>j <span style="color: #339933;">+</span> <span style="color: #cc66cc;">1</span><span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> temp<span style="color: #339933;">;</span>
    				<span style="color: #009900;">&#125;</span>
    			<span style="color: #009900;">&#125;</span>
    		<span style="color: #009900;">&#125;</span>
    		<span style="color: #000000; font-weight: bold;">return</span> a<span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">	int[] bubbleSort(int[] a) {
    		//每个都进行冒泡(一个一个来)
    		for (int i = 0; i &lt; a.length; i++) {
    
    			//和前n-i个比较，把最大的数沉下去
    			int temp;
    			for (int j = 0; j &lt; a.length - i - 1; j++) {
    				if (a[j] &gt; a[j + 1]) {
    					//交换
    					temp = a[j];
    					a[j] = a[j + 1];
    					a[j + 1] = temp;
    				}
    			}
    		}
    		return a;
    	}</p></div>
    ";}
categories:
  - J2EE
tags:
  - 冒泡排序
  - 排序算法
  - 算法

---
冒泡排序：和每一个比较，如果比后面大则交换，最终每一趟结果是最大值会沉到后面。  
时间复杂度O(n<sup>2</sup>)，最佳情况是已排好序只比较n-1次，不用交换。
<pre escaped="true" lang="java">int[] bubbleSort(int[] a) {
		//每个都进行冒泡(一个一个来)
		for (int i = 0; i &lt; a.length; i++) {

			//和前n-i个比较，把最大的数沉下去
			int temp;
			for (int j = 0; j &lt; a.length - i - 1; j++) {
				if (a[j] &gt; a[j + 1]) {
					//交换
					temp = a[j];
					a[j] = a[j + 1];
					a[j + 1] = temp;
				}
			}
		}
		return a;
	}</pre>