---
title: python生成缩略图和合并图片
author: fatkun
type: post
date: 2012-06-02T14:58:25+00:00
url: /2012/06/python-create-thumb-and-merge-images.html
duoshuo_thread_id:
  - 6300408858800030466
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:17390:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #808080; font-style: italic;">#!/usr/bin/env python</span>
    <span style="color: #808080; font-style: italic;">#coding=utf-8</span>
    <span style="color: #483d8b;">'''
    Created on 2012-6-2
    &nbsp;
    @author: fatkun
    '''</span>
    <span style="color: #ff7700;font-weight:bold;">import</span> Image
    <span style="color: #ff7700;font-weight:bold;">import</span> <span style="color: #dc143c;">os</span>
    <span style="color: #ff7700;font-weight:bold;">import</span> <span style="color: #dc143c;">sys</span>
    <span style="color: #ff7700;font-weight:bold;">import</span> <span style="color: #dc143c;">glob</span>
    <span style="color: #ff7700;font-weight:bold;">import</span> <span style="color: #dc143c;">time</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> make_thumb<span style="color: black;">&#40;</span>path<span style="color: #66cc66;">,</span> thumb_path<span style="color: #66cc66;">,</span> size<span style="color: black;">&#41;</span>:
        <span style="color: #483d8b;">&quot;&quot;&quot;生成缩略图&quot;&quot;&quot;</span>
        img <span style="color: #66cc66;">=</span> Image.<span style="color: #008000;">open</span><span style="color: black;">&#40;</span>path<span style="color: black;">&#41;</span>
        width<span style="color: #66cc66;">,</span> height <span style="color: #66cc66;">=</span> img.<span style="color: black;">size</span>
        <span style="color: #808080; font-style: italic;"># 裁剪图片成正方形</span>
        <span style="color: #ff7700;font-weight:bold;">if</span> width <span style="color: #66cc66;">&gt;</span> height:
            delta <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>width - height<span style="color: black;">&#41;</span> / <span style="color: #ff4500;">2</span>
            box <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>delta<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span> width - delta<span style="color: #66cc66;">,</span> height<span style="color: black;">&#41;</span>
            region <span style="color: #66cc66;">=</span> img.<span style="color: black;">crop</span><span style="color: black;">&#40;</span>box<span style="color: black;">&#41;</span>
        <span style="color: #ff7700;font-weight:bold;">elif</span> height <span style="color: #66cc66;">&gt;</span> width:
            delta <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>height - width<span style="color: black;">&#41;</span> / <span style="color: #ff4500;">2</span>
            box <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span> delta<span style="color: #66cc66;">,</span> width<span style="color: #66cc66;">,</span> height - delta<span style="color: black;">&#41;</span>
            region <span style="color: #66cc66;">=</span> img.<span style="color: black;">crop</span><span style="color: black;">&#40;</span>box<span style="color: black;">&#41;</span>
        <span style="color: #ff7700;font-weight:bold;">else</span>:
            region <span style="color: #66cc66;">=</span> img
    &nbsp;
        <span style="color: #808080; font-style: italic;"># 缩放</span>
        thumb <span style="color: #66cc66;">=</span> region.<span style="color: black;">resize</span><span style="color: black;">&#40;</span><span style="color: black;">&#40;</span>size<span style="color: #66cc66;">,</span> size<span style="color: black;">&#41;</span><span style="color: #66cc66;">,</span> Image.<span style="color: black;">ANTIALIAS</span><span style="color: black;">&#41;</span>
    &nbsp;
        base<span style="color: #66cc66;">,</span> ext <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">os</span>.<span style="color: black;">path</span>.<span style="color: black;">splitext</span><span style="color: black;">&#40;</span><span style="color: #dc143c;">os</span>.<span style="color: black;">path</span>.<span style="color: black;">basename</span><span style="color: black;">&#40;</span>path<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
        filename <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">os</span>.<span style="color: black;">path</span>.<span style="color: black;">join</span><span style="color: black;">&#40;</span>thumb_path<span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'%s_thumb.jpg'</span> % <span style="color: black;">&#40;</span>base<span style="color: #66cc66;">,</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
        <span style="color: #ff7700;font-weight:bold;">print</span> filename
        <span style="color: #808080; font-style: italic;"># 保存</span>
        thumb.<span style="color: black;">save</span><span style="color: black;">&#40;</span>filename<span style="color: #66cc66;">,</span> quality<span style="color: #66cc66;">=</span><span style="color: #ff4500;">70</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> merge_thumb<span style="color: black;">&#40;</span>files<span style="color: #66cc66;">,</span> output_file<span style="color: black;">&#41;</span>:
        <span style="color: #483d8b;">&quot;&quot;&quot;合并图片&quot;&quot;&quot;</span>
        imgs <span style="color: #66cc66;">=</span> <span style="color: black;">&#91;</span><span style="color: black;">&#93;</span>
        width <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
        height <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
    &nbsp;
        <span style="color: #808080; font-style: italic;"># 计算总宽度和长度</span>
        <span style="color: #ff7700;font-weight:bold;">for</span> <span style="color: #008000;">file</span> <span style="color: #ff7700;font-weight:bold;">in</span> files:
            img <span style="color: #66cc66;">=</span> Image.<span style="color: #008000;">open</span><span style="color: black;">&#40;</span><span style="color: #008000;">file</span><span style="color: black;">&#41;</span>
            <span style="color: #ff7700;font-weight:bold;">if</span> img.<span style="color: black;">mode</span> <span style="color: #66cc66;">!=</span> <span style="color: #483d8b;">'RGB'</span>:
                img <span style="color: #66cc66;">=</span> img.<span style="color: black;">convert</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">'RGB'</span><span style="color: black;">&#41;</span>
            imgs.<span style="color: black;">append</span><span style="color: black;">&#40;</span>img<span style="color: black;">&#41;</span>
            <span style="color: #ff7700;font-weight:bold;">if</span> img.<span style="color: black;">size</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span> <span style="color: #66cc66;">&gt;</span> width:
                width <span style="color: #66cc66;">=</span> img.<span style="color: black;">size</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">0</span><span style="color: black;">&#93;</span>
            height +<span style="color: #66cc66;">=</span> img.<span style="color: black;">size</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    &nbsp;
        <span style="color: #808080; font-style: italic;"># 新建一个白色底的图片</span>
        merge_img <span style="color: #66cc66;">=</span> Image.<span style="color: #dc143c;">new</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">'RGB'</span><span style="color: #66cc66;">,</span> <span style="color: black;">&#40;</span>width<span style="color: #66cc66;">,</span> height<span style="color: black;">&#41;</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">0xffffff</span><span style="color: black;">&#41;</span>
        cur_height <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">0</span>
        <span style="color: #ff7700;font-weight:bold;">for</span> img <span style="color: #ff7700;font-weight:bold;">in</span> imgs:
            <span style="color: #808080; font-style: italic;"># 把图片粘贴上去</span>
            merge_img.<span style="color: black;">paste</span><span style="color: black;">&#40;</span>img<span style="color: #66cc66;">,</span> <span style="color: black;">&#40;</span><span style="color: #ff4500;">0</span><span style="color: #66cc66;">,</span> cur_height<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
            cur_height +<span style="color: #66cc66;">=</span> img.<span style="color: black;">size</span><span style="color: black;">&#91;</span><span style="color: #ff4500;">1</span><span style="color: black;">&#93;</span>
    &nbsp;
        merge_img.<span style="color: black;">save</span><span style="color: black;">&#40;</span>output_file<span style="color: #66cc66;">,</span> quality<span style="color: #66cc66;">=</span><span style="color: #ff4500;">70</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> __name__ <span style="color: #66cc66;">==</span> <span style="color: #483d8b;">'__main__'</span>:
        ROOT_PATH <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">os</span>.<span style="color: black;">path</span>.<span style="color: black;">abspath</span><span style="color: black;">&#40;</span><span style="color: #dc143c;">os</span>.<span style="color: black;">path</span>.<span style="color: black;">dirname</span><span style="color: black;">&#40;</span>__file__<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
        IMG_PATH <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">os</span>.<span style="color: black;">path</span>.<span style="color: black;">join</span><span style="color: black;">&#40;</span>ROOT_PATH<span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'img'</span><span style="color: black;">&#41;</span>
        THUMB_PATH <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">os</span>.<span style="color: black;">path</span>.<span style="color: black;">join</span><span style="color: black;">&#40;</span>IMG_PATH<span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'thumbs'</span><span style="color: black;">&#41;</span>
        <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #ff7700;font-weight:bold;">not</span> <span style="color: #dc143c;">os</span>.<span style="color: black;">path</span>.<span style="color: black;">exists</span><span style="color: black;">&#40;</span>THUMB_PATH<span style="color: black;">&#41;</span>:
            <span style="color: #dc143c;">os</span>.<span style="color: black;">makedirs</span><span style="color: black;">&#40;</span>THUMB_PATH<span style="color: black;">&#41;</span>
    &nbsp;
        <span style="color: #808080; font-style: italic;"># 生成缩略图</span>
        files <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">glob</span>.<span style="color: #dc143c;">glob</span><span style="color: black;">&#40;</span><span style="color: #dc143c;">os</span>.<span style="color: black;">path</span>.<span style="color: black;">join</span><span style="color: black;">&#40;</span>IMG_PATH<span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'*.jpg'</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
        begin_time <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">time</span>.<span style="color: black;">clock</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
        <span style="color: #ff7700;font-weight:bold;">for</span> <span style="color: #008000;">file</span> <span style="color: #ff7700;font-weight:bold;">in</span> files:
            make_thumb<span style="color: black;">&#40;</span><span style="color: #008000;">file</span><span style="color: #66cc66;">,</span> THUMB_PATH<span style="color: #66cc66;">,</span> <span style="color: #ff4500;">90</span><span style="color: black;">&#41;</span>
        end_time <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">time</span>.<span style="color: black;">clock</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
        <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: black;">&#40;</span><span style="color: #483d8b;">'make_thumb time:%s'</span> % <span style="color: #008000;">str</span><span style="color: black;">&#40;</span>end_time - begin_time<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    &nbsp;
        <span style="color: #808080; font-style: italic;"># 合并图片</span>
        files <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">glob</span>.<span style="color: #dc143c;">glob</span><span style="color: black;">&#40;</span><span style="color: #dc143c;">os</span>.<span style="color: black;">path</span>.<span style="color: black;">join</span><span style="color: black;">&#40;</span>THUMB_PATH<span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'*_thumb.jpg'</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
        merge_output <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">os</span>.<span style="color: black;">path</span>.<span style="color: black;">join</span><span style="color: black;">&#40;</span>THUMB_PATH<span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'thumbs.jpg'</span><span style="color: black;">&#41;</span>
        begin_time <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">time</span>.<span style="color: black;">clock</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
        merge_thumb<span style="color: black;">&#40;</span>files<span style="color: #66cc66;">,</span> merge_output<span style="color: black;">&#41;</span>
        end_time <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">time</span>.<span style="color: black;">clock</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
        <span style="color: #ff7700;font-weight:bold;">print</span> <span style="color: black;">&#40;</span><span style="color: #483d8b;">'merge_thumb time:%s'</span> % <span style="color: #008000;">str</span><span style="color: black;">&#40;</span>end_time - begin_time<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">#!/usr/bin/env python
    #coding=utf-8
    '''
    Created on 2012-6-2
    
    @author: fatkun
    '''
    import Image
    import os
    import sys
    import glob
    import time
    
    def make_thumb(path, thumb_path, size):
        &quot;&quot;&quot;生成缩略图&quot;&quot;&quot;
        img = Image.open(path)
        width, height = img.size
        # 裁剪图片成正方形
        if width &gt; height:
            delta = (width - height) / 2
            box = (delta, 0, width - delta, height)
            region = img.crop(box)
        elif height &gt; width:
            delta = (height - width) / 2
            box = (0, delta, width, height - delta)
            region = img.crop(box)
        else:
            region = img
        
        # 缩放
        thumb = region.resize((size, size), Image.ANTIALIAS)
        
        base, ext = os.path.splitext(os.path.basename(path))
        filename = os.path.join(thumb_path, '%s_thumb.jpg' % (base,))
        print filename
        # 保存
        thumb.save(filename, quality=70)
        
    def merge_thumb(files, output_file):
        &quot;&quot;&quot;合并图片&quot;&quot;&quot;
        imgs = []
        width = 0
        height = 0
        
        # 计算总宽度和长度
        for file in files:
            img = Image.open(file)
            if img.mode != 'RGB':
                img = img.convert('RGB')
            imgs.append(img)
            if img.size[0] &gt; width:
                width = img.size[0]
            height += img.size[1]
        
        # 新建一个白色底的图片
        merge_img = Image.new('RGB', (width, height), 0xffffff)
        cur_height = 0
        for img in imgs:
            # 把图片粘贴上去
            merge_img.paste(img, (0, cur_height))
            cur_height += img.size[1]
        
        merge_img.save(output_file, quality=70)
    
    if __name__ == '__main__':
        ROOT_PATH = os.path.abspath(os.path.dirname(__file__))
        IMG_PATH = os.path.join(ROOT_PATH, 'img')
        THUMB_PATH = os.path.join(IMG_PATH, 'thumbs')
        if not os.path.exists(THUMB_PATH):
            os.makedirs(THUMB_PATH)
        
        # 生成缩略图
        files = glob.glob(os.path.join(IMG_PATH, '*.jpg'))
        begin_time = time.clock()
        for file in files:
            make_thumb(file, THUMB_PATH, 90)
        end_time = time.clock()
        print ('make_thumb time:%s' % str(end_time - begin_time))
        
        # 合并图片
        files = glob.glob(os.path.join(THUMB_PATH, '*_thumb.jpg'))
        merge_output = os.path.join(THUMB_PATH, 'thumbs.jpg')
        begin_time = time.clock()
        merge_thumb(files, merge_output)
        end_time = time.clock()
        print ('merge_thumb time:%s' % str(end_time - begin_time))</p></div>
    ";}
categories:
  - python
tags:
  - PIL
  - 合并图片
  - 图片处理
  - 缩略图

---
第一次使用[Python Imaging Library][1],参考了各类文章.  
直接贴代码吧,不长.容易理解
以下代码是把一个目录下的图片生成正方形的缩略图,并把缩略图合并成一个大图&#8230;
<pre escaped="true" lang="python">#!/usr/bin/env python
#coding=utf-8
'''
Created on 2012-6-2

@author: fatkun
'''
import Image
import os
import sys
import glob
import time

def make_thumb(path, thumb_path, size):
    """生成缩略图"""
    img = Image.open(path)
    width, height = img.size
    # 裁剪图片成正方形
    if width &gt; height:
        delta = (width - height) / 2
        box = (delta, 0, width - delta, height)
        region = img.crop(box)
    elif height &gt; width:
        delta = (height - width) / 2
        box = (0, delta, width, height - delta)
        region = img.crop(box)
    else:
        region = img
    
    # 缩放
    thumb = region.resize((size, size), Image.ANTIALIAS)
    
    base, ext = os.path.splitext(os.path.basename(path))
    filename = os.path.join(thumb_path, '%s_thumb.jpg' % (base,))
    print filename
    # 保存
    thumb.save(filename, quality=70)
    
def merge_thumb(files, output_file):
    """合并图片"""
    imgs = []
    width = 0
    height = 0
    
    # 计算总宽度和长度
    for file in files:
        img = Image.open(file)
        if img.mode != 'RGB':
            img = img.convert('RGB')
        imgs.append(img)
        if img.size[0] &gt; width:
            width = img.size[0]
        height += img.size[1]
    
    # 新建一个白色底的图片
    merge_img = Image.new('RGB', (width, height), 0xffffff)
    cur_height = 0
    for img in imgs:
        # 把图片粘贴上去
        merge_img.paste(img, (0, cur_height))
        cur_height += img.size[1]
    
    merge_img.save(output_file, quality=70)

if __name__ == '__main__':
    ROOT_PATH = os.path.abspath(os.path.dirname(__file__))
    IMG_PATH = os.path.join(ROOT_PATH, 'img')
    THUMB_PATH = os.path.join(IMG_PATH, 'thumbs')
    if not os.path.exists(THUMB_PATH):
        os.makedirs(THUMB_PATH)
    
    # 生成缩略图
    files = glob.glob(os.path.join(IMG_PATH, '*.jpg'))
    begin_time = time.clock()
    for file in files:
        make_thumb(file, THUMB_PATH, 90)
    end_time = time.clock()
    print ('make_thumb time:%s' % str(end_time - begin_time))
    
    # 合并图片
    files = glob.glob(os.path.join(THUMB_PATH, '*_thumb.jpg'))
    merge_output = os.path.join(THUMB_PATH, 'thumbs.jpg')
    begin_time = time.clock()
    merge_thumb(files, merge_output)
    end_time = time.clock()
    print ('merge_thumb time:%s' % str(end_time - begin_time))
    
</pre>
## 参考文章

[API][2]  
<a href="http://www.cnblogs.com/RChen/archive/2007/03/31/pil_thumb.html" title="用 PIL 写了个简单的缩略图生成程序" target="_blank">用 PIL 写了个简单的缩略图生成程序</a>  
<a href="http://hi.baidu.com/bluebanboom/item/08a7f4e2280a25adcf2d4f29" title="Python代码：合并图片" target="_blank">Python代码：合并图片</a>

 [1]: http://www.pythonware.com/products/pil/index.htm
 [2]: http://www.pythonware.com/library/pil/handbook/image.htm "http://www.pythonware.com/library/pil/handbook/image.htm"