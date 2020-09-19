---
title: python实现一个简单的地址簿
author: fatkun
type: post
date: 2011-04-17T10:51:16+00:00
url: /2011/04/python-addressbook.html
duoshuo_thread_id:
  - 6300408803653321473
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:5083:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #808080; font-style: italic;">#!/usr/bin/python</span>
    <span style="color: #808080; font-style: italic;"># Filename: addressBook.py</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">import</span> <span style="color: #dc143c;">cPickle</span> <span style="color: #ff7700;font-weight:bold;">as</span> <span style="color: #dc143c;">pickle</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">class</span> PersonInfo:
        <span style="color: #ff7700;font-weight:bold;">def</span> <span style="color: #0000cd;">__init__</span><span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: #66cc66;">,</span> name<span style="color: #66cc66;">,</span> age<span style="color: black;">&#41;</span>:
            <span style="color: #008000;">self</span>.<span style="color: black;">name</span> <span style="color: #66cc66;">=</span> name
            <span style="color: #008000;">self</span>.<span style="color: black;">age</span> <span style="color: #66cc66;">=</span> age
        <span style="color: #ff7700;font-weight:bold;">def</span> <span style="color: #0000cd;">__str__</span><span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: black;">&#41;</span>:
            <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: #483d8b;">'姓名:%s，年龄:%s'</span> % <span style="color: black;">&#40;</span><span style="color: #008000;">self</span>.<span style="color: black;">name</span><span style="color: #66cc66;">,</span> <span style="color: #008000;">self</span>.<span style="color: black;">age</span><span style="color: black;">&#41;</span>
    &nbsp;
    &nbsp;
    addrFileName <span style="color: #66cc66;">=</span> <span style="color: #483d8b;">'address.data'</span>
    addrList <span style="color: #66cc66;">=</span> <span style="color: black;">&#123;</span><span style="color: black;">&#125;</span>
    pi <span style="color: #66cc66;">=</span> PersonInfo<span style="color: black;">&#40;</span><span style="color: #483d8b;">'Fatkun'</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">23</span><span style="color: black;">&#41;</span>
    addrList<span style="color: black;">&#91;</span>pi.<span style="color: black;">name</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> pi
    pi <span style="color: #66cc66;">=</span> PersonInfo<span style="color: black;">&#40;</span><span style="color: #483d8b;">'Olunx'</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">22</span><span style="color: black;">&#41;</span>
    addrList<span style="color: black;">&#91;</span>pi.<span style="color: black;">name</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> pi
    addrFile <span style="color: #66cc66;">=</span> <span style="color: #008000;">file</span><span style="color: black;">&#40;</span>addrFileName<span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'w'</span><span style="color: black;">&#41;</span>
    <span style="color: #dc143c;">pickle</span>.<span style="color: black;">dump</span><span style="color: black;">&#40;</span>addrList<span style="color: #66cc66;">,</span> addrFile<span style="color: black;">&#41;</span>
    addrFile.<span style="color: black;">close</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">del</span> pi
    &nbsp;
    addrFile <span style="color: #66cc66;">=</span> <span style="color: #008000;">file</span><span style="color: black;">&#40;</span>addrFileName<span style="color: black;">&#41;</span>
    storedPi <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">pickle</span>.<span style="color: black;">load</span><span style="color: black;">&#40;</span>addrFile<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">for</span> key<span style="color: #66cc66;">,</span> pi <span style="color: #ff7700;font-weight:bold;">in</span> storedPi.<span style="color: black;">items</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>:
        <span style="color: #ff7700;font-weight:bold;">print</span> pi</pre></td></tr></table><p class="theCode" style="display:none;">#!/usr/bin/python
    # Filename: addressBook.py
    
    import cPickle as pickle
    
    class PersonInfo:
        def __init__(self, name, age):
            self.name = name
            self.age = age
        def __str__(self):
            return '姓名:%s，年龄:%s' % (self.name, self.age)
        
    
    addrFileName = 'address.data'
    addrList = {}
    pi = PersonInfo('Fatkun', 23)
    addrList[pi.name] = pi
    pi = PersonInfo('Olunx', 22)
    addrList[pi.name] = pi
    addrFile = file(addrFileName, 'w')
    pickle.dump(addrList, addrFile)
    addrFile.close()
    
    del pi
    
    addrFile = file(addrFileName)
    storedPi = pickle.load(addrFile)
    
    for key, pi in storedPi.items():
        print pi</p></div>
    ";i:2;s:14930:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #808080; font-style: italic;">#!/usr/bin/python</span>
    <span style="color: #808080; font-style: italic;"># -*- coding: gbk -*-</span>
    <span style="color: #808080; font-style: italic;"># Filename: addressBook.py</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">import</span> <span style="color: #dc143c;">cPickle</span> <span style="color: #ff7700;font-weight:bold;">as</span> <span style="color: #dc143c;">pickle</span>
    <span style="color: #ff7700;font-weight:bold;">import</span> <span style="color: #dc143c;">sys</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">class</span> PersonInfo:
        <span style="color: #ff7700;font-weight:bold;">def</span> <span style="color: #0000cd;">__init__</span><span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: #66cc66;">,</span> name<span style="color: #66cc66;">,</span> age<span style="color: black;">&#41;</span>:
            <span style="color: #008000;">self</span>.<span style="color: black;">name</span> <span style="color: #66cc66;">=</span> name
            <span style="color: #008000;">self</span>.<span style="color: black;">age</span> <span style="color: #66cc66;">=</span> age
        <span style="color: #ff7700;font-weight:bold;">def</span> <span style="color: #0000cd;">__str__</span><span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: black;">&#41;</span>:
            <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: #483d8b;">'姓名:%s，年龄:%s'</span> % <span style="color: black;">&#40;</span><span style="color: #008000;">self</span>.<span style="color: black;">name</span><span style="color: #66cc66;">,</span> <span style="color: #008000;">self</span>.<span style="color: black;">age</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #808080; font-style: italic;">#读取文件</span>
    <span style="color: #ff7700;font-weight:bold;">def</span> readObj<span style="color: black;">&#40;</span>addrFileName<span style="color: black;">&#41;</span>:
        addrFile <span style="color: #66cc66;">=</span> <span style="color: #008000;">file</span><span style="color: black;">&#40;</span>addrFileName<span style="color: black;">&#41;</span>
        storedList <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">pickle</span>.<span style="color: black;">load</span><span style="color: black;">&#40;</span>addrFile<span style="color: black;">&#41;</span>
        <span style="color: #ff7700;font-weight:bold;">return</span> storedList
    &nbsp;
    <span style="color: #808080; font-style: italic;">#添加或更新</span>
    <span style="color: #ff7700;font-weight:bold;">def</span> addOrUpdatePerson<span style="color: black;">&#40;</span>name<span style="color: #66cc66;">,</span> age<span style="color: black;">&#41;</span>:
        <span style="color: #ff7700;font-weight:bold;">global</span> addrList
        pi <span style="color: #66cc66;">=</span> PersonInfo<span style="color: black;">&#40;</span>name<span style="color: #66cc66;">,</span> age<span style="color: black;">&#41;</span>
        addrList<span style="color: black;">&#91;</span>name<span style="color: black;">&#93;</span> <span style="color: #66cc66;">=</span> pi
    &nbsp;
    <span style="color: #808080; font-style: italic;">#保存对象到文件</span>
    <span style="color: #ff7700;font-weight:bold;">def</span> save<span style="color: black;">&#40;</span>addrFileName<span style="color: black;">&#41;</span>:
        <span style="color: #ff7700;font-weight:bold;">global</span> addrList
        addrFile <span style="color: #66cc66;">=</span> <span style="color: #008000;">file</span><span style="color: black;">&#40;</span>addrFileName<span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'w'</span><span style="color: black;">&#41;</span>
        <span style="color: #dc143c;">pickle</span>.<span style="color: black;">dump</span><span style="color: black;">&#40;</span>addrList<span style="color: #66cc66;">,</span> addrFile<span style="color: black;">&#41;</span>
        addrFile.<span style="color: black;">close</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">def</span> delPersion<span style="color: black;">&#40;</span>name<span style="color: black;">&#41;</span>:
        <span style="color: #ff7700;font-weight:bold;">global</span> addrList
        <span style="color: #808080; font-style: italic;">#if addrList.has_key(name): 可以用这个判断是否有key，但我想练习一下捕捉异常，so...</span>
        <span style="color: #ff7700;font-weight:bold;">try</span>:
            <span style="color: #ff7700;font-weight:bold;">del</span> addrList<span style="color: black;">&#91;</span>name<span style="color: black;">&#93;</span>
        <span style="color: #ff7700;font-weight:bold;">except</span> <span style="color: #008000;">KeyError</span>:
            <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">&quot;出错啦，可能已经删除了。<span style="color: #000099; font-weight: bold;">\n</span>&quot;</span>
    <span style="color: #808080; font-style: italic;">#遍历</span>
    <span style="color: #ff7700;font-weight:bold;">def</span> printAll<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>:
        <span style="color: #ff7700;font-weight:bold;">global</span> addrList
        <span style="color: #ff7700;font-weight:bold;">for</span> key<span style="color: #66cc66;">,</span> pi <span style="color: #ff7700;font-weight:bold;">in</span> addrList.<span style="color: black;">items</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>:
            <span style="color: #ff7700;font-weight:bold;">print</span> pi
    &nbsp;
    <span style="color: #808080; font-style: italic;">#保存对象的文件名</span>
    addrFileName <span style="color: #66cc66;">=</span> <span style="color: #483d8b;">'address.data'</span>
    <span style="color: #808080; font-style: italic;">#map</span>
    addrList <span style="color: #66cc66;">=</span> readObj<span style="color: black;">&#40;</span>addrFileName<span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span><span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#41;</span> <span style="color: #66cc66;">&lt;</span> <span style="color: #ff4500;">2</span>:
        printAll<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">elif</span> <span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>.<span style="color: black;">startswith</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">'--'</span><span style="color: black;">&#41;</span>:
        option <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">2</span>:<span style="color: black;">&#93;</span>
        <span style="color: #ff7700;font-weight:bold;">if</span> option <span style="color: #66cc66;">==</span> <span style="color: #483d8b;">'version'</span>:
            <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">'Version 1.0'</span>
        <span style="color: #ff7700;font-weight:bold;">elif</span> option <span style="color: #66cc66;">==</span> <span style="color: #483d8b;">'help'</span>:
            <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">'''<span style="color: #000099; font-weight: bold;">\</span>
    这只是一个简单的地址簿（坑爹啊，哪里有地址了，就一个名字和年龄）
    参数：
        --version : 打印版本
        --help : 显示帮助
        -a username age ：添加
        -u username age ：更新
        -d username : 删除
        '''</span>
        <span style="color: #ff7700;font-weight:bold;">else</span>:
            <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">'未知参数'</span>
    <span style="color: #ff7700;font-weight:bold;">elif</span> <span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>.<span style="color: black;">startswith</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">'-'</span><span style="color: black;">&#41;</span>:
        option <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span>:<span style="color: black;">&#93;</span>
        <span style="color: #ff7700;font-weight:bold;">if</span> option <span style="color: #66cc66;">==</span> <span style="color: #483d8b;">'a'</span>:<span style="color: #808080; font-style: italic;">#添加</span>
            <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span><span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#41;</span> <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">4</span>:
                addOrUpdatePerson<span style="color: black;">&#40;</span><span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span><span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">3</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
        <span style="color: #ff7700;font-weight:bold;">elif</span> option <span style="color: #66cc66;">==</span> <span style="color: #483d8b;">'u'</span>:<span style="color: #808080; font-style: italic;">#更新</span>
            <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span><span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#41;</span> <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">4</span>:
                addOrUpdatePerson<span style="color: black;">&#40;</span><span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span><span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">3</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
        <span style="color: #ff7700;font-weight:bold;">elif</span> option <span style="color: #66cc66;">==</span> <span style="color: #483d8b;">'d'</span>:<span style="color: #808080; font-style: italic;">#删除</span>
            <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #008000;">len</span><span style="color: black;">&#40;</span><span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#41;</span> <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">3</span>:
                delPersion<span style="color: black;">&#40;</span><span style="color: #dc143c;">sys</span>.<span style="color: black;">argv</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
        printAll<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
        save<span style="color: black;">&#40;</span>addrFileName<span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">#!/usr/bin/python
    # -*- coding: gbk -*-
    # Filename: addressBook.py
    
    import cPickle as pickle
    import sys
    
    class PersonInfo:
        def __init__(self, name, age):
            self.name = name
            self.age = age
        def __str__(self):
            return '姓名:%s，年龄:%s' % (self.name, self.age)
    
    #读取文件
    def readObj(addrFileName):
        addrFile = file(addrFileName)
        storedList = pickle.load(addrFile)
        return storedList
    
    #添加或更新
    def addOrUpdatePerson(name, age):
        global addrList
        pi = PersonInfo(name, age)
        addrList[name] = pi
    
    #保存对象到文件
    def save(addrFileName):
        global addrList
        addrFile = file(addrFileName, 'w')
        pickle.dump(addrList, addrFile)
        addrFile.close()
    def delPersion(name):
        global addrList
        #if addrList.has_key(name): 可以用这个判断是否有key，但我想练习一下捕捉异常，so...
        try:
            del addrList[name]
        except KeyError:
            print &quot;出错啦，可能已经删除了。\n&quot;
    #遍历
    def printAll():
        global addrList
        for key, pi in addrList.items():
            print pi
    
    #保存对象的文件名
    addrFileName = 'address.data'
    #map
    addrList = readObj(addrFileName)
    
    if len(sys.argv) &lt; 2:
        printAll()
    elif sys.argv[1].startswith('--'):
        option = sys.argv[1][2:]
        if option == 'version':
            print 'Version 1.0'
        elif option == 'help':
            print '''\
    这只是一个简单的地址簿（坑爹啊，哪里有地址了，就一个名字和年龄）
    参数：
        --version : 打印版本
        --help : 显示帮助
        -a username age ：添加
        -u username age ：更新
        -d username : 删除
        '''
        else:
            print '未知参数'
    elif sys.argv[1].startswith('-'):
        option = sys.argv[1][1:]
        if option == 'a':#添加
            if len(sys.argv) == 4:
                addOrUpdatePerson(sys.argv[2],sys.argv[3])
        elif option == 'u':#更新
            if len(sys.argv) == 4:
                addOrUpdatePerson(sys.argv[2],sys.argv[3])
        elif option == 'd':#删除
            if len(sys.argv) == 3:
                delPersion(sys.argv[2])
        printAll()
        save(addrFileName)</p></div>
    ";}
categories:
  - python
tags:
  - python
  - 地址簿

---
看了简明python教程，动手试试，用python实现一个简单的地址簿  
<!--more-->

## 版本一

这只是一个简单的试验版本，如何新建对象并保存。
<pre escaped="true" lang="python">#!/usr/bin/python
# Filename: addressBook.py

import cPickle as pickle

class PersonInfo:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    def __str__(self):
        return '姓名:%s，年龄:%s' % (self.name, self.age)
    

addrFileName = 'address.data'
addrList = {}
pi = PersonInfo('Fatkun', 23)
addrList[pi.name] = pi
pi = PersonInfo('Olunx', 22)
addrList[pi.name] = pi
addrFile = file(addrFileName, 'w')
pickle.dump(addrList, addrFile)
addrFile.close()

del pi

addrFile = file(addrFileName)
storedPi = pickle.load(addrFile)

for key, pi in storedPi.items():
    print pi
</pre>
## 版本2

这个版本是较完整的例子，实现了多个方法。
<pre escaped="true" lang="python">#!/usr/bin/python
# -*- coding: gbk -*-
# Filename: addressBook.py

import cPickle as pickle
import sys

class PersonInfo:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    def __str__(self):
        return '姓名:%s，年龄:%s' % (self.name, self.age)

#读取文件
def readObj(addrFileName):
    addrFile = file(addrFileName)
    storedList = pickle.load(addrFile)
    return storedList

#添加或更新
def addOrUpdatePerson(name, age):
    global addrList
    pi = PersonInfo(name, age)
    addrList[name] = pi

#保存对象到文件
def save(addrFileName):
    global addrList
    addrFile = file(addrFileName, 'w')
    pickle.dump(addrList, addrFile)
    addrFile.close()
def delPersion(name):
    global addrList
    #if addrList.has_key(name): 可以用这个判断是否有key，但我想练习一下捕捉异常，so...
    try:
        del addrList[name]
    except KeyError:
        print "出错啦，可能已经删除了。\n"
#遍历
def printAll():
    global addrList
    for key, pi in addrList.items():
        print pi

#保存对象的文件名
addrFileName = 'address.data'
#map
addrList = readObj(addrFileName)

if len(sys.argv) &lt; 2:
    printAll()
elif sys.argv[1].startswith('--'):
    option = sys.argv[1][2:]
    if option == 'version':
        print 'Version 1.0'
    elif option == 'help':
        print '''\
这只是一个简单的地址簿（坑爹啊，哪里有地址了，就一个名字和年龄）
参数：
    --version : 打印版本
    --help : 显示帮助
    -a username age ：添加
    -u username age ：更新
    -d username : 删除
    '''
    else:
        print '未知参数'
elif sys.argv[1].startswith('-'):
    option = sys.argv[1][1:]
    if option == 'a':#添加
        if len(sys.argv) == 4:
            addOrUpdatePerson(sys.argv[2],sys.argv[3])
    elif option == 'u':#更新
        if len(sys.argv) == 4:
            addOrUpdatePerson(sys.argv[2],sys.argv[3])
    elif option == 'd':#删除
        if len(sys.argv) == 3:
            delPersion(sys.argv[2])
    printAll()
    save(addrFileName)
</pre>