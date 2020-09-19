---
title: 格式化Hive语法树(python)
author: fatkun
type: post
date: 2012-05-19T17:19:02+00:00
url: /2012/05/format-hive-astnode.html
duoshuo_thread_id:
  - 6300408858745504514
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:1581:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;">&nbsp;
    (TOK_QUERY 
        (TOK_FROM 
            (TOK_JOIN 
                (TOK_TABREF 
                    (TOK_TABNAME kv)
                 mykv)
    &nbsp;
                (TOK_TABREF 
                    (TOK_TABNAME test)
                 mytest)
    &nbsp;
                (== 
                    (. 
                        (TOK_TABLE_OR_COL mykv)
                     key)
    &nbsp;
                    (. 
                        (TOK_TABLE_OR_COL mytest)
                     id)
                )
            )
        )
    &nbsp;
        (TOK_INSERT 
            (TOK_DESTINATION 
                (TOK_DIR TOK_TMP_FILE)
            )
    &nbsp;
            (TOK_SELECT 
                (TOK_SELEXPR 
                    (TOK_TABLE_OR_COL key)
                )
            )
        )
    )</pre></td></tr></table><p class="theCode" style="display:none;">
    (TOK_QUERY 
        (TOK_FROM 
            (TOK_JOIN 
                (TOK_TABREF 
                    (TOK_TABNAME kv)
                 mykv)
             
                (TOK_TABREF 
                    (TOK_TABNAME test)
                 mytest)
             
                (== 
                    (. 
                        (TOK_TABLE_OR_COL mykv)
                     key)
                 
                    (. 
                        (TOK_TABLE_OR_COL mytest)
                     id)
                )
            )
        )
     
        (TOK_INSERT 
            (TOK_DESTINATION 
                (TOK_DIR TOK_TMP_FILE)
            )
         
            (TOK_SELECT 
                (TOK_SELEXPR 
                    (TOK_TABLE_OR_COL key)
                )
            )
        )
    )</p></div>
    ";i:2;s:5936:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #808080; font-style: italic;">#!/usr/bin/env python</span>
    <span style="color: #808080; font-style: italic;"># -*- coding: utf-8 -*-</span>
    <span style="color: #483d8b;">'''
    Created on 2012-5-20
    &nbsp;
    @author: fatkun
    '''</span>
    <span style="color: #ff7700;font-weight:bold;">import</span> <span style="color: #dc143c;">sys</span>
    &nbsp;
    <span style="color: #808080; font-style: italic;"># explain select key from kv mykv join test mytest on (mykv.key == mytest.id);</span>
    original_str <span style="color: #66cc66;">=</span> <span style="color: #483d8b;">&quot;&quot;&quot;(TOK_QUERY (TOK_FROM (TOK_JOIN (TOK_TABREF 
    (TOK_TABNAME kv) mykv) (TOK_TABREF (TOK_TABNAME test) mytest) 
    (== (. (TOK_TABLE_OR_COL mykv) key) (. (TOK_TABLE_OR_COL mytest) id)))) 
    (TOK_INSERT (TOK_DESTINATION (TOK_DIR TOK_TMP_FILE)) (TOK_SELECT (TOK_SELEXPR (TOK_TABLE_OR_COL key)))))&quot;&quot;&quot;</span>
    &nbsp;
    tmp_str <span style="color: #66cc66;">=</span> original_str.<span style="color: black;">strip</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>.<span style="color: black;">replace</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">'<span style="color: #000099; font-weight: bold;">\n</span>'</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">''</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> my_print<span style="color: black;">&#40;</span>mystr<span style="color: black;">&#41;</span>:
        <span style="color: #dc143c;">sys</span>.<span style="color: black;">stdout</span>.<span style="color: black;">write</span><span style="color: black;">&#40;</span>mystr<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> print_indent<span style="color: black;">&#40;</span>indent_level<span style="color: black;">&#41;</span>:
        <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">range</span><span style="color: black;">&#40;</span>indent_level<span style="color: black;">&#41;</span>:
            my_print<span style="color: black;">&#40;</span><span style="color: #483d8b;">' '</span> * <span style="color: #ff4500;">4</span><span style="color: black;">&#41;</span>
    &nbsp;
    &nbsp;
    indent_level <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> char <span style="color: #ff7700;font-weight:bold;">in</span> tmp_str:
        <span style="color: #ff7700;font-weight:bold;">if</span> char <span style="color: #66cc66;">==</span> <span style="color: #483d8b;">'('</span>:
            <span style="color: #808080; font-style: italic;"># 如果是左括号,先换行,然后打印缩进+(</span>
            my_print<span style="color: black;">&#40;</span><span style="color: #483d8b;">'<span style="color: #000099; font-weight: bold;">\n</span>'</span><span style="color: black;">&#41;</span>
            print_indent<span style="color: black;">&#40;</span>indent_level<span style="color: black;">&#41;</span>
            my_print<span style="color: black;">&#40;</span>char<span style="color: black;">&#41;</span>
            indent_level +<span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
        <span style="color: #ff7700;font-weight:bold;">elif</span> char <span style="color: #66cc66;">==</span> <span style="color: #483d8b;">')'</span>:
            <span style="color: #808080; font-style: italic;"># 如果是右括号,先打印),再换行,打印下一级别的缩进</span>
            indent_level -<span style="color: #66cc66;">=</span> <span style="color: #ff4500;">1</span>
            my_print<span style="color: black;">&#40;</span>char<span style="color: black;">&#41;</span>
            my_print<span style="color: black;">&#40;</span><span style="color: #483d8b;">'<span style="color: #000099; font-weight: bold;">\n</span>'</span><span style="color: black;">&#41;</span>
            print_indent<span style="color: black;">&#40;</span>indent_level - <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>
        <span style="color: #ff7700;font-weight:bold;">else</span>:
            <span style="color: #808080; font-style: italic;"># 其他的直接打印出来</span>
            my_print<span style="color: black;">&#40;</span>char<span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">#!/usr/bin/env python
    # -*- coding: utf-8 -*-
    '''
    Created on 2012-5-20
    
    @author: fatkun
    '''
    import sys
    
    # explain select key from kv mykv join test mytest on (mykv.key == mytest.id);
    original_str = &quot;&quot;&quot;(TOK_QUERY (TOK_FROM (TOK_JOIN (TOK_TABREF 
    (TOK_TABNAME kv) mykv) (TOK_TABREF (TOK_TABNAME test) mytest) 
    (== (. (TOK_TABLE_OR_COL mykv) key) (. (TOK_TABLE_OR_COL mytest) id)))) 
    (TOK_INSERT (TOK_DESTINATION (TOK_DIR TOK_TMP_FILE)) (TOK_SELECT (TOK_SELEXPR (TOK_TABLE_OR_COL key)))))&quot;&quot;&quot;
    
    tmp_str = original_str.strip().replace('\n', '')
    
    def my_print(mystr):
        sys.stdout.write(mystr)
    
    def print_indent(indent_level):
        for i in range(indent_level):
            my_print(' ' * 4)
    
    
    indent_level = 0
    for char in tmp_str:
        if char == '(':
            # 如果是左括号,先换行,然后打印缩进+(
            my_print('\n')
            print_indent(indent_level)
            my_print(char)
            indent_level += 1
        elif char == ')':
            # 如果是右括号,先打印),再换行,打印下一级别的缩进
            indent_level -= 1
            my_print(char)
            my_print('\n')
            print_indent(indent_level - 1)
        else:
            # 其他的直接打印出来
            my_print(char)</p></div>
    ";}
categories:
  - hive
tags:
  - hadoop
  - hive

---
为了容易看一点，把用explain得到的语法树加上一些缩进.
该代码只是简单的加上缩进.
## 效果

这是查询explain select key from kv mykv join test mytest on (mykv.key == mytest.id);语句获取的语法树
<pre escaped="true" lang="xml">(TOK_QUERY 
    (TOK_FROM 
        (TOK_JOIN 
            (TOK_TABREF 
                (TOK_TABNAME kv)
             mykv)
         
            (TOK_TABREF 
                (TOK_TABNAME test)
             mytest)
         
            (== 
                (. 
                    (TOK_TABLE_OR_COL mykv)
                 key)
             
                (. 
                    (TOK_TABLE_OR_COL mytest)
                 id)
            )
        )
    )
 
    (TOK_INSERT 
        (TOK_DESTINATION 
            (TOK_DIR TOK_TMP_FILE)
        )
     
        (TOK_SELECT 
            (TOK_SELEXPR 
                (TOK_TABLE_OR_COL key)
            )
        )
    )
)
</pre>
## 代码如下

<pre escaped="true" lang="python">#!/usr/bin/env python
# -*- coding: utf-8 -*-
'''
Created on 2012-5-20

@author: fatkun
'''
import sys

# explain select key from kv mykv join test mytest on (mykv.key == mytest.id);
original_str = """(TOK_QUERY (TOK_FROM (TOK_JOIN (TOK_TABREF 
(TOK_TABNAME kv) mykv) (TOK_TABREF (TOK_TABNAME test) mytest) 
(== (. (TOK_TABLE_OR_COL mykv) key) (. (TOK_TABLE_OR_COL mytest) id)))) 
(TOK_INSERT (TOK_DESTINATION (TOK_DIR TOK_TMP_FILE)) (TOK_SELECT (TOK_SELEXPR (TOK_TABLE_OR_COL key)))))"""

tmp_str = original_str.strip().replace('\n', '')

def my_print(mystr):
    sys.stdout.write(mystr)

def print_indent(indent_level):
    for i in range(indent_level):
        my_print(' ' * 4)


indent_level = 0
for char in tmp_str:
    if char == '(':
        # 如果是左括号,先换行,然后打印缩进+(
        my_print('\n')
        print_indent(indent_level)
        my_print(char)
        indent_level += 1
    elif char == ')':
        # 如果是右括号,先打印),再换行,打印下一级别的缩进
        indent_level -= 1
        my_print(char)
        my_print('\n')
        print_indent(indent_level - 1)
    else:
        # 其他的直接打印出来
        my_print(char)
        
</pre>