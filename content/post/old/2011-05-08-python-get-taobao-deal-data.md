---
title: Python遍历淘宝成交记录
author: fatkun
type: post
date: 2011-05-08T13:19:21+00:00
url: /2011/05/python-get-taobao-deal-data.html
duoshuo_thread_id:
  - 6300408813790954242
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:15526:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #808080; font-style: italic;">#-*- encoding: gbk -*-</span>
    <span style="color: #483d8b;">'''
    Created on 2011-5-8
    &nbsp;
    @author: fatkun
    '''</span>
    <span style="color: #ff7700;font-weight:bold;">import</span> <span style="color: #dc143c;">urllib2</span>
    <span style="color: #ff7700;font-weight:bold;">import</span> <span style="color: #dc143c;">re</span>
    <span style="color: #ff7700;font-weight:bold;">import</span> <span style="color: #dc143c;">time</span>
    <span style="color: #ff7700;font-weight:bold;">import</span> <span style="color: #dc143c;">string</span>
    &nbsp;
    <span style="color: #808080; font-style: italic;">#读取网页</span>
    <span style="color: #ff7700;font-weight:bold;">def</span> read<span style="color: black;">&#40;</span>url<span style="color: black;">&#41;</span>:
        opener <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">urllib2</span>.<span style="color: black;">build_opener</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
        <span style="color: #808080; font-style: italic;">#opener.handle_open[&quot;http&quot;][0].set_http_debuglevel(1)</span>
        opener.<span style="color: black;">addheaders</span> <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">'User-agent'</span><span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'Mozilla/5.0'</span><span style="color: black;">&#41;</span><span style="color: black;">&#93;</span>
        f<span style="color: #66cc66;">=</span> opener.<span style="color: #008000;">open</span><span style="color: black;">&#40;</span>url<span style="color: black;">&#41;</span>
        content <span style="color: #66cc66;">=</span> f.<span style="color: black;">read</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
        <span style="color: #ff7700;font-weight:bold;">return</span> content
    &nbsp;
    <span style="color: #808080; font-style: italic;">#正则表达式返回需要的内容</span>
    <span style="color: #ff7700;font-weight:bold;">def</span> display<span style="color: black;">&#40;</span>content<span style="color: black;">&#41;</span>:
        pattern <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">re</span>.<span style="color: #008000;">compile</span><span style="color: black;">&#40;</span>r<span style="color: #483d8b;">&quot;&quot;&quot;&lt;tr(?:[^&gt;]+)?&gt; #TR
                            [<span style="color: #000099; font-weight: bold;">\S</span><span style="color: #000099; font-weight: bold;">\s</span>]*?&lt;td[<span style="color: #000099; font-weight: bold;">\S</span><span style="color: #000099; font-weight: bold;">\s</span>]*?&lt;/td&gt;[<span style="color: #000099; font-weight: bold;">\S</span><span style="color: #000099; font-weight: bold;">\s</span>]*?&lt;td(?:[^&gt;]+)?&gt; #Second TD
                            [<span style="color: #000099; font-weight: bold;">\S</span><span style="color: #000099; font-weight: bold;">\s</span>]*?&lt;a [^&gt;]+&gt;([<span style="color: #000099; font-weight: bold;">\S</span><span style="color: #000099; font-weight: bold;">\s</span>]*?)&lt;/a&gt; # 链接
                            [<span style="color: #000099; font-weight: bold;">\S</span><span style="color: #000099; font-weight: bold;">\s</span>]*?&lt;br/&gt;<span style="color: #000099; font-weight: bold;">\s</span>+((?:[<span style="color: #000099; font-weight: bold;">\S</span>]+[ ]?)+)<span style="color: #000099; font-weight: bold;">\s</span>+&lt;/td&gt; # 物品名称
                            [<span style="color: #000099; font-weight: bold;">\S</span><span style="color: #000099; font-weight: bold;">\s</span>]*?&lt;em&gt;(<span style="color: #000099; font-weight: bold;">\d</span>+)&lt;/em&gt; # 价格
                            [<span style="color: #000099; font-weight: bold;">\S</span><span style="color: #000099; font-weight: bold;">\s</span>]*?&lt;td&gt;[<span style="color: #000099; font-weight: bold;">\S</span><span style="color: #000099; font-weight: bold;">\s</span>]*?&lt;/td&gt; # TD
                            [<span style="color: #000099; font-weight: bold;">\S</span><span style="color: #000099; font-weight: bold;">\s</span>]*?&lt;td&gt;([<span style="color: #000099; font-weight: bold;">\S</span><span style="color: #000099; font-weight: bold;">\s</span>]*?)&lt;/td&gt; # 日期
                            [<span style="color: #000099; font-weight: bold;">\S</span><span style="color: #000099; font-weight: bold;">\s</span>]*?&lt;/tr&gt; #Last TR
                            &quot;&quot;&quot;</span><span style="color: #66cc66;">,</span> flags<span style="color: #66cc66;">=</span><span style="color: #dc143c;">re</span>.<span style="color: black;">MULTILINE</span>|<span style="color: #dc143c;">re</span>.<span style="color: black;">IGNORECASE</span>|<span style="color: #dc143c;">re</span>.<span style="color: black;">VERBOSE</span><span style="color: black;">&#41;</span>
    &nbsp;
        matchs <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">re</span>.<span style="color: black;">findall</span><span style="color: black;">&#40;</span>pattern<span style="color: #66cc66;">,</span> content <span style="color: black;">&#41;</span>
        <span style="color: #008000;">str</span> <span style="color: #66cc66;">=</span> <span style="color: #483d8b;">''</span>
        <span style="color: #ff7700;font-weight:bold;">for</span> match <span style="color: #ff7700;font-weight:bold;">in</span> matchs:
            <span style="color: #008000;">str</span> +<span style="color: #66cc66;">=</span> <span style="color: #dc143c;">string</span>.<span style="color: black;">ljust</span><span style="color: black;">&#40;</span>match<span style="color: black;">&#91;</span><span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span>.<span style="color: black;">strip</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">7</span><span style="color: black;">&#41;</span> + <span style="color: #dc143c;">string</span>.<span style="color: black;">ljust</span><span style="color: black;">&#40;</span>match<span style="color: black;">&#91;</span><span style="color: #ff4500;">3</span><span style="color: black;">&#93;</span><span style="color: black;">&#91;</span>:<span style="color: #ff4500;">11</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">15</span><span style="color: black;">&#41;</span> + match<span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>.<span style="color: black;">strip</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
            <span style="color: #008000;">str</span> +<span style="color: #66cc66;">=</span> <span style="color: #483d8b;">'<span style="color: #000099; font-weight: bold;">\n</span>'</span>
        <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: #008000;">str</span>
    &nbsp;
    filepath <span style="color: #66cc66;">=</span> <span style="color: #483d8b;">'c:<span style="color: #000099; font-weight: bold;">\\</span>log.txt'</span>
    <span style="color: #008000;">open</span><span style="color: black;">&#40;</span>filepath<span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'w'</span><span style="color: black;">&#41;</span>.<span style="color: black;">close</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    lastpage <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">150</span>
    <span style="color: #808080; font-style: italic;">#淘宝物品的成交记录下一页的链接，请复制链接，把最后一个页数的数字删掉，放在url变量里</span>
    url <span style="color: #66cc66;">=</span> <span style="color: #483d8b;">'http://tbskip.taobao.com/json/show_buyer_list.htm?is_offline=&amp;page_size=15&amp;is_start=false&amp;item_type=b&amp;ends=1305101478000&amp;starts=1304496678000&amp;item_id=8689953932&amp;user_tag=475363344&amp;old_quantity=1187&amp;sold_total_num=365&amp;closed=false&amp;seller_num_id=69211806&amp;zhichong=true&amp;bidPage='</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">range</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> lastpage + <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>:
        fullurl <span style="color: #66cc66;">=</span> url + <span style="color: #483d8b;">'%d'</span> % <span style="color: black;">&#40;</span>i<span style="color: #66cc66;">,</span><span style="color: black;">&#41;</span>
        <span style="color: #808080; font-style: italic;">#不出错运行后设为False</span>
        runfail <span style="color: #66cc66;">=</span> <span style="color: #008000;">True</span>
        <span style="color: #808080; font-style: italic;">#重试次数</span>
        retry <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">2</span>
        <span style="color: #ff7700;font-weight:bold;">print</span> fullurl
    &nbsp;
        <span style="color: #ff7700;font-weight:bold;">try</span>:
            logfile <span style="color: #66cc66;">=</span> <span style="color: #008000;">open</span><span style="color: black;">&#40;</span>filepath<span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'a'</span><span style="color: black;">&#41;</span>
    &nbsp;
            <span style="color: #ff7700;font-weight:bold;">while</span> <span style="color: black;">&#40;</span>runfail <span style="color: #ff7700;font-weight:bold;">and</span> retry <span style="color: #66cc66;">&gt;=</span> <span style="color: #ff4500;">0</span><span style="color: black;">&#41;</span>:
                <span style="color: #ff7700;font-weight:bold;">try</span>:
                    content <span style="color: #66cc66;">=</span> read<span style="color: black;">&#40;</span>fullurl<span style="color: black;">&#41;</span>
                    <span style="color: #008000;">str</span> <span style="color: #66cc66;">=</span> display<span style="color: black;">&#40;</span>content<span style="color: black;">&#41;</span>
                    logfile.<span style="color: black;">write</span><span style="color: black;">&#40;</span><span style="color: #008000;">str</span><span style="color: black;">&#41;</span>
    &nbsp;
                    runfail <span style="color: #66cc66;">=</span> <span style="color: #008000;">False</span>
                <span style="color: #ff7700;font-weight:bold;">except</span>:
                    <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">'*'</span> * <span style="color: #ff4500;">100</span>
                    <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">'error'</span>
                    <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">'*'</span> * <span style="color: #ff4500;">100</span>
                    retry <span style="color: #66cc66;">=</span> retry - <span style="color: #ff4500;">1</span>
                    <span style="color: #dc143c;">time</span>.<span style="color: black;">sleep</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">5</span><span style="color: black;">&#41;</span>
                    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: black;">&#40;</span>retry <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">0</span><span style="color: black;">&#41;</span>:<span style="color: #dc143c;">time</span>.<span style="color: black;">sleep</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">10</span><span style="color: black;">&#41;</span> <span style="color: #808080; font-style: italic;">#最后一次尝试等10秒</span>
    &nbsp;
            logfile.<span style="color: black;">flush</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
        <span style="color: #ff7700;font-weight:bold;">except</span>:
            <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">'write file fail!'</span>
        <span style="color: #ff7700;font-weight:bold;">finally</span>:
            logfile.<span style="color: black;">close</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">#-*- encoding: gbk -*-
    '''
    Created on 2011-5-8
    
    @author: fatkun
    '''
    import urllib2
    import re
    import time
    import string
    
    #读取网页
    def read(url):
        opener = urllib2.build_opener()
        #opener.handle_open[&quot;http&quot;][0].set_http_debuglevel(1)
        opener.addheaders = [('User-agent', 'Mozilla/5.0')]
        f= opener.open(url)
        content = f.read()
        return content
    
    #正则表达式返回需要的内容
    def display(content):
        pattern = re.compile(r&quot;&quot;&quot;&lt;tr(?:[^&gt;]+)?&gt; #TR
                            [\S\s]*?&lt;td[\S\s]*?&lt;/td&gt;[\S\s]*?&lt;td(?:[^&gt;]+)?&gt; #Second TD
                            [\S\s]*?&lt;a [^&gt;]+&gt;([\S\s]*?)&lt;/a&gt; # 链接
                            [\S\s]*?&lt;br/&gt;\s+((?:[\S]+[ ]?)+)\s+&lt;/td&gt; # 物品名称
                            [\S\s]*?&lt;em&gt;(\d+)&lt;/em&gt; # 价格
                            [\S\s]*?&lt;td&gt;[\S\s]*?&lt;/td&gt; # TD
                            [\S\s]*?&lt;td&gt;([\S\s]*?)&lt;/td&gt; # 日期
                            [\S\s]*?&lt;/tr&gt; #Last TR
                            &quot;&quot;&quot;, flags=re.MULTILINE|re.IGNORECASE|re.VERBOSE)
    
        matchs = re.findall(pattern, content )
        str = ''
        for match in matchs:
            str += string.ljust(match[2].strip(), 7) + string.ljust(match[3][:11], 15) + match[1].strip()
            str += '\n'
        return str
    
    filepath = 'c:\\log.txt'
    open(filepath, 'w').close()
    lastpage = 150
    #淘宝物品的成交记录下一页的链接，请复制链接，把最后一个页数的数字删掉，放在url变量里
    url = 'http://tbskip.taobao.com/json/show_buyer_list.htm?is_offline=&amp;page_size=15&amp;is_start=false&amp;item_type=b&amp;ends=1305101478000&amp;starts=1304496678000&amp;item_id=8689953932&amp;user_tag=475363344&amp;old_quantity=1187&amp;sold_total_num=365&amp;closed=false&amp;seller_num_id=69211806&amp;zhichong=true&amp;bidPage='
    for i in range(1, lastpage + 1):
        fullurl = url + '%d' % (i,)
        #不出错运行后设为False
        runfail = True
        #重试次数
        retry = 2
        print fullurl
    
        try:
            logfile = open(filepath, 'a')
    
            while (runfail and retry &gt;= 0):
                try:
                    content = read(fullurl)
                    str = display(content)
                    logfile.write(str)
    
                    runfail = False
                except:
                    print '*' * 100
                    print 'error'
                    print '*' * 100
                    retry = retry - 1
                    time.sleep(5)
                    if (retry == 0):time.sleep(10) #最后一次尝试等10秒
    
            logfile.flush()
        except:
            print 'write file fail!'
        finally:
            logfile.close()</p></div>
    ";}
categories:
  - python
tags:
  - python
  - 价格变化
  - 成交记录
  - 淘宝

---
本着学习urllib和正则re的原因和无比蛋疼，另外想把淘宝的成交记录全部列出来看看价格的变化  
在这个例子中你可以学到
  1. urllib2 addHeader的使用
  2. 正则表达式的使用
使用前需要配置一下url变量，淘宝物品的成交记录下一页的链接，请复制链接，把最后一个页数的数字删掉，放在url变量里  
因为里面太多参数了，没办法只改变某些变量
结果会保存在c:\log.txt文件内。  
<!--more-->

  
以下是代码
<pre escaped="true" lang="python">#-*- encoding: gbk -*-
'''
Created on 2011-5-8

@author: fatkun
'''
import urllib2
import re
import time
import string

#读取网页
def read(url):
    opener = urllib2.build_opener()
    #opener.handle_open["http"][0].set_http_debuglevel(1)
    opener.addheaders = [('User-agent', 'Mozilla/5.0')]
    f= opener.open(url)
    content = f.read()
    return content

#正则表达式返回需要的内容
def display(content):
    pattern = re.compile(r"""&lt;tr(?:[^&gt;]+)?&gt; #TR
                        [\S\s]*?&lt;td[\S\s]*?&lt;/td&gt;[\S\s]*?&lt;td(?:[^&gt;]+)?&gt; #Second TD
                        [\S\s]*?&lt;a [^&gt;]+&gt;([\S\s]*?)&lt;/a&gt; # 链接
                        [\S\s]*?&lt;br/&gt;\s+((?:[\S]+[ ]?)+)\s+&lt;/td&gt; # 物品名称
                        [\S\s]*?&lt;em&gt;(\d+)&lt;/em&gt; # 价格
                        [\S\s]*?&lt;td&gt;[\S\s]*?&lt;/td&gt; # TD
                        [\S\s]*?&lt;td&gt;([\S\s]*?)&lt;/td&gt; # 日期
                        [\S\s]*?&lt;/tr&gt; #Last TR
                        """, flags=re.MULTILINE|re.IGNORECASE|re.VERBOSE)

    matchs = re.findall(pattern, content )
    str = ''
    for match in matchs:
        str += string.ljust(match[2].strip(), 7) + string.ljust(match[3][:11], 15) + match[1].strip()
        str += '\n'
    return str

filepath = 'c:\\log.txt'
open(filepath, 'w').close()
lastpage = 150
#淘宝物品的成交记录下一页的链接，请复制链接，把最后一个页数的数字删掉，放在url变量里
url = 'http://tbskip.taobao.com/json/show_buyer_list.htm?is_offline=&page_size=15&is_start=false&item_type=b&ends=1305101478000&starts=1304496678000&item_id=8689953932&user_tag=475363344&old_quantity=1187&sold_total_num=365&closed=false&seller_num_id=69211806&zhichong=true&bidPage='
for i in range(1, lastpage + 1):
    fullurl = url + '%d' % (i,)
    #不出错运行后设为False
    runfail = True
    #重试次数
    retry = 2
    print fullurl

    try:
        logfile = open(filepath, 'a')

        while (runfail and retry &gt;= 0):
            try:
                content = read(fullurl)
                str = display(content)
                logfile.write(str)

                runfail = False
            except:
                print '*' * 100
                print 'error'
                print '*' * 100
                retry = retry - 1
                time.sleep(5)
                if (retry == 0):time.sleep(10) #最后一次尝试等10秒

        logfile.flush()
    except:
        print 'write file fail!'
    finally:
        logfile.close()</pre>