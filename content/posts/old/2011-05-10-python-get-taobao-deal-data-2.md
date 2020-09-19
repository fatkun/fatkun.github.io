---
title: Python遍历淘宝成交记录（版本二）
author: fatkun
type: post
date: 2011-05-10T15:49:15+00:00
url: /2011/05/python-get-taobao-deal-data-2.html
duoshuo_thread_id:
  - 6300408813887423233
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:21672:"
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
    <span style="color: #ff7700;font-weight:bold;">from</span> <span style="color: #dc143c;">operator</span> <span style="color: #ff7700;font-weight:bold;">import</span> itemgetter
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
        alist <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: black;">&#93;</span>
        <span style="color: #ff7700;font-weight:bold;">for</span> match <span style="color: #ff7700;font-weight:bold;">in</span> matchs:
            alist.<span style="color: black;">append</span><span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>match<span style="color: black;">&#91;</span><span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span>.<span style="color: black;">strip</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span><span style="color: #66cc66;">,</span> match<span style="color: black;">&#91;</span><span style="color: #ff4500;">3</span><span style="color: black;">&#93;</span>.<span style="color: black;">strip</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span><span style="color: black;">&#91;</span>:<span style="color: #ff4500;">11</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> match<span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>.<span style="color: black;">strip</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
        <span style="color: #ff7700;font-weight:bold;">return</span> alist
    &nbsp;
    filepath <span style="color: #66cc66;">=</span> <span style="color: #483d8b;">'c:<span style="color: #000099; font-weight: bold;">\\</span>log.txt'</span>
    resultfilepath <span style="color: #66cc66;">=</span> <span style="color: #483d8b;">'c:<span style="color: #000099; font-weight: bold;">\\</span>log_result.txt'</span>
    <span style="color: #008000;">open</span><span style="color: black;">&#40;</span>filepath<span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'w'</span><span style="color: black;">&#41;</span>.<span style="color: black;">close</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    lastpage <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">50</span>
    <span style="color: #808080; font-style: italic;">#淘宝物品的成交记录下一页的链接，请复制链接，把最后一个页数的数字删掉，放在url变量里</span>
    url <span style="color: #66cc66;">=</span> <span style="color: #483d8b;">'http://tbskip.taobao.com/json/show_buyer_list.htm?is_offline=&amp;page_size=15&amp;is_start=false&amp;item_type=b&amp;ends=1305198406000&amp;starts=1304593606000&amp;item_id=5964804060&amp;user_tag=475363344&amp;old_quantity=5521&amp;sold_total_num=3057&amp;closed=false&amp;seller_num_id=69211806&amp;zhichong=true&amp;bidPage='</span>
    onlyonelist <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: black;">&#93;</span>
    allfieldlist <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: black;">&#93;</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> i <span style="color: #ff7700;font-weight:bold;">in</span> <span style="color: #008000;">range</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">1</span><span style="color: #66cc66;">,</span> lastpage + <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span>:
        fullurl <span style="color: #66cc66;">=</span> <span style="color: #483d8b;">'%s%d'</span> % <span style="color: black;">&#40;</span>url<span style="color: #66cc66;">,</span> i<span style="color: black;">&#41;</span>
        <span style="color: #808080; font-style: italic;">#不出错运行后设为False</span>
        runfail <span style="color: #66cc66;">=</span> <span style="color: #008000;">True</span>
        <span style="color: #808080; font-style: italic;">#重试次数</span>
        retry <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">2</span>
        <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">'第%d页 - %s'</span> % <span style="color: black;">&#40;</span>i<span style="color: #66cc66;">,</span> fullurl<span style="color: black;">&#41;</span>
    &nbsp;
        <span style="color: #ff7700;font-weight:bold;">try</span>:
            logfile <span style="color: #66cc66;">=</span> <span style="color: #008000;">open</span><span style="color: black;">&#40;</span>filepath<span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'a'</span><span style="color: black;">&#41;</span>
    &nbsp;
            <span style="color: #ff7700;font-weight:bold;">while</span> <span style="color: black;">&#40;</span>runfail <span style="color: #ff7700;font-weight:bold;">and</span> retry <span style="color: #66cc66;">&gt;=</span> <span style="color: #ff4500;">0</span><span style="color: black;">&#41;</span>:
                <span style="color: #ff7700;font-weight:bold;">try</span>:
                    content <span style="color: #66cc66;">=</span> read<span style="color: black;">&#40;</span>fullurl<span style="color: black;">&#41;</span>
                    alist <span style="color: #66cc66;">=</span> display<span style="color: black;">&#40;</span>content<span style="color: black;">&#41;</span>
                    <span style="color: #008000;">str</span> <span style="color: #66cc66;">=</span> <span style="color: #483d8b;">''</span><span style="color: #66cc66;">;</span>
                    <span style="color: #ff7700;font-weight:bold;">for</span> record <span style="color: #ff7700;font-weight:bold;">in</span> alist:
                        price_product_record <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>record<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> record<span style="color: black;">&#91;</span><span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span><span style="color: black;">&#41;</span>
                        <span style="color: #ff7700;font-weight:bold;">if</span> price_product_record <span style="color: #ff7700;font-weight:bold;">not</span> <span style="color: #ff7700;font-weight:bold;">in</span> onlyonelist:
                            onlyonelist.<span style="color: black;">append</span><span style="color: black;">&#40;</span>price_product_record<span style="color: black;">&#41;</span>
                            allfieldlist.<span style="color: black;">append</span><span style="color: black;">&#40;</span>record<span style="color: black;">&#41;</span>
                            <span style="color: #008000;">str</span> +<span style="color: #66cc66;">=</span> <span style="color: #dc143c;">string</span>.<span style="color: black;">ljust</span><span style="color: black;">&#40;</span>record<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">7</span><span style="color: black;">&#41;</span> + <span style="color: #dc143c;">string</span>.<span style="color: black;">ljust</span><span style="color: black;">&#40;</span>record<span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">15</span><span style="color: black;">&#41;</span> + record<span style="color: black;">&#91;</span><span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span>
                            <span style="color: #008000;">str</span> +<span style="color: #66cc66;">=</span> <span style="color: #483d8b;">'<span style="color: #000099; font-weight: bold;">\n</span>'</span>
                    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #008000;">str</span> <span style="color: #66cc66;">!=</span> <span style="color: #483d8b;">''</span>: logfile.<span style="color: black;">write</span><span style="color: black;">&#40;</span><span style="color: #008000;">str</span><span style="color: black;">&#41;</span>
                    runfail <span style="color: #66cc66;">=</span> <span style="color: #008000;">False</span>
                <span style="color: #ff7700;font-weight:bold;">except</span> <span style="color: #008000;">IOError</span>:
                    <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">'IO error'</span>
                    retry <span style="color: #66cc66;">=</span> retry - <span style="color: #ff4500;">1</span>
                    <span style="color: #dc143c;">time</span>.<span style="color: black;">sleep</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">5</span><span style="color: black;">&#41;</span>
                    <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: black;">&#40;</span>retry <span style="color: #66cc66;">==</span> <span style="color: #ff4500;">0</span><span style="color: black;">&#41;</span>:<span style="color: #dc143c;">time</span>.<span style="color: black;">sleep</span><span style="color: black;">&#40;</span><span style="color: #ff4500;">10</span><span style="color: black;">&#41;</span> <span style="color: #808080; font-style: italic;">#最后一次尝试等10秒</span>
    &nbsp;
            logfile.<span style="color: black;">flush</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
        <span style="color: #ff7700;font-weight:bold;">except</span>:
            <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">'write file fail!'</span>
        <span style="color: #ff7700;font-weight:bold;">finally</span>:
            logfile.<span style="color: black;">close</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #808080; font-style: italic;">#保存排序后结果</span>
    allfieldlist.<span style="color: black;">sort</span><span style="color: black;">&#40;</span>key<span style="color: #66cc66;">=</span>itemgetter<span style="color: black;">&#40;</span><span style="color: #ff4500;">2</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">1</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    resultfile <span style="color: #66cc66;">=</span> <span style="color: #008000;">open</span><span style="color: black;">&#40;</span>resultfilepath<span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'w'</span><span style="color: black;">&#41;</span>
    <span style="color: #008000;">str</span> <span style="color: #66cc66;">=</span> <span style="color: #483d8b;">''</span>
    <span style="color: #ff7700;font-weight:bold;">for</span> record <span style="color: #ff7700;font-weight:bold;">in</span> allfieldlist:
        <span style="color: #008000;">str</span> +<span style="color: #66cc66;">=</span> <span style="color: #dc143c;">string</span>.<span style="color: black;">ljust</span><span style="color: black;">&#40;</span>record<span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">7</span><span style="color: black;">&#41;</span> + <span style="color: #dc143c;">string</span>.<span style="color: black;">ljust</span><span style="color: black;">&#40;</span>record<span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">15</span><span style="color: black;">&#41;</span> + record<span style="color: black;">&#91;</span><span style="color: #ff4500;">2</span><span style="color: black;">&#93;</span>
        <span style="color: #008000;">str</span> +<span style="color: #66cc66;">=</span> <span style="color: #483d8b;">'<span style="color: #000099; font-weight: bold;">\n</span>'</span>
    resultfile.<span style="color: black;">write</span><span style="color: black;">&#40;</span><span style="color: #008000;">str</span><span style="color: black;">&#41;</span>
    resultfile.<span style="color: black;">close</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
    <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: #483d8b;">'Success!'</span></pre></td></tr></table><p class="theCode" style="display:none;">#-*- encoding: gbk -*-
    '''
    Created on 2011-5-8
    
    @author: fatkun
    '''
    import urllib2
    import re
    import time
    import string
    from operator import itemgetter
    
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
        alist = []
        for match in matchs:
            alist.append((match[2].strip(), match[3].strip()[:11], match[1].strip()))
        return alist
    
    filepath = 'c:\\log.txt'
    resultfilepath = 'c:\\log_result.txt'
    open(filepath, 'w').close()
    lastpage = 50
    #淘宝物品的成交记录下一页的链接，请复制链接，把最后一个页数的数字删掉，放在url变量里
    url = 'http://tbskip.taobao.com/json/show_buyer_list.htm?is_offline=&amp;page_size=15&amp;is_start=false&amp;item_type=b&amp;ends=1305198406000&amp;starts=1304593606000&amp;item_id=5964804060&amp;user_tag=475363344&amp;old_quantity=5521&amp;sold_total_num=3057&amp;closed=false&amp;seller_num_id=69211806&amp;zhichong=true&amp;bidPage='
    onlyonelist = []
    allfieldlist = []
    for i in range(1, lastpage + 1):
        fullurl = '%s%d' % (url, i)
        #不出错运行后设为False
        runfail = True
        #重试次数
        retry = 2
        print '第%d页 - %s' % (i, fullurl)
        
        try:
            logfile = open(filepath, 'a')
            
            while (runfail and retry &gt;= 0):
                try:
                    content = read(fullurl)
                    alist = display(content)
                    str = '';
                    for record in alist:
                        price_product_record = (record[0], record[2])
                        if price_product_record not in onlyonelist:
                            onlyonelist.append(price_product_record)
                            allfieldlist.append(record)
                            str += string.ljust(record[0], 7) + string.ljust(record[1], 15) + record[2]
                            str += '\n'
                    if str != '': logfile.write(str)
                    runfail = False
                except IOError:
                    print 'IO error'
                    retry = retry - 1
                    time.sleep(5)
                    if (retry == 0):time.sleep(10) #最后一次尝试等10秒
                    
            logfile.flush()
        except:
            print 'write file fail!'
        finally:
            logfile.close()
    
    #保存排序后结果
    allfieldlist.sort(key=itemgetter(2, 1))
    resultfile = open(resultfilepath, 'w')
    str = ''
    for record in allfieldlist:
        str += string.ljust(record[0], 7) + string.ljust(record[1], 15) + record[2]
        str += '\n'
    resultfile.write(str)
    resultfile.close()
    print 'Success!'</p></div>
    ";}
categories:
  - python
tags:
  - python
  - 成交记录
  - 淘宝

---
在[前一版本][1]的基础上，加入了排序。按物品和日期来排序，排除重复的价格和物品  
<!--more-->

<pre escaped="true" lang="python">#-*- encoding: gbk -*-
'''
Created on 2011-5-8

@author: fatkun
'''
import urllib2
import re
import time
import string
from operator import itemgetter

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
    alist = []
    for match in matchs:
        alist.append((match[2].strip(), match[3].strip()[:11], match[1].strip()))
    return alist

filepath = 'c:\\log.txt'
resultfilepath = 'c:\\log_result.txt'
open(filepath, 'w').close()
lastpage = 50
#淘宝物品的成交记录下一页的链接，请复制链接，把最后一个页数的数字删掉，放在url变量里
url = 'http://tbskip.taobao.com/json/show_buyer_list.htm?is_offline=&page_size=15&is_start=false&item_type=b&ends=1305198406000&starts=1304593606000&item_id=5964804060&user_tag=475363344&old_quantity=5521&sold_total_num=3057&closed=false&seller_num_id=69211806&zhichong=true&bidPage='
onlyonelist = []
allfieldlist = []
for i in range(1, lastpage + 1):
    fullurl = '%s%d' % (url, i)
    #不出错运行后设为False
    runfail = True
    #重试次数
    retry = 2
    print '第%d页 - %s' % (i, fullurl)
    
    try:
        logfile = open(filepath, 'a')
        
        while (runfail and retry &gt;= 0):
            try:
                content = read(fullurl)
                alist = display(content)
                str = '';
                for record in alist:
                    price_product_record = (record[0], record[2])
                    if price_product_record not in onlyonelist:
                        onlyonelist.append(price_product_record)
                        allfieldlist.append(record)
                        str += string.ljust(record[0], 7) + string.ljust(record[1], 15) + record[2]
                        str += '\n'
                if str != '': logfile.write(str)
                runfail = False
            except IOError:
                print 'IO error'
                retry = retry - 1
                time.sleep(5)
                if (retry == 0):time.sleep(10) #最后一次尝试等10秒
                
        logfile.flush()
    except:
        print 'write file fail!'
    finally:
        logfile.close()

#保存排序后结果
allfieldlist.sort(key=itemgetter(2, 1))
resultfile = open(resultfilepath, 'w')
str = ''
for record in allfieldlist:
    str += string.ljust(record[0], 7) + string.ljust(record[1], 15) + record[2]
    str += '\n'
resultfile.write(str)
resultfile.close()
print 'Success!'
</pre>

 [1]: http://fatkun.com/2011/05/python-get-taobao-deal-data.html