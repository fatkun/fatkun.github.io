---
title: 选择排序算法(JAVA版)
author: fatkun
type: post
date: 2010-12-04T15:24:59+00:00
url: /2010/12/select-sort-java.html
duoshuo_thread_id:
  - 6300408788788708097
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:8010:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> Test <span style="color: #009900;">&#123;</span>
    	<span style="color: #666666; font-style: italic;">/*
    	 * 选择排序：选择最小/大的放在前面，每一趟前几个按序排列
    	 */</span>
    	<span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000066; font-weight: bold;">int</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> selectSort<span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> arr<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    		<span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> i <span style="color: #339933;">=</span> <span style="color: #cc66cc;">0</span><span style="color: #339933;">;</span> i <span style="color: #339933;">&lt;</span> arr.<span style="color: #006633;">length</span> <span style="color: #339933;">-</span> <span style="color: #cc66cc;">1</span><span style="color: #339933;">;</span> i<span style="color: #339933;">++</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    			<span style="color: #000066; font-weight: bold;">int</span> k <span style="color: #339933;">=</span> i<span style="color: #339933;">;</span>
    			<span style="color: #000066; font-weight: bold;">int</span> min <span style="color: #339933;">=</span> arr<span style="color: #009900;">&#91;</span>i<span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span>
    			<span style="color: #666666; font-style: italic;">// 和i后面的每一个比较，如果有比i小的记下下标k</span>
    			<span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> j <span style="color: #339933;">=</span> i <span style="color: #339933;">+</span> <span style="color: #cc66cc;">1</span><span style="color: #339933;">;</span> j <span style="color: #339933;">&lt;</span> arr.<span style="color: #006633;">length</span><span style="color: #339933;">;</span> j<span style="color: #339933;">++</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    				<span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>arr<span style="color: #009900;">&#91;</span>j<span style="color: #009900;">&#93;</span> <span style="color: #339933;">&lt;</span> min<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    					k <span style="color: #339933;">=</span> j<span style="color: #339933;">;</span>
    					min <span style="color: #339933;">=</span> arr<span style="color: #009900;">&#91;</span>j<span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span>
    				<span style="color: #009900;">&#125;</span>
    			<span style="color: #009900;">&#125;</span>
    			<span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>k <span style="color: #339933;">!=</span> i<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span><span style="color: #666666; font-style: italic;">// 交换</span>
    				<span style="color: #000066; font-weight: bold;">int</span> temp <span style="color: #339933;">=</span> arr<span style="color: #009900;">&#91;</span>i<span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span>
    				arr<span style="color: #009900;">&#91;</span>i<span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> arr<span style="color: #009900;">&#91;</span>k<span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span>
    				arr<span style="color: #009900;">&#91;</span>k<span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> temp<span style="color: #339933;">;</span>
    			<span style="color: #009900;">&#125;</span>
    		<span style="color: #009900;">&#125;</span>
    		<span style="color: #000000; font-weight: bold;">return</span> arr<span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span>
    &nbsp;
    	<span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000066; font-weight: bold;">void</span> main<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> args<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    		<span style="color: #000066; font-weight: bold;">int</span> arr<span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #000066; font-weight: bold;">int</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> <span style="color: #009900;">&#123;</span> <span style="color: #cc66cc;">1</span>, <span style="color: #cc66cc;">5</span>, <span style="color: #cc66cc;">7</span>, <span style="color: #cc66cc;">2</span>, <span style="color: #cc66cc;">6</span>, <span style="color: #cc66cc;">0</span> <span style="color: #009900;">&#125;</span><span style="color: #339933;">;</span>
    		<span style="color: #000066; font-weight: bold;">int</span> newarr<span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> selectSort<span style="color: #009900;">&#40;</span>arr<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;----------------------&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
    		<span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> i <span style="color: #339933;">:</span> newarr<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    			<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>i<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #009900;">&#125;</span>
    	<span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">public class Test {
    	/*
    	 * 选择排序：选择最小/大的放在前面，每一趟前几个按序排列
    	 */
    	static int[] selectSort(int[] arr) {
    		for (int i = 0; i &lt; arr.length - 1; i++) {
    			int k = i;
    			int min = arr[i];
    			// 和i后面的每一个比较，如果有比i小的记下下标k
    			for (int j = i + 1; j &lt; arr.length; j++) {
    				if (arr[j] &lt; min) {
    					k = j;
    					min = arr[j];
    				}
    			}
    			if (k != i) {// 交换
    				int temp = arr[i];
    				arr[i] = arr[k];
    				arr[k] = temp;
    			}
    		}
    		return arr;
    	}
    
    	public static void main(String[] args) {
    		int arr[] = new int[] { 1, 5, 7, 2, 6, 0 };
    		int newarr[] = selectSort(arr);
    		
    		System.out.println(&quot;----------------------&quot;);
    		
    		for (int i : newarr) {
    			System.out.println(i);
    		}
    	}
    }</p></div>
    ";}
categories:
  - J2EE
tags:
  - 排序算法
  - 数据结构
  - 算法
  - 选择排序

---
选择排序和插入排序差不多，交换的次数减少。平均/最好/最坏时间复杂度是O(n<sup>2</sup>)，是不稳定的排序算法。（插入排序是稳定排序算法）
update:以前写错了一个地方，应该每次要把最小值找出来，记下来，每次和最小值去比较，目的就是为了从后面找到最小的值。
<pre escaped="true" lang="java">public class Test {
	/*
	 * 选择排序：选择最小/大的放在前面，每一趟前几个按序排列
	 */
	static int[] selectSort(int[] arr) {
		for (int i = 0; i &lt; arr.length - 1; i++) {
			int k = i;
			int min = arr[i];
			// 和i后面的每一个比较，如果有比i小的记下下标k
			for (int j = i + 1; j &lt; arr.length; j++) {
				if (arr[j] &lt; min) {
					k = j;
					min = arr[j];
				}
			}
			if (k != i) {// 交换
				int temp = arr[i];
				arr[i] = arr[k];
				arr[k] = temp;
			}
		}
		return arr;
	}

	public static void main(String[] args) {
		int arr[] = new int[] { 1, 5, 7, 2, 6, 0 };
		int newarr[] = selectSort(arr);
		
		System.out.println("----------------------");
		
		for (int i : newarr) {
			System.out.println(i);
		}
	}
}
</pre>