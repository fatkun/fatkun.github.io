---
title: JDK源码分析：java.lang.String
author: fatkun
type: post
date: 2011-03-10T15:24:57+00:00
url: /2011/03/jdk-source-java-lang-string.html
duoshuo_thread_id:
  - 6300408802848015105
wp-syntax-cache-content:
  - |
    a:5:{i:1;s:1702:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">   <span style="color: #008000; font-style: italic; font-weight: bold;">/** The value is used for character storage. */</span>
        <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000000; font-weight: bold;">final</span> <span style="color: #000066; font-weight: bold;">char</span> value<span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #008000; font-style: italic; font-weight: bold;">/** The offset is the first index of the storage that is used. */</span>
        <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000000; font-weight: bold;">final</span> <span style="color: #000066; font-weight: bold;">int</span> offset<span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #008000; font-style: italic; font-weight: bold;">/** The count is the number of characters in the String. */</span>
        <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000000; font-weight: bold;">final</span> <span style="color: #000066; font-weight: bold;">int</span> count<span style="color: #339933;">;</span></pre></td></tr></table><p class="theCode" style="display:none;">   /** The value is used for character storage. */
        private final char value[];
    
        /** The offset is the first index of the storage that is used. */
        private final int offset;
    
        /** The count is the number of characters in the String. */
        private final int count;</p></div>
    ";i:2;s:2922:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #003399;">String</span> concat<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> str<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    	<span style="color: #000066; font-weight: bold;">int</span> otherLen <span style="color: #339933;">=</span> str.<span style="color: #006633;">length</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	<span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>otherLen <span style="color: #339933;">==</span> <span style="color: #cc66cc;">0</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    	    <span style="color: #000000; font-weight: bold;">return</span> <span style="color: #000000; font-weight: bold;">this</span><span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span>
    	<span style="color: #000066; font-weight: bold;">char</span> buf<span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #000066; font-weight: bold;">char</span><span style="color: #009900;">&#91;</span>count <span style="color: #339933;">+</span> otherLen<span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span>
    	getChars<span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">0</span>, count, buf, <span style="color: #cc66cc;">0</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	str.<span style="color: #006633;">getChars</span><span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">0</span>, otherLen, buf, count<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	<span style="color: #000000; font-weight: bold;">return</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">String</span><span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">0</span>, count <span style="color: #339933;">+</span> otherLen, buf<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">    public String concat(String str) {
    	int otherLen = str.length();
    	if (otherLen == 0) {
    	    return this;
    	}
    	char buf[] = new char[count + otherLen];
    	getChars(0, count, buf, 0);
    	str.getChars(0, otherLen, buf, count);
    	return new String(0, count + otherLen, buf);
        }</p></div>
    ";i:3;s:11224:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">int</span> indexOf<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> str, <span style="color: #000066; font-weight: bold;">int</span> fromIndex<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">return</span> indexOf<span style="color: #009900;">&#40;</span>value, offset, count,
                           str.<span style="color: #006633;">value</span>, str.<span style="color: #006633;">offset</span>, str.<span style="color: #006633;">count</span>, fromIndex<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        <span style="color: #666666; font-style: italic;">//source源字符，sourceOffset源偏移，sourceCount源长度</span>
        <span style="color: #666666; font-style: italic;">//target查找的字符 ...</span>
        <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000066; font-weight: bold;">int</span> indexOf<span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">char</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> source, <span style="color: #000066; font-weight: bold;">int</span> sourceOffset, <span style="color: #000066; font-weight: bold;">int</span> sourceCount,
                           <span style="color: #000066; font-weight: bold;">char</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> target, <span style="color: #000066; font-weight: bold;">int</span> targetOffset, <span style="color: #000066; font-weight: bold;">int</span> targetCount,
                           <span style="color: #000066; font-weight: bold;">int</span> fromIndex<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #666666; font-style: italic;">//如果fromIndex比源字符还长(从0算起)，并且查找的字符长度为0，那就返回源字符的长度，否则返回-1</span>
    	<span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>fromIndex <span style="color: #339933;">&gt;=</span> sourceCount<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                <span style="color: #000000; font-weight: bold;">return</span> <span style="color: #009900;">&#40;</span>targetCount <span style="color: #339933;">==</span> <span style="color: #cc66cc;">0</span> <span style="color: #339933;">?</span> sourceCount <span style="color: #339933;">:</span> <span style="color: #339933;">-</span><span style="color: #cc66cc;">1</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span>
        	<span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>fromIndex <span style="color: #339933;">&lt;</span> <span style="color: #cc66cc;">0</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
        	    fromIndex <span style="color: #339933;">=</span> <span style="color: #cc66cc;">0</span><span style="color: #339933;">;</span>
        	<span style="color: #009900;">&#125;</span>
            <span style="color: #666666; font-style: italic;">//如果fromIndex比源字符短，查找的字符长度为0，直接返回fromIndex</span>
    	<span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>targetCount <span style="color: #339933;">==</span> <span style="color: #cc66cc;">0</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    	    <span style="color: #000000; font-weight: bold;">return</span> fromIndex<span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span>
    &nbsp;
            <span style="color: #666666; font-style: italic;">//先取出第一个字符</span>
            <span style="color: #000066; font-weight: bold;">char</span> first  <span style="color: #339933;">=</span> target<span style="color: #009900;">&#91;</span>targetOffset<span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span>
            <span style="color: #000066; font-weight: bold;">int</span> max <span style="color: #339933;">=</span> sourceOffset <span style="color: #339933;">+</span> <span style="color: #009900;">&#40;</span>sourceCount <span style="color: #339933;">-</span> targetCount<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
            <span style="color: #666666; font-style: italic;">//循环每一个字符</span>
            <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> i <span style="color: #339933;">=</span> sourceOffset <span style="color: #339933;">+</span> fromIndex<span style="color: #339933;">;</span> i <span style="color: #339933;">&lt;=</span> max<span style="color: #339933;">;</span> i<span style="color: #339933;">++</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                <span style="color: #666666; font-style: italic;">/* 直到找到第一个字符 */</span>
                <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>source<span style="color: #009900;">&#91;</span>i<span style="color: #009900;">&#93;</span> <span style="color: #339933;">!=</span> first<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                    <span style="color: #000000; font-weight: bold;">while</span> <span style="color: #009900;">&#40;</span><span style="color: #339933;">++</span>i <span style="color: #339933;">&lt;=</span> max <span style="color: #339933;">&amp;&amp;</span> source<span style="color: #009900;">&#91;</span>i<span style="color: #009900;">&#93;</span> <span style="color: #339933;">!=</span> first<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #009900;">&#125;</span>
    &nbsp;
                <span style="color: #666666; font-style: italic;">/* 找到第一个字符后，比较剩下的字符 */</span>
                <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>i <span style="color: #339933;">&lt;=</span> max<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                    <span style="color: #000066; font-weight: bold;">int</span> j <span style="color: #339933;">=</span> i <span style="color: #339933;">+</span> <span style="color: #cc66cc;">1</span><span style="color: #339933;">;</span>
                    <span style="color: #000066; font-weight: bold;">int</span> end <span style="color: #339933;">=</span> j <span style="color: #339933;">+</span> targetCount <span style="color: #339933;">-</span> <span style="color: #cc66cc;">1</span><span style="color: #339933;">;</span>
                    <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> k <span style="color: #339933;">=</span> targetOffset <span style="color: #339933;">+</span> <span style="color: #cc66cc;">1</span><span style="color: #339933;">;</span> j <span style="color: #339933;">&lt;</span> end <span style="color: #339933;">&amp;&amp;</span> source<span style="color: #009900;">&#91;</span>j<span style="color: #009900;">&#93;</span> <span style="color: #339933;">==</span>
                             target<span style="color: #009900;">&#91;</span>k<span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span> j<span style="color: #339933;">++</span>, k<span style="color: #339933;">++</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
                    <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>j <span style="color: #339933;">==</span> end<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                        <span style="color: #666666; font-style: italic;">/* 如果j能到end，那就说明找到整个字符串啦，返回偏移 */</span>
                        <span style="color: #000000; font-weight: bold;">return</span> i <span style="color: #339933;">-</span> sourceOffset<span style="color: #339933;">;</span>
                    <span style="color: #009900;">&#125;</span>
                <span style="color: #009900;">&#125;</span>
            <span style="color: #009900;">&#125;</span>
            <span style="color: #000000; font-weight: bold;">return</span> <span style="color: #339933;">-</span><span style="color: #cc66cc;">1</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">    public int indexOf(String str, int fromIndex) {
            return indexOf(value, offset, count,
                           str.value, str.offset, str.count, fromIndex);
        }
        
        //source源字符，sourceOffset源偏移，sourceCount源长度
        //target查找的字符 ...
        static int indexOf(char[] source, int sourceOffset, int sourceCount,
                           char[] target, int targetOffset, int targetCount,
                           int fromIndex) {
            //如果fromIndex比源字符还长(从0算起)，并且查找的字符长度为0，那就返回源字符的长度，否则返回-1
    	if (fromIndex &gt;= sourceCount) {
                return (targetCount == 0 ? sourceCount : -1);
    	}
        	if (fromIndex &lt; 0) {
        	    fromIndex = 0;
        	}
            //如果fromIndex比源字符短，查找的字符长度为0，直接返回fromIndex
    	if (targetCount == 0) {
    	    return fromIndex;
    	}
    
            //先取出第一个字符
            char first  = target[targetOffset];
            int max = sourceOffset + (sourceCount - targetCount);
    
            //循环每一个字符
            for (int i = sourceOffset + fromIndex; i &lt;= max; i++) {
                /* 直到找到第一个字符 */
                if (source[i] != first) {
                    while (++i &lt;= max &amp;&amp; source[i] != first);
                }
    
                /* 找到第一个字符后，比较剩下的字符 */
                if (i &lt;= max) {
                    int j = i + 1;
                    int end = j + targetCount - 1;
                    for (int k = targetOffset + 1; j &lt; end &amp;&amp; source[j] ==
                             target[k]; j++, k++);
    
                    if (j == end) {
                        /* 如果j能到end，那就说明找到整个字符串啦，返回偏移 */
                        return i - sourceOffset;
                    }
                }
            }
            return -1;
        }</p></div>
    ";i:4;s:4829:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">boolean</span> equals<span style="color: #009900;">&#40;</span><span style="color: #003399;">Object</span> anObject<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    	<span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">this</span> <span style="color: #339933;">==</span> anObject<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    	    <span style="color: #000000; font-weight: bold;">return</span> <span style="color: #000066; font-weight: bold;">true</span><span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span>
    	<span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>anObject <span style="color: #000000; font-weight: bold;">instanceof</span> <span style="color: #003399;">String</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    	    <span style="color: #003399;">String</span> anotherString <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span><span style="color: #009900;">&#41;</span>anObject<span style="color: #339933;">;</span>
    	    <span style="color: #000066; font-weight: bold;">int</span> n <span style="color: #339933;">=</span> count<span style="color: #339933;">;</span>
    	    <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>n <span style="color: #339933;">==</span> anotherString.<span style="color: #006633;">count</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    		<span style="color: #000066; font-weight: bold;">char</span> v1<span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> value<span style="color: #339933;">;</span>
    		<span style="color: #000066; font-weight: bold;">char</span> v2<span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> anotherString.<span style="color: #006633;">value</span><span style="color: #339933;">;</span>
    		<span style="color: #000066; font-weight: bold;">int</span> i <span style="color: #339933;">=</span> offset<span style="color: #339933;">;</span>
    		<span style="color: #000066; font-weight: bold;">int</span> j <span style="color: #339933;">=</span> anotherString.<span style="color: #006633;">offset</span><span style="color: #339933;">;</span>
    		<span style="color: #000000; font-weight: bold;">while</span> <span style="color: #009900;">&#40;</span>n<span style="color: #339933;">--</span> <span style="color: #339933;">!=</span> <span style="color: #cc66cc;">0</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    		    <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>v1<span style="color: #009900;">&#91;</span>i<span style="color: #339933;">++</span><span style="color: #009900;">&#93;</span> <span style="color: #339933;">!=</span> v2<span style="color: #009900;">&#91;</span>j<span style="color: #339933;">++</span><span style="color: #009900;">&#93;</span><span style="color: #009900;">&#41;</span>
    			<span style="color: #000000; font-weight: bold;">return</span> <span style="color: #000066; font-weight: bold;">false</span><span style="color: #339933;">;</span>
    		<span style="color: #009900;">&#125;</span>
    		<span style="color: #000000; font-weight: bold;">return</span> <span style="color: #000066; font-weight: bold;">true</span><span style="color: #339933;">;</span>
    	    <span style="color: #009900;">&#125;</span>
    	<span style="color: #009900;">&#125;</span>
    	<span style="color: #000000; font-weight: bold;">return</span> <span style="color: #000066; font-weight: bold;">false</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">    public boolean equals(Object anObject) {
    	if (this == anObject) {
    	    return true;
    	}
    	if (anObject instanceof String) {
    	    String anotherString = (String)anObject;
    	    int n = count;
    	    if (n == anotherString.count) {
    		char v1[] = value;
    		char v2[] = anotherString.value;
    		int i = offset;
    		int j = anotherString.offset;
    		while (n-- != 0) {
    		    if (v1[i++] != v2[j++])
    			return false;
    		}
    		return true;
    	    }
    	}
    	return false;
        }</p></div>
    ";i:5;s:2971:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #003399;">String</span> replace<span style="color: #009900;">&#40;</span>CharSequence target, CharSequence replacement<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">return</span> Pattern.<span style="color: #006633;">compile</span><span style="color: #009900;">&#40;</span>target.<span style="color: #006633;">toString</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, Pattern.<span style="color: #006633;">LITERAL</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">matcher</span><span style="color: #009900;">&#40;</span>
                <span style="color: #000000; font-weight: bold;">this</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">replaceAll</span><span style="color: #009900;">&#40;</span>Matcher.<span style="color: #006633;">quoteReplacement</span><span style="color: #009900;">&#40;</span>replacement.<span style="color: #006633;">toString</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #003399;">String</span> replaceAll<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> regex, <span style="color: #003399;">String</span> replacement<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    	<span style="color: #000000; font-weight: bold;">return</span> Pattern.<span style="color: #006633;">compile</span><span style="color: #009900;">&#40;</span>regex<span style="color: #009900;">&#41;</span>.<span style="color: #006633;">matcher</span><span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">this</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">replaceAll</span><span style="color: #009900;">&#40;</span>replacement<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">    public String replace(CharSequence target, CharSequence replacement) {
            return Pattern.compile(target.toString(), Pattern.LITERAL).matcher(
                this).replaceAll(Matcher.quoteReplacement(replacement.toString()));
        }
    
        public String replaceAll(String regex, String replacement) {
    	return Pattern.compile(regex).matcher(this).replaceAll(replacement);
        }</p></div>
    ";}
categories:
  - J2EE
tags:
  - JAVA
  - JDK源码分析
  - String

---
最近开始看JDK源码，不能太懒了~~注释非常详细（虽然是英文），而且部分代码也不算很复杂。先挑的简单的看看。。为了坚持下去，所以在博客写些记录，一是为了记忆，二是给自己一个坚持的理由~~哇咔咔，英文不算很好，那就对着中文API一起看吧。。
## String结构

这个类结构很简单。。
<pre escaped="true" lang="java">/** The value is used for character storage. */
    private final char value[];

    /** The offset is the first index of the storage that is used. */
    private final int offset;

    /** The count is the number of characters in the String. */
    private final int count;</pre>
用了一个char数组来存储字符，然后offset是偏移（这个我还搞不懂有啥用），count是String的长度。  
注意到String类是final的，不可以被继承，而且private final char value[];，只能赋值一次，赋值后就不能变了，只有从新生成一个String对象。
## public String concat(String str)

<pre escaped="true" lang="java">public String concat(String str) {
	int otherLen = str.length();
	if (otherLen == 0) {
	    return this;
	}
	char buf[] = new char[count + otherLen];
	getChars(0, count, buf, 0);
	str.getChars(0, otherLen, buf, count);
	return new String(0, count + otherLen, buf);
    }</pre>
这段代码是连接两个String的，先拿个char数组当容器，从this和str分别取出char放入buf内，注意getChars方法的第四个参数，这个是说buf从count个开始拷贝。也就是说把两个string的char放在了一个char数组内，再返回一个新的String对象。(因为之前的String已经不可以改变)
## public int indexOf(String str, int fromIndex)

<pre escaped="true" lang="java">public int indexOf(String str, int fromIndex) {
        return indexOf(value, offset, count,
                       str.value, str.offset, str.count, fromIndex);
    }
    
    //source源字符，sourceOffset源偏移，sourceCount源长度
    //target查找的字符 ...
    static int indexOf(char[] source, int sourceOffset, int sourceCount,
                       char[] target, int targetOffset, int targetCount,
                       int fromIndex) {
        //如果fromIndex比源字符还长(从0算起)，并且查找的字符长度为0，那就返回源字符的长度，否则返回-1
	if (fromIndex >= sourceCount) {
            return (targetCount == 0 ? sourceCount : -1);
	}
    	if (fromIndex &lt; 0) {
    	    fromIndex = 0;
    	}
        //如果fromIndex比源字符短，查找的字符长度为0，直接返回fromIndex
	if (targetCount == 0) {
	    return fromIndex;
	}

        //先取出第一个字符
        char first  = target[targetOffset];
        int max = sourceOffset + (sourceCount - targetCount);

        //循环每一个字符
        for (int i = sourceOffset + fromIndex; i &lt;= max; i++) {
            /* 直到找到第一个字符 */
            if (source[i] != first) {
                while (++i &lt;= max &#038;&#038; source[i] != first);
            }

            /* 找到第一个字符后，比较剩下的字符 */
            if (i &lt;= max) {
                int j = i + 1;
                int end = j + targetCount - 1;
                for (int k = targetOffset + 1; j &lt; end &#038;&#038; source[j] ==
                         target[k]; j++, k++);

                if (j == end) {
                    /* 如果j能到end，那就说明找到整个字符串啦，返回偏移 */
                    return i - sourceOffset;
                }
            }
        }
        return -1;
    }
</pre>
indexOf只要看它的查找方法，先找到第一个，然后再匹配剩下的。
## public boolean equals(Object anObject)

<pre escaped="true" lang="java">public boolean equals(Object anObject) {
	if (this == anObject) {
	    return true;
	}
	if (anObject instanceof String) {
	    String anotherString = (String)anObject;
	    int n = count;
	    if (n == anotherString.count) {
		char v1[] = value;
		char v2[] = anotherString.value;
		int i = offset;
		int j = anotherString.offset;
		while (n-- != 0) {
		    if (v1[i++] != v2[j++])
			return false;
		}
		return true;
	    }
	}
	return false;
    }</pre>
比较char~~
## replace与replaceAll

<pre escaped="true" lang="java">public String replace(CharSequence target, CharSequence replacement) {
        return Pattern.compile(target.toString(), Pattern.LITERAL).matcher(
            this).replaceAll(Matcher.quoteReplacement(replacement.toString()));
    }

    public String replaceAll(String regex, String replacement) {
	return Pattern.compile(regex).matcher(this).replaceAll(replacement);
    }</pre>
这两句真短啊。。用正则表达式来替换的。可以看出他们的区别。  
replace只支持普通字符的替换哦，Pattern.LITERAL是指启用模式的字面值解析。Matcher.quoteReplacement(str)返回指定 String 的字面值替换 String。这个方法也就是替换\\为\\\\(四个反斜杠)，$换为\\$。这样，它就不能用正则表达式了，但是看到依然是replaceAll，替换所有。  
replaceAll很简单的一个正则表达式使用~~  
要注意的是源字符串替换后内容并没有发生变化。  
举例如下: [来源][1]  
String src = new String("ab43a2c43d");  
System.out.println(src.replace("3","f"));=>ab4f2c4fd.  
System.out.println(src.replace('3','f'));=>ab4f2c4fd.  
System.out.println(src.replaceAll("\\d","f"));=>abffafcffd.  
System.out.println(src.replaceAll("a","f"));=>fb43fc23d.  
System.out.println(src.replaceFirst("\\d,"f"));=>abf32c43d  
System.out.println(src.replaceFirst("4","h"));=>abh32c43d.

 [1]: http://satellite.javaeye.com/blog/224820