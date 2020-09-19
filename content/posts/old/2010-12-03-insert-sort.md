---
title: 直接插入排序算法（JAVA版）
author: fatkun
type: post
date: 2010-12-03T02:23:31+00:00
url: /2010/12/insert-sort.html
duoshuo_thread_id:
  - 6300408788620935938
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:10240:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> Paixu <span style="color: #009900;">&#123;</span>
    &nbsp;
    	<span style="color: #008000; font-style: italic; font-weight: bold;">/**
    	 * @param args
    	 */</span>
    	<span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000066; font-weight: bold;">void</span> main<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> args<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    		<span style="color: #000066; font-weight: bold;">int</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> a <span style="color: #339933;">=</span> <span style="color: #009900;">&#123;</span><span style="color: #cc66cc;">8</span>,<span style="color: #cc66cc;">4</span>,<span style="color: #cc66cc;">5</span>,<span style="color: #cc66cc;">3</span><span style="color: #009900;">&#125;</span><span style="color: #339933;">;</span>
    		<span style="color: #000066; font-weight: bold;">int</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> insertSorta <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> Paixu<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">insertSort</span><span style="color: #009900;">&#40;</span>a<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		pw<span style="color: #009900;">&#40;</span>insertSorta<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span>
    &nbsp;
    	<span style="color: #666666; font-style: italic;">/*
    http://fatkun.com
    直接插入排序：遍历第二个到最后一个，找到每一个值的最佳位置，插入进去
    1.a[i]和前一个值a[i-1]比较，如果小于前一个值
    2.设此值为temp，把a[i-1]向后移一位a[i]=a[i-1]
    3.检查前面的a[&lt;=i-2]是否有比temp大的，如果比temp大，后移一位
    4.直到一个比temp小的或者j=-1，此时把temp赋值到j+1即可
    &nbsp;
    初始序列：8 4 5 3
    4 8 5 3
    4 5 8 3
    3 4 5 8
    	 */</span>
    	<span style="color: #000066; font-weight: bold;">int</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> insertSort<span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> arr<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    		<span style="color: #000066; font-weight: bold;">int</span> temp<span style="color: #339933;">;</span>
    		<span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> i <span style="color: #339933;">=</span> <span style="color: #cc66cc;">1</span><span style="color: #339933;">;</span> i <span style="color: #339933;">&lt;</span> arr.<span style="color: #006633;">length</span><span style="color: #339933;">;</span> i<span style="color: #339933;">++</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    			pw<span style="color: #009900;">&#40;</span>arr<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    			<span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>arr<span style="color: #009900;">&#91;</span>i<span style="color: #009900;">&#93;</span> <span style="color: #339933;">&lt;</span> arr<span style="color: #009900;">&#91;</span>i <span style="color: #339933;">-</span> <span style="color: #cc66cc;">1</span><span style="color: #009900;">&#93;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span><span style="color: #666666; font-style: italic;">//如果当前值小于前一个</span>
    				temp <span style="color: #339933;">=</span> arr<span style="color: #009900;">&#91;</span>i<span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">//设定岗哨</span>
    				arr<span style="color: #009900;">&#91;</span>i<span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> arr<span style="color: #009900;">&#91;</span>i <span style="color: #339933;">-</span> <span style="color: #cc66cc;">1</span><span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">//把前一个值移到后一位</span>
    &nbsp;
    				<span style="color: #666666; font-style: italic;">//继续和前面的进行比较，如果比temp大，则后移一位</span>
    				<span style="color: #666666; font-style: italic;">//这里j从前两个开始，因为前一个知道必定比temp大了，无需再比较</span>
    				<span style="color: #000066; font-weight: bold;">int</span> j <span style="color: #339933;">=</span> i <span style="color: #339933;">-</span> <span style="color: #cc66cc;">2</span><span style="color: #339933;">;</span>
    				<span style="color: #000000; font-weight: bold;">while</span> <span style="color: #009900;">&#40;</span>j<span style="color: #339933;">&gt;=</span><span style="color: #cc66cc;">0</span> <span style="color: #339933;">&amp;&amp;</span> temp <span style="color: #339933;">&lt;</span> arr<span style="color: #009900;">&#91;</span>j<span style="color: #009900;">&#93;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#123;</span>
    					arr<span style="color: #009900;">&#91;</span>j <span style="color: #339933;">+</span> <span style="color: #cc66cc;">1</span><span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> arr<span style="color: #009900;">&#91;</span>j<span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span>
    					j<span style="color: #339933;">--;</span>
    				<span style="color: #009900;">&#125;</span>
    				<span style="color: #666666; font-style: italic;">//上一个循环结束后，j在最后一个比temp小的位置或者-1，所以j+1，把当前值放在这里</span>
    				arr<span style="color: #009900;">&#91;</span>j <span style="color: #339933;">+</span> <span style="color: #cc66cc;">1</span><span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> temp<span style="color: #339933;">;</span>
    			<span style="color: #009900;">&#125;</span>
    		<span style="color: #009900;">&#125;</span>
    		<span style="color: #000000; font-weight: bold;">return</span> arr<span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span>
    &nbsp;
    	<span style="color: #666666; font-style: italic;">//打印数组</span>
    	<span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000066; font-weight: bold;">void</span> pw<span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> arr<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#123;</span>
    		<span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> i <span style="color: #339933;">:</span> arr<span style="color: #009900;">&#41;</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">print</span><span style="color: #009900;">&#40;</span>i<span style="color: #339933;">+</span><span style="color: #0000ff;">&quot; &quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">public class Paixu {
    
    	/**
    	 * @param args
    	 */
    	public static void main(String[] args) {
    		int[] a = {8,4,5,3};
    		int[] insertSorta = new Paixu().insertSort(a);
    		pw(insertSorta);
    	}
    
    	/*
    http://fatkun.com
    直接插入排序：遍历第二个到最后一个，找到每一个值的最佳位置，插入进去
    1.a[i]和前一个值a[i-1]比较，如果小于前一个值
    2.设此值为temp，把a[i-1]向后移一位a[i]=a[i-1]
    3.检查前面的a[&lt;=i-2]是否有比temp大的，如果比temp大，后移一位
    4.直到一个比temp小的或者j=-1，此时把temp赋值到j+1即可
    
    初始序列：8 4 5 3
    4 8 5 3
    4 5 8 3
    3 4 5 8
    	 */
    	int[] insertSort(int[] arr) {
    		int temp;
    		for (int i = 1; i &lt; arr.length; i++) {
    			pw(arr);
    			if (arr[i] &lt; arr[i - 1]) {//如果当前值小于前一个
    				temp = arr[i]; //设定岗哨
    				arr[i] = arr[i - 1]; //把前一个值移到后一位
    
    				//继续和前面的进行比较，如果比temp大，则后移一位
    				//这里j从前两个开始，因为前一个知道必定比temp大了，无需再比较
    				int j = i - 2;
    				while (j&gt;=0 &amp;&amp; temp &lt; arr[j]){
    					arr[j + 1] = arr[j];
    					j--;
    				}
    				//上一个循环结束后，j在最后一个比temp小的位置或者-1，所以j+1，把当前值放在这里
    				arr[j + 1] = temp;
    			}
    		}
    		return arr;
    	}
    
    	//打印数组
    	private static void pw(int[] arr){
    		for (int i : arr)
    		System.out.print(i+&quot; &quot;);
    		System.out.println(&quot;&quot;);
    	}
    
    }</p></div>
    ";i:2;s:4357:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">	<span style="color: #000066; font-weight: bold;">int</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> insertSort<span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> arr<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    		<span style="color: #000066; font-weight: bold;">int</span> temp<span style="color: #339933;">;</span>
    		<span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> i <span style="color: #339933;">=</span> <span style="color: #cc66cc;">1</span><span style="color: #339933;">;</span> i <span style="color: #339933;">&lt;</span> arr.<span style="color: #006633;">length</span><span style="color: #339933;">;</span> i<span style="color: #339933;">++</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    			pw<span style="color: #009900;">&#40;</span>arr<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    			<span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>arr<span style="color: #009900;">&#91;</span>i<span style="color: #009900;">&#93;</span> <span style="color: #339933;">&lt;</span> arr<span style="color: #009900;">&#91;</span>i <span style="color: #339933;">-</span> <span style="color: #cc66cc;">1</span><span style="color: #009900;">&#93;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    				temp <span style="color: #339933;">=</span> arr<span style="color: #009900;">&#91;</span>i<span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span>
    				<span style="color: #666666; font-style: italic;">//这里和前面不太一样，从i的前一个就开始比较，也就是判断前面所有元素（多判断了一次arr[i]和arr[i-1]）</span>
    				<span style="color: #000066; font-weight: bold;">int</span> j <span style="color: #339933;">=</span> i <span style="color: #339933;">-</span> <span style="color: #cc66cc;">1</span><span style="color: #339933;">;</span>
    				<span style="color: #000000; font-weight: bold;">while</span> <span style="color: #009900;">&#40;</span>j<span style="color: #339933;">&gt;=</span><span style="color: #cc66cc;">0</span> <span style="color: #339933;">&amp;&amp;</span> temp <span style="color: #339933;">&lt;</span> arr<span style="color: #009900;">&#91;</span>j<span style="color: #009900;">&#93;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#123;</span>
    					arr<span style="color: #009900;">&#91;</span>j <span style="color: #339933;">+</span> <span style="color: #cc66cc;">1</span><span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> arr<span style="color: #009900;">&#91;</span>j<span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span>
    					j<span style="color: #339933;">--;</span>
    				<span style="color: #009900;">&#125;</span>
    				arr<span style="color: #009900;">&#91;</span>j <span style="color: #339933;">+</span> <span style="color: #cc66cc;">1</span><span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> temp<span style="color: #339933;">;</span>
    			<span style="color: #009900;">&#125;</span>
    		<span style="color: #009900;">&#125;</span>
    		<span style="color: #000000; font-weight: bold;">return</span> arr<span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">	int[] insertSort(int[] arr) {
    		int temp;
    		for (int i = 1; i &lt; arr.length; i++) {
    			pw(arr);
    			if (arr[i] &lt; arr[i - 1]) {
    				temp = arr[i];
    				//这里和前面不太一样，从i的前一个就开始比较，也就是判断前面所有元素（多判断了一次arr[i]和arr[i-1]）
    				int j = i - 1;
    				while (j&gt;=0 &amp;&amp; temp &lt; arr[j]){
    					arr[j + 1] = arr[j];
    					j--;
    				}
    				arr[j + 1] = temp;
    			}
    		}
    		return arr;
    	}</p></div>
    ";}
categories:
  - J2EE
tags:
  - 排序算法
  - 数据结构
  - 直接插入
  - 算法

---
时间复杂度：O(n*n)
直接插入排序：遍历第二个到最后一个，找到每一个值的最佳位置，插进去：）  
1.a[i]和前一个值a[i-1]比较，如果小于前一个值  
2.设此值为temp，把a[i-1]向后移一位a[i]=a[i-1]  
3.检查前面的a[<=i-2]是否有比temp大的，如果比temp大，后移一位  
4.直到一个比temp小的或者j=-1，此时把temp赋值到j+1即可
举例子：  
**原序列**：8 4 5 3  
**第一次** 4 8 5 3  
**第二次** 5<8，所以temp = 5, 序列变成 4 8 8 3,然后和i-2=0前面的4比较大小，5>4，所以5应该在1的位置上，把temp赋值到1位置上，4 5 8 3  
**第三次** 3<8，所以temp = 3, 序列变成 4 5 8 8,然后和i-2=2前面的5比较大小，3>5，序列变成 4 5 5 8,再比较3>4，序列变成 4 4 5 8，此时j=-1，那temp肯定在0位上，最终序列3 4 5 8
<pre lang="java" escaped="true">public class Paixu {

	/**
	 * @param args
	 */
	public static void main(String[] args) {
		int[] a = {8,4,5,3};
		int[] insertSorta = new Paixu().insertSort(a);
		pw(insertSorta);
	}

	/*
http://fatkun.com
直接插入排序：遍历第二个到最后一个，找到每一个值的最佳位置，插入进去
1.a[i]和前一个值a[i-1]比较，如果小于前一个值
2.设此值为temp，把a[i-1]向后移一位a[i]=a[i-1]
3.检查前面的a[&lt;=i-2]是否有比temp大的，如果比temp大，后移一位
4.直到一个比temp小的或者j=-1，此时把temp赋值到j+1即可

初始序列：8 4 5 3
4 8 5 3
4 5 8 3
3 4 5 8
	 */
	int[] insertSort(int[] arr) {
		int temp;
		for (int i = 1; i &lt; arr.length; i++) {
			pw(arr);
			if (arr[i] &lt; arr[i - 1]) {//如果当前值小于前一个
				temp = arr[i]; //设定岗哨
				arr[i] = arr[i - 1]; //把前一个值移到后一位

				//继续和前面的进行比较，如果比temp大，则后移一位
				//这里j从前两个开始，因为前一个知道必定比temp大了，无需再比较
				int j = i - 2;
				while (j&gt;=0 && temp &lt; arr[j]){
					arr[j + 1] = arr[j];
					j--;
				}
				//上一个循环结束后，j在最后一个比temp小的位置或者-1，所以j+1，把当前值放在这里
				arr[j + 1] = temp;
			}
		}
		return arr;
	}

	//打印数组
	private static void pw(int[] arr){
		for (int i : arr)
		System.out.print(i+" ");
		System.out.println("");
	}

}</pre>
**简化一些，去掉一些注释，代码基本一样**
<pre lang="java" escaped="true">int[] insertSort(int[] arr) {
		int temp;
		for (int i = 1; i &lt; arr.length; i++) {
			pw(arr);
			if (arr[i] &lt; arr[i - 1]) {
				temp = arr[i];
				//这里和前面不太一样，从i的前一个就开始比较，也就是判断前面所有元素（多判断了一次arr[i]和arr[i-1]）
				int j = i - 1;
				while (j&gt;=0 && temp &lt; arr[j]){
					arr[j + 1] = arr[j];
					j--;
				}
				arr[j + 1] = temp;
			}
		}
		return arr;
	}</pre>