---
title: Python list的多列排序
author: fatkun
type: post
date: 2011-05-09T15:02:55+00:00
url: /2011/05/python-list-sort.html
duoshuo_thread_id:
  - 6300408813845480193
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:5726:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #808080; font-style: italic;">#默认顺序</span>
    <span style="color: #66cc66;">&gt;&gt;&gt;</span> l
    <span style="color: black;">&#91;</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">'aa'</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'2'</span><span style="color: black;">&#41;</span><span style="color: #66cc66;">,</span> <span style="color: black;">&#40;</span><span style="color: #483d8b;">'aa'</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'1'</span><span style="color: black;">&#41;</span><span style="color: #66cc66;">,</span> <span style="color: black;">&#40;</span><span style="color: #483d8b;">'bb'</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'1'</span><span style="color: black;">&#41;</span><span style="color: #66cc66;">,</span> <span style="color: black;">&#40;</span><span style="color: #483d8b;">'dd'</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'3'</span><span style="color: black;">&#41;</span><span style="color: #66cc66;">,</span> <span style="color: black;">&#40;</span><span style="color: #483d8b;">'cc'</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'4'</span><span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    &nbsp;
    <span style="color: #808080; font-style: italic;">#普通排序，默认会按顺序进行排序</span>
    <span style="color: #66cc66;">&gt;&gt;&gt;</span> <span style="color: #008000;">sorted</span><span style="color: black;">&#40;</span>l<span style="color: black;">&#41;</span>
    <span style="color: black;">&#91;</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">'aa'</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'1'</span><span style="color: black;">&#41;</span><span style="color: #66cc66;">,</span> <span style="color: black;">&#40;</span><span style="color: #483d8b;">'aa'</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'2'</span><span style="color: black;">&#41;</span><span style="color: #66cc66;">,</span> <span style="color: black;">&#40;</span><span style="color: #483d8b;">'bb'</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'1'</span><span style="color: black;">&#41;</span><span style="color: #66cc66;">,</span> <span style="color: black;">&#40;</span><span style="color: #483d8b;">'cc'</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'4'</span><span style="color: black;">&#41;</span><span style="color: #66cc66;">,</span> <span style="color: black;">&#40;</span><span style="color: #483d8b;">'dd'</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'3'</span><span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
    &nbsp;
    <span style="color: #808080; font-style: italic;">#指定排序的优先级，在这里你可以看到多列排序只需要用逗号隔开即可</span>
    <span style="color: #66cc66;">&gt;&gt;&gt;</span> <span style="color: #ff7700;font-weight:bold;">from</span> <span style="color: #dc143c;">operator</span> <span style="color: #ff7700;font-weight:bold;">import</span> itemgetter<span style="color: #66cc66;">,</span> attrgetter
    <span style="color: #66cc66;">&gt;&gt;&gt;</span> <span style="color: #008000;">sorted</span><span style="color: black;">&#40;</span>l<span style="color: #66cc66;">,</span> key<span style="color: #66cc66;">=</span>itemgetter<span style="color: black;">&#40;</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    <span style="color: black;">&#91;</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">'aa'</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'1'</span><span style="color: black;">&#41;</span><span style="color: #66cc66;">,</span> <span style="color: black;">&#40;</span><span style="color: #483d8b;">'bb'</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'1'</span><span style="color: black;">&#41;</span><span style="color: #66cc66;">,</span> <span style="color: black;">&#40;</span><span style="color: #483d8b;">'aa'</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'2'</span><span style="color: black;">&#41;</span><span style="color: #66cc66;">,</span> <span style="color: black;">&#40;</span><span style="color: #483d8b;">'dd'</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'3'</span><span style="color: black;">&#41;</span><span style="color: #66cc66;">,</span> <span style="color: black;">&#40;</span><span style="color: #483d8b;">'cc'</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'4'</span><span style="color: black;">&#41;</span><span style="color: black;">&#93;</span></pre></td></tr></table><p class="theCode" style="display:none;">#默认顺序
    &gt;&gt;&gt; l
    [('aa', '2'), ('aa', '1'), ('bb', '1'), ('dd', '3'), ('cc', '4')]
    
    #普通排序，默认会按顺序进行排序
    &gt;&gt;&gt; sorted(l)
    [('aa', '1'), ('aa', '2'), ('bb', '1'), ('cc', '4'), ('dd', '3')]
    
    #指定排序的优先级，在这里你可以看到多列排序只需要用逗号隔开即可
    &gt;&gt;&gt; from operator import itemgetter, attrgetter
    &gt;&gt;&gt; sorted(l, key=itemgetter(1, 0))
    [('aa', '1'), ('bb', '1'), ('aa', '2'), ('dd', '3'), ('cc', '4')]</p></div>
    ";i:2;s:2279:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #66cc66;">&gt;&gt;&gt;</span> l <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: black;">&#123;</span><span style="color: #483d8b;">'a'</span>:<span style="color: #483d8b;">'fatkun'</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'b'</span>:<span style="color: #ff4500;">23</span><span style="color: black;">&#125;</span><span style="color: #66cc66;">,</span> <span style="color: black;">&#123;</span><span style="color: #483d8b;">'a'</span>:<span style="color: #483d8b;">'ken'</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'b'</span>:<span style="color: #ff4500;">21</span><span style="color: black;">&#125;</span><span style="color: black;">&#93;</span>
    <span style="color: #66cc66;">&gt;&gt;&gt;</span> <span style="color: #008000;">sorted</span><span style="color: black;">&#40;</span>l<span style="color: #66cc66;">,</span> key<span style="color: #66cc66;">=</span><span style="color: #ff7700;font-weight:bold;">lambda</span> x:x<span style="color: black;">&#91;</span><span style="color: #483d8b;">'b'</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
    <span style="color: black;">&#91;</span><span style="color: black;">&#123;</span><span style="color: #483d8b;">'a'</span>: <span style="color: #483d8b;">'ken'</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'b'</span>: <span style="color: #ff4500;">21</span><span style="color: black;">&#125;</span><span style="color: #66cc66;">,</span> <span style="color: black;">&#123;</span><span style="color: #483d8b;">'a'</span>: <span style="color: #483d8b;">'fatkun'</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'b'</span>: <span style="color: #ff4500;">23</span><span style="color: black;">&#125;</span><span style="color: black;">&#93;</span></pre></td></tr></table><p class="theCode" style="display:none;">&gt;&gt;&gt; l = [{'a':'fatkun', 'b':23}, {'a':'ken', 'b':21}]
    &gt;&gt;&gt; sorted(l, key=lambda x:x['b'])
    [{'a': 'ken', 'b': 21}, {'a': 'fatkun', 'b': 23}]</p></div>
    ";}
categories:
  - python
tags:
  - python
  - sorted
  - 多列排序
  - 排序

---
Python 中的排序真的很方便  
你可以使用alist.sort()或者sorted(alist)进行排序。不同的是，前者会改变原来list的顺序。  
在python中你可以简单的指定key则可以按照某一列排序
<pre escaped="true" lang="python">#默认顺序
&gt;&gt;&gt; l
[('aa', '2'), ('aa', '1'), ('bb', '1'), ('dd', '3'), ('cc', '4')]

#普通排序，默认会按顺序进行排序
&gt;&gt;&gt; sorted(l)
[('aa', '1'), ('aa', '2'), ('bb', '1'), ('cc', '4'), ('dd', '3')]

#指定排序的优先级，在这里你可以看到多列排序只需要用逗号隔开即可
&gt;&gt;&gt; from operator import itemgetter, attrgetter
&gt;&gt;&gt; sorted(l, key=itemgetter(1, 0))
[('aa', '1'), ('bb', '1'), ('aa', '2'), ('dd', '3'), ('cc', '4')]

</pre>
对List里的dict排序，key=lambda x:x[&#8216;b&#8217;]。b为你想排序的列
<pre escaped="true" lang="python">&gt;&gt;&gt; l = [{'a':'fatkun', 'b':23}, {'a':'ken', 'b':21}]
&gt;&gt;&gt; sorted(l, key=lambda x:x['b'])
[{'a': 'ken', 'b': 21}, {'a': 'fatkun', 'b': 23}]</pre>
这样的排序方法实在是太简单了~~另外如果需要更复杂的方法，可以使用cmp参数，自己写一个方法比较。
参考文章：  
<http://wiki.python.org/moin/HowTo/Sorting/>