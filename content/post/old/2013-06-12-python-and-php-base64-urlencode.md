---
title: 使用base64加密在URL传递(python和php版本)
author: fatkun
type: post
date: 2013-06-12T06:37:54+00:00
url: /2013/06/python-and-php-base64-urlencode.html
duoshuo_thread_id:
  - 6300410024078344961
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:2386:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">def</span> base64_url_decode<span style="color: black;">&#40;</span>inp<span style="color: black;">&#41;</span>:
        <span style="color: #808080; font-style: italic;"># 通过url传输时去掉了=号，所以需要补上=号</span>
        <span style="color: #ff7700;font-weight:bold;">import</span> <span style="color: #dc143c;">base64</span>
        <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: #dc143c;">base64</span>.<span style="color: black;">urlsafe_b64decode</span><span style="color: black;">&#40;</span><span style="color: #008000;">str</span><span style="color: black;">&#40;</span>inp + <span style="color: #483d8b;">'='</span> * <span style="color: black;">&#40;</span><span style="color: #ff4500;">4</span> - <span style="color: #008000;">len</span><span style="color: black;">&#40;</span>inp<span style="color: black;">&#41;</span> % <span style="color: #ff4500;">4</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> base64_url_encode<span style="color: black;">&#40;</span>inp<span style="color: black;">&#41;</span>:
        <span style="color: #ff7700;font-weight:bold;">import</span> <span style="color: #dc143c;">base64</span>
        <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: #dc143c;">base64</span>.<span style="color: black;">urlsafe_b64encode</span><span style="color: black;">&#40;</span><span style="color: #008000;">str</span><span style="color: black;">&#40;</span>inp<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>.<span style="color: black;">rstrip</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">'='</span><span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">def base64_url_decode(inp):
        # 通过url传输时去掉了=号，所以需要补上=号
        import base64
        return base64.urlsafe_b64decode(str(inp + '=' * (4 - len(inp) % 4)))
    
    def base64_url_encode(inp):
        import base64
        return base64.urlsafe_b64encode(str(inp)).rstrip('=')</p></div>
    ";i:2;s:2886:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="php" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">function</span> base64url_encode<span style="color: #009900;">&#40;</span><span style="color: #000088;">$data</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span> 
      <span style="color: #b1b100;">return</span> <span style="color: #990000;">rtrim</span><span style="color: #009900;">&#40;</span><span style="color: #990000;">strtr</span><span style="color: #009900;">&#40;</span><span style="color: #990000;">base64_encode</span><span style="color: #009900;">&#40;</span><span style="color: #000088;">$data</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #0000ff;">'+/'</span><span style="color: #339933;">,</span> <span style="color: #0000ff;">'-_'</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #0000ff;">'='</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> 
    <span style="color: #009900;">&#125;</span> 
    <span style="color: #000000; font-weight: bold;">function</span> base64url_decode<span style="color: #009900;">&#40;</span><span style="color: #000088;">$data</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span> 
      <span style="color: #b1b100;">return</span> <span style="color: #990000;">base64_decode</span><span style="color: #009900;">&#40;</span><span style="color: #990000;">str_pad</span><span style="color: #009900;">&#40;</span><span style="color: #990000;">strtr</span><span style="color: #009900;">&#40;</span><span style="color: #000088;">$data</span><span style="color: #339933;">,</span> <span style="color: #0000ff;">'-_'</span><span style="color: #339933;">,</span> <span style="color: #0000ff;">'+/'</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">,</span> <span style="color: #990000;">strlen</span><span style="color: #009900;">&#40;</span><span style="color: #000088;">$data</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">%</span> <span style="color: #cc66cc;">4</span><span style="color: #339933;">,</span> <span style="color: #0000ff;">'='</span><span style="color: #339933;">,</span> STR_PAD_RIGHT<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> 
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">function base64url_encode($data) { 
      return rtrim(strtr(base64_encode($data), '+/', '-_'), '='); 
    } 
    function base64url_decode($data) { 
      return base64_decode(str_pad(strtr($data, '-_', '+/'), strlen($data) % 4, '=', STR_PAD_RIGHT)); 
    }</p></div>
    ";}
categories:
  - python
tags:
  - base64
  - php
  - python

---
把base64加密后在url传输，会把“+“，”/”分别替换为&#8221;-&#8220;，&#8221;_&#8221;，以及会把末尾的等号“=”去掉。  
另外base64加密后的长度必然是4的倍数，所以可以根据这个还原“=”号
解密的过程就是这个的逆向。
注意：python必须补齐=号才正常，不然会抛错no padding.
python版本：
<pre escaped="true" lang="python">def base64_url_decode(inp):
    # 通过url传输时去掉了=号，所以需要补上=号
    import base64
    return base64.urlsafe_b64decode(str(inp + '=' * (4 - len(inp) % 4)))

def base64_url_encode(inp):
    import base64
    return base64.urlsafe_b64encode(str(inp)).rstrip('=')</pre>
php版本：
<pre escaped="true" lang="php">function base64url_encode($data) { 
  return rtrim(strtr(base64_encode($data), '+/', '-_'), '='); 
} 
function base64url_decode($data) { 
  return base64_decode(str_pad(strtr($data, '-_', '+/'), strlen($data) % 4, '=', STR_PAD_RIGHT)); 
} 
</pre>