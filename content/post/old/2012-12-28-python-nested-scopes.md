---
title: python嵌套作用域问题
author: fatkun
type: post
date: 2012-12-27T16:28:02+00:00
url: /2012/12/python-nested-scopes.html
duoshuo_thread_id:
  - 6300409441762149122
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:1152:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;">i <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">6</span>
    <span style="color: #ff7700;font-weight:bold;">def</span> f<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>:
        <span style="color: #ff7700;font-weight:bold;">def</span> g<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>:
            <span style="color: #ff7700;font-weight:bold;">print</span> i <span style="color: #808080; font-style: italic;"># 返回10</span>
        i <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">10</span> <span style="color: #808080; font-style: italic;"># 会绑定在f函数上</span>
        g<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    f<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">i = 6
    def f():
        def g():
            print i # 返回10
        i = 10 # 会绑定在f函数上
        g()
    f()</p></div>
    ";i:2;s:1181:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;">i <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">6</span>
    <span style="color: #ff7700;font-weight:bold;">def</span> f<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>:
        <span style="color: #ff7700;font-weight:bold;">def</span> g<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>:
            <span style="color: #ff7700;font-weight:bold;">print</span> i <span style="color: #808080; font-style: italic;"># NameError: free variable 'i' referenced before assignment in enclosing scope</span>
        g<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
        i <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">10</span>
    f<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">i = 6
    def f():
        def g():
            print i # NameError: free variable 'i' referenced before assignment in enclosing scope
        g()
        i = 10
    f()</p></div>
    ";}
categories:
  - python
tags:
  - python
  - 作用域
  - 嵌套作用域

---
之前都不太理解这个。。。
> 在Python中，使用一个变量之前不必预先声明它，但是在真正使用它之前，它必须已经绑定到某个对象；而名字绑定将在当前作用域中引入新的变量，同时屏蔽外层作用域中的同名变量，不论这个名字绑定发生在当前作用域中的哪个位置。
&nbsp;
## 代码一

<pre lang="python">i = 6
def f():
    def g():
        print i # 返回10
    i = 10 # 会绑定在f函数上
    g()
f()
</pre>
在f函数里，i有个赋值操作，所以全局变量i=6被屏蔽掉了。i绑定后，执行g函数，g函数会有f函数的作用域（？？），打印的i值=10
## 代码二

<pre lang="python">i = 6
def f():
    def g():
        print i # NameError: free variable 'i' referenced before assignment in enclosing scope
    g()
    i = 10
f()
</pre>
把位置换了一下,i赋值在g函数的后面。print的时候就抛异常NameError了。  
由于f函数中有一个同名的i参数赋值，会把外层的全局变量i给屏蔽掉（不管这个赋值在f函数的什么地方，都会先屏蔽掉上层的同名变量），但由于还没有绑定值就先执行g函数了，所以抛出异常。
## 参考

<http://www.cnblogs.com/frydsh/archive/2012/08/12/2602100.html>  
<http://www.python.org/dev/peps/pep-0227/>