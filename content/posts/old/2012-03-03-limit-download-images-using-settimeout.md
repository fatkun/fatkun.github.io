---
title: js模拟限制图片同时下载个数(使用setTimeout)
author: fatkun
type: post
date: 2012-03-03T13:24:15+00:00
url: /2012/03/limit-download-images-using-settimeout.html
duoshuo_thread_id:
  - 6300408827867038465
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:1834:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="js" style="font-family:monospace;">&lt;script language=&quot;javascript&quot;&gt;
    &nbsp;
        // 构造一些不同子域名的图片链接
        url = '.topit.me/4/cf/69/1130159413c3c69cf4l.jpg';
        var array = [];
        var hex = ['1', '2', '3', '4', '5', '6', '7', '8', '9', 'a', 'b', 'c', 'd', 'e', 'f']
        for (var i=0; i &lt; 20; i++) {
            var index = hex[i % 15];
            array.push('http://i' + index + url + '?time=' + i);
        }
    &nbsp;
        console.log(array);
    &nbsp;
        for (var i=0; i &lt; array.length; i++) {
            var img = new Image();
            img.onload = function() {
                console.log('onload', this.src);
            }
            img.onerror = function() {
                console.log('onerror', this.src);
            }
            img.src = array[i];
            console.log('array[i]', array[i]);
        }
    &nbsp;
    &lt;/script&gt;</pre></td></tr></table><p class="theCode" style="display:none;">&lt;script language=&quot;javascript&quot;&gt;
        
        // 构造一些不同子域名的图片链接
        url = '.topit.me/4/cf/69/1130159413c3c69cf4l.jpg';
        var array = [];
        var hex = ['1', '2', '3', '4', '5', '6', '7', '8', '9', 'a', 'b', 'c', 'd', 'e', 'f']
        for (var i=0; i &lt; 20; i++) {
            var index = hex[i % 15];
            array.push('http://i' + index + url + '?time=' + i);
        }
    
        console.log(array);
        
        for (var i=0; i &lt; array.length; i++) {
            var img = new Image();
            img.onload = function() {
                console.log('onload', this.src);
            }
            img.onerror = function() {
                console.log('onerror', this.src);
            }
            img.src = array[i];
            console.log('array[i]', array[i]);
        }
        
    &lt;/script&gt;</p></div>
    ";i:2;s:5018:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="js" style="font-family:monospace;">&lt;script language=&quot;javascript&quot;&gt;
    &nbsp;
        // 构造一些不同子域名的图片链接
        url = '.topit.me/4/cf/69/1130159413c3c69cf4l.jpg';
        var array = [];
        var hex = ['1', '2', '3', '4', '5', '6', '7', '8', '9', 'a', 'b', 'c', 'd', 'e', 'f']
        for (var i=0; i &lt; 20; i++) {
            var index = hex[i % 15];
            array.push('http://i' + index + url + '?time=' + i);
        }
    &nbsp;
        console.log(array);
    &nbsp;
        var QueneEnginer = function(){
            this.Quene = [];
        }
    &nbsp;
        QueneEnginer.prototype = {
            processTime: 100,
            loadNum: 0,
            maxDownloadNum: 5,
            add: function(arr) {
                for (var i=0; i &lt; arr.length; i++) {
                    this.Quene.push(arr[i]);
                }
            },
            start: function() {
                var that = this;
                setTimeout(function() {that.process();}, that.processTime);
            }, 
            process: function() {
                var that = this;
                if (this.Quene.length &gt; 0) {
                    while (this.loadNum &lt; this.maxDownloadNum) { // 如果有空位，就加载图片吧
                        var url = this.Quene.shift(); // 从数组取一个出来吧
                        if (url == null) {break;} // 取完了就中断
                        this.loadNum++;// 标记一下，我要开始下载咯
                        this.loadPic(url, function(src) {
                            document.write(src + '&lt;br/&gt;');
                            that.loadNum--; // 加载完图片记得减一哦
                            console.log('callback');
                        });
                    }
                    this.start(); // 这里是重点，利用了setTimeout，不断的循环，直到this.Quene.length &lt;= 0
                }
            }, 
            loadPic: function(url, callback) { //加载图片，实现callback为了回调计数
                var img = new Image();
                img.onload = function() {
                    console.log('onload', this.src);
                    callback(this.src);
                }
                img.onerror = function() {
                    console.log('onerror', this.src);
                    callback(this.src);
                }
                img.src = url;
                console.log('array[i]', url);
            }
        }
    &nbsp;
        var qe = new QueneEnginer();
        qe.add(array);
        qe.start();
    &nbsp;
    &lt;/script&gt;</pre></td></tr></table><p class="theCode" style="display:none;">&lt;script language=&quot;javascript&quot;&gt;
        
        // 构造一些不同子域名的图片链接
        url = '.topit.me/4/cf/69/1130159413c3c69cf4l.jpg';
        var array = [];
        var hex = ['1', '2', '3', '4', '5', '6', '7', '8', '9', 'a', 'b', 'c', 'd', 'e', 'f']
        for (var i=0; i &lt; 20; i++) {
            var index = hex[i % 15];
            array.push('http://i' + index + url + '?time=' + i);
        }
    
        console.log(array);
        
        var QueneEnginer = function(){
            this.Quene = [];
        }
        
        QueneEnginer.prototype = {
            processTime: 100,
            loadNum: 0,
            maxDownloadNum: 5,
            add: function(arr) {
                for (var i=0; i &lt; arr.length; i++) {
                    this.Quene.push(arr[i]);
                }
            },
            start: function() {
                var that = this;
                setTimeout(function() {that.process();}, that.processTime);
            }, 
            process: function() {
                var that = this;
                if (this.Quene.length &gt; 0) {
                    while (this.loadNum &lt; this.maxDownloadNum) { // 如果有空位，就加载图片吧
                        var url = this.Quene.shift(); // 从数组取一个出来吧
                        if (url == null) {break;} // 取完了就中断
                        this.loadNum++;// 标记一下，我要开始下载咯
                        this.loadPic(url, function(src) {
                            document.write(src + '&lt;br/&gt;');
                            that.loadNum--; // 加载完图片记得减一哦
                            console.log('callback');
                        });
                    }
                    this.start(); // 这里是重点，利用了setTimeout，不断的循环，直到this.Quene.length &lt;= 0
                }
            }, 
            loadPic: function(url, callback) { //加载图片，实现callback为了回调计数
                var img = new Image();
                img.onload = function() {
                    console.log('onload', this.src);
                    callback(this.src);
                }
                img.onerror = function() {
                    console.log('onerror', this.src);
                    callback(this.src);
                }
                img.src = url;
                console.log('array[i]', url);
            }
        }
        
        var qe = new QueneEnginer();
        qe.add(array);
        qe.start();
        
    &lt;/script&gt;</p></div>
    ";}
categories:
  - 网页前端
tags:
  - javascript
  - js
  - setTimeout
  - 图片下载

---
浏览器默认会对同一域名的图片有一个限制同时最多下载X个图片，但是如果图片是多域名的，有时候就会同时下载了很多图片，导致有些图片下载失败！  
先来看一段代码：
<pre escaped="true" lang="js">&lt;script language="javascript"&gt;
    
    // 构造一些不同子域名的图片链接
    url = '.topit.me/4/cf/69/1130159413c3c69cf4l.jpg';
    var array = [];
    var hex = ['1', '2', '3', '4', '5', '6', '7', '8', '9', 'a', 'b', 'c', 'd', 'e', 'f']
    for (var i=0; i &lt; 20; i++) {
        var index = hex[i % 15];
        array.push('http://i' + index + url + '?time=' + i);
    }

    console.log(array);
    
    for (var i=0; i &lt; array.length; i++) {
        var img = new Image();
        img.onload = function() {
            console.log('onload', this.src);
        }
        img.onerror = function() {
            console.log('onerror', this.src);
        }
        img.src = array[i];
        console.log('array[i]', array[i]);
    }
    
&lt;/script&gt;</pre>
这段代码模拟网页打开时加载图片，一次性给浏览器加载N个图片。  
把代码保存为html文件，在chrome浏览器打开。  
可以在控制台network看到图片的加载，如果是同一域名下，会限制X个图片同时下载，但不同域名就会看到一堆的图片在下载了，还有些图片下载失败了。
## 需求

我们需要人为限制一下图片同时下载的个数！并且分批来完成下载所有图片。
## 思路

有点像消费者/生产者模式，有一个生产者（目前已经生产了产品啦，就是一堆图片url），然后就有多个消费者去消费（拿url去下载图片）  
利用一个数组来模拟队列~然后取吧。。
## 实现

<pre escaped="true" lang="js">&lt;script language="javascript"&gt;
    
    // 构造一些不同子域名的图片链接
    url = '.topit.me/4/cf/69/1130159413c3c69cf4l.jpg';
    var array = [];
    var hex = ['1', '2', '3', '4', '5', '6', '7', '8', '9', 'a', 'b', 'c', 'd', 'e', 'f']
    for (var i=0; i &lt; 20; i++) {
        var index = hex[i % 15];
        array.push('http://i' + index + url + '?time=' + i);
    }

    console.log(array);
    
    var QueneEnginer = function(){
        this.Quene = [];
    }
    
    QueneEnginer.prototype = {
        processTime: 100,
        loadNum: 0,
        maxDownloadNum: 5,
        add: function(arr) {
            for (var i=0; i &lt; arr.length; i++) {
                this.Quene.push(arr[i]);
            }
        },
        start: function() {
            var that = this;
            setTimeout(function() {that.process();}, that.processTime);
        }, 
        process: function() {
            var that = this;
            if (this.Quene.length &gt; 0) {
                while (this.loadNum &lt; this.maxDownloadNum) { // 如果有空位，就加载图片吧
                    var url = this.Quene.shift(); // 从数组取一个出来吧
                    if (url == null) {break;} // 取完了就中断
                    this.loadNum++;// 标记一下，我要开始下载咯
                    this.loadPic(url, function(src) {
                        document.write(src + '&lt;br/&gt;');
                        that.loadNum--; // 加载完图片记得减一哦
                        console.log('callback');
                    });
                }
                this.start(); // 这里是重点，利用了setTimeout，不断的循环，直到this.Quene.length &lt;= 0
            }
        }, 
        loadPic: function(url, callback) { //加载图片，实现callback为了回调计数
            var img = new Image();
            img.onload = function() {
                console.log('onload', this.src);
                callback(this.src);
            }
            img.onerror = function() {
                console.log('onerror', this.src);
                callback(this.src);
            }
            img.src = url;
            console.log('array[i]', url);
        }
    }
    
    var qe = new QueneEnginer();
    qe.add(array);
    qe.start();
    
&lt;/script&gt;</pre>