---
title: 快速排序算法(JAVA版)
author: fatkun
type: post
date: 2010-12-04T02:57:47+00:00
url: /2010/12/quick-sort-java.html
duoshuo_thread_id:
  - 6300408788734182145
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:7666:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="line_numbers"><pre>1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13
    14
    15
    16
    17
    18
    19
    20
    21
    22
    23
    24
    25
    26
    27
    28
    29
    30
    31
    32
    33
    34
    35
    36
    37
    </pre></td><td class="code"><pre class="java" style="font-family:monospace;">	<span style="color: #666666; font-style: italic;">/*
    	 * 快速排序：选一个值pivokey(一般是第一个),小于pivokey放在左边，大于pivokey放在右边，分成两个序列，递归直到low &gt;= high
    	 * 步骤：
    	 * 1，设定两个指针low,high。初值是0和数组长度-1，指定关键字pivokey
    	 * 2，从high所指的位置向前找，找到一个比pivokey小的，和关键字交换值(arr[low] = arr[high])
    	 * 3，从low所指的位置向后找，找到一个比pivokey大的，和关键字交换值
    	 * 4，直到low&gt;=high，把关键字赋值arr[low]=pivokey
    	 * 5，递归分出的两个序列[lowStart,low-1]  [low+1,highEnd]
    	 * */</span>
    	<span style="color: #000066; font-weight: bold;">int</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> quickSort<span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> arr, <span style="color: #000066; font-weight: bold;">int</span> low, <span style="color: #000066; font-weight: bold;">int</span> high<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    		<span style="color: #666666; font-style: italic;">//为后面的递归使用</span>
    		<span style="color: #000066; font-weight: bold;">int</span> lowStart <span style="color: #339933;">=</span> low<span style="color: #339933;">;</span>
    		<span style="color: #000066; font-weight: bold;">int</span> highEnd <span style="color: #339933;">=</span> high<span style="color: #339933;">;</span>
    		<span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>low <span style="color: #339933;">&lt;</span> high<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    			<span style="color: #000066; font-weight: bold;">int</span> pivokey <span style="color: #339933;">=</span> arr<span style="color: #009900;">&#91;</span>low<span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span>
    			<span style="color: #000000; font-weight: bold;">while</span> <span style="color: #009900;">&#40;</span>low <span style="color: #339933;">&lt;</span> high<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    				<span style="color: #666666; font-style: italic;">//如果都是大于pivokey，high指针往前移</span>
    				<span style="color: #000000; font-weight: bold;">while</span> <span style="color: #009900;">&#40;</span>low <span style="color: #339933;">&lt;</span> high <span style="color: #339933;">&amp;&amp;</span> arr<span style="color: #009900;">&#91;</span>high<span style="color: #009900;">&#93;</span> <span style="color: #339933;">&gt;</span> pivokey<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    					high<span style="color: #339933;">--;</span>
    				<span style="color: #009900;">&#125;</span>
    				<span style="color: #666666; font-style: italic;">//这里low++是先把arr[low]赋值为arr[high]，再low+=1，因为这个值是比pivokey小的，下一次不用比较了</span>
    				<span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>low <span style="color: #339933;">&lt;</span> high<span style="color: #009900;">&#41;</span>
    				arr<span style="color: #009900;">&#91;</span>low<span style="color: #339933;">++</span><span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> arr<span style="color: #009900;">&#91;</span>high<span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span>
    				<span style="color: #666666; font-style: italic;">//如果都是小于pivokey，low指针往后移</span>
    				<span style="color: #000000; font-weight: bold;">while</span> <span style="color: #009900;">&#40;</span>low <span style="color: #339933;">&lt;</span> high <span style="color: #339933;">&amp;&amp;</span> arr<span style="color: #009900;">&#91;</span>low<span style="color: #009900;">&#93;</span> <span style="color: #339933;">&lt;</span> pivokey<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    					low<span style="color: #339933;">++;</span>
    				<span style="color: #009900;">&#125;</span>
    				<span style="color: #666666; font-style: italic;">//这里的high--和上面同理</span>
    				<span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>low <span style="color: #339933;">&lt;</span> high<span style="color: #009900;">&#41;</span>
    				arr<span style="color: #009900;">&#91;</span>high<span style="color: #339933;">--</span><span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> arr<span style="color: #009900;">&#91;</span>low<span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span>
    			<span style="color: #009900;">&#125;</span>
    			arr<span style="color: #009900;">&#91;</span>low<span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> pivokey<span style="color: #339933;">;</span>
    			quickSort<span style="color: #009900;">&#40;</span>arr, lowStart, low <span style="color: #339933;">-</span> <span style="color: #cc66cc;">1</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    			quickSort<span style="color: #009900;">&#40;</span>arr, low <span style="color: #339933;">+</span> <span style="color: #cc66cc;">1</span>, highEnd<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #009900;">&#125;</span>
    		<span style="color: #000000; font-weight: bold;">return</span> arr<span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">	/*
    	 * 快速排序：选一个值pivokey(一般是第一个),小于pivokey放在左边，大于pivokey放在右边，分成两个序列，递归直到low &gt;= high
    	 * 步骤：
    	 * 1，设定两个指针low,high。初值是0和数组长度-1，指定关键字pivokey
    	 * 2，从high所指的位置向前找，找到一个比pivokey小的，和关键字交换值(arr[low] = arr[high])
    	 * 3，从low所指的位置向后找，找到一个比pivokey大的，和关键字交换值
    	 * 4，直到low&gt;=high，把关键字赋值arr[low]=pivokey
    	 * 5，递归分出的两个序列[lowStart,low-1]  [low+1,highEnd]
    	 * */
    	int[] quickSort(int[] arr, int low, int high) {
    		//为后面的递归使用
    		int lowStart = low;
    		int highEnd = high;
    		if (low &lt; high) {
    			int pivokey = arr[low];
    			while (low &lt; high) {
    				//如果都是大于pivokey，high指针往前移
    				while (low &lt; high &amp;&amp; arr[high] &gt; pivokey) {
    					high--;
    				}
    				//这里low++是先把arr[low]赋值为arr[high]，再low+=1，因为这个值是比pivokey小的，下一次不用比较了
    				if (low &lt; high)
    				arr[low++] = arr[high];
    				//如果都是小于pivokey，low指针往后移
    				while (low &lt; high &amp;&amp; arr[low] &lt; pivokey) {
    					low++;
    				}
    				//这里的high--和上面同理
    				if (low &lt; high)
    				arr[high--] = arr[low];
    			}
    			arr[low] = pivokey;
    			quickSort(arr, lowStart, low - 1);
    			quickSort(arr, low + 1, highEnd);
    		}
    		return arr;
    	}</p></div>
    ";}
categories:
  - J2EE
tags:
  - 快速排序
  - 排序算法
  - 算法

---
快速排序是不稳定的排序方法，平均时间复杂度为O(nlogn)，空间复杂度为O(logn)，最差时是有序或基本有序时，算法退化为冒泡排序，时间复杂度是O(n<sup>2</sup>)
<pre escaped="true" lang="java" line="1">/*
	 * 快速排序：选一个值pivokey(一般是第一个),小于pivokey放在左边，大于pivokey放在右边，分成两个序列，递归直到low &gt;= high
	 * 步骤：
	 * 1，设定两个指针low,high。初值是0和数组长度-1，指定关键字pivokey
	 * 2，从high所指的位置向前找，找到一个比pivokey小的，和关键字交换值(arr[low] = arr[high])
	 * 3，从low所指的位置向后找，找到一个比pivokey大的，和关键字交换值
	 * 4，直到low&gt;=high，把关键字赋值arr[low]=pivokey
	 * 5，递归分出的两个序列[lowStart,low-1]  [low+1,highEnd]
	 * */
	int[] quickSort(int[] arr, int low, int high) {
		//为后面的递归使用
		int lowStart = low;
		int highEnd = high;
		if (low &lt; high) {
			int pivokey = arr[low];
			while (low &lt; high) {
				//如果都是大于pivokey，high指针往前移
				while (low &lt; high && arr[high] &gt; pivokey) {
					high--;
				}
				//这里low++是先把arr[low]赋值为arr[high]，再low+=1，因为这个值是比pivokey小的，下一次不用比较了
				if (low &lt; high)
				arr[low++] = arr[high];
				//如果都是小于pivokey，low指针往后移
				while (low &lt; high && arr[low] &lt; pivokey) {
					low++;
				}
				//这里的high--和上面同理
				if (low &lt; high)
				arr[high--] = arr[low];
			}
			arr[low] = pivokey;
			quickSort(arr, lowStart, low - 1);
			quickSort(arr, low + 1, highEnd);
		}
		return arr;
	}</pre>