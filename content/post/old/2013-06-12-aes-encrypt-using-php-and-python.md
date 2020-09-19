---
title: AES加密例子（python和php版本）
author: fatkun
type: post
date: 2013-06-12T06:48:18+00:00
url: /2013/06/aes-encrypt-using-php-and-python.html
duoshuo_thread_id:
  - 6300410024120288001
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:7470:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #ff7700;font-weight:bold;">class</span> MyCrypt<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>:
        <span style="color: #ff7700;font-weight:bold;">def</span> <span style="color: #0000cd;">__init__</span><span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: #66cc66;">,</span> key<span style="color: black;">&#41;</span>:
            <span style="color: #008000;">self</span>.<span style="color: black;">key</span> <span style="color: #66cc66;">=</span> key
            <span style="color: #008000;">self</span>.<span style="color: black;">mode</span> <span style="color: #66cc66;">=</span> AES.<span style="color: black;">MODE_CBC</span>
            <span style="color: #008000;">self</span>.<span style="color: black;">padding</span> <span style="color: #66cc66;">=</span> <span style="color: #483d8b;">'<span style="color: #000099; font-weight: bold;">\0</span>'</span>
    &nbsp;
        <span style="color: #ff7700;font-weight:bold;">def</span> encrypt<span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: #66cc66;">,</span> text<span style="color: black;">&#41;</span>:
            cryptor <span style="color: #66cc66;">=</span> AES.<span style="color: #dc143c;">new</span><span style="color: black;">&#40;</span><span style="color: #008000;">self</span>.<span style="color: black;">key</span><span style="color: #66cc66;">,</span> <span style="color: #008000;">self</span>.<span style="color: black;">mode</span><span style="color: black;">&#41;</span>
            length <span style="color: #66cc66;">=</span> <span style="color: #ff4500;">16</span>
            count <span style="color: #66cc66;">=</span> text.<span style="color: black;">count</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">''</span><span style="color: black;">&#41;</span>
            <span style="color: #ff7700;font-weight:bold;">if</span> count <span style="color: #66cc66;">&lt;</span> length:
                add <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>length - count<span style="color: black;">&#41;</span> + <span style="color: #ff4500;">1</span>
                text +<span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span><span style="color: #008000;">self</span>.<span style="color: black;">padding</span> * add<span style="color: black;">&#41;</span>
            <span style="color: #ff7700;font-weight:bold;">elif</span> count <span style="color: #66cc66;">&gt;</span> length:
                add <span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span>length - <span style="color: black;">&#40;</span>count % length<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span> + <span style="color: #ff4500;">1</span>
                text +<span style="color: #66cc66;">=</span> <span style="color: black;">&#40;</span><span style="color: #008000;">self</span>.<span style="color: black;">padding</span> * add<span style="color: black;">&#41;</span>
            <span style="color: #008000;">self</span>.<span style="color: black;">ciphertext</span> <span style="color: #66cc66;">=</span> cryptor.<span style="color: black;">encrypt</span><span style="color: black;">&#40;</span>text<span style="color: black;">&#41;</span>
            <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: #008000;">self</span>.<span style="color: black;">ciphertext</span>
    &nbsp;
        <span style="color: #ff7700;font-weight:bold;">def</span> decrypt<span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: #66cc66;">,</span> text<span style="color: black;">&#41;</span>:
            cryptor <span style="color: #66cc66;">=</span> AES.<span style="color: #dc143c;">new</span><span style="color: black;">&#40;</span><span style="color: #008000;">self</span>.<span style="color: black;">key</span><span style="color: #66cc66;">,</span> <span style="color: #008000;">self</span>.<span style="color: black;">mode</span><span style="color: black;">&#41;</span>
            plain_text <span style="color: #66cc66;">=</span> cryptor.<span style="color: black;">decrypt</span><span style="color: black;">&#40;</span>text<span style="color: black;">&#41;</span>
            <span style="color: #ff7700;font-weight:bold;">return</span> plain_text.<span style="color: black;">rstrip</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">&quot;<span style="color: #000099; font-weight: bold;">\0</span>&quot;</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> __name__ <span style="color: #66cc66;">==</span> <span style="color: #483d8b;">'__main__'</span>:
        key <span style="color: #66cc66;">=</span> <span style="color: #483d8b;">'1234567890abcdef'</span>
        data <span style="color: #66cc66;">=</span> <span style="color: #483d8b;">'{&quot;a&quot;: &quot;123中文&quot;, sss} '</span>
        ec <span style="color: #66cc66;">=</span> MyCrypt<span style="color: black;">&#40;</span>key<span style="color: black;">&#41;</span>
        encrpt_data <span style="color: #66cc66;">=</span> ec.<span style="color: black;">encrypt</span><span style="color: black;">&#40;</span>data<span style="color: black;">&#41;</span>
        decrpt_data <span style="color: #66cc66;">=</span> ec.<span style="color: black;">decrypt</span><span style="color: black;">&#40;</span>encrpt_data<span style="color: black;">&#41;</span>
        <span style="color: #ff7700;font-weight:bold;">print</span> encrpt_data<span style="color: #66cc66;">,</span> decrpt_data<span style="color: #66cc66;">,</span> decrpt_data <span style="color: #66cc66;">==</span> data
    &nbsp;
        <span style="color: #ff7700;font-weight:bold;">from</span> <span style="color: #dc143c;">base64</span> <span style="color: #ff7700;font-weight:bold;">import</span> b64encode<span style="color: #66cc66;">,</span> b64decode
        <span style="color: #ff7700;font-weight:bold;">print</span> b64encode<span style="color: black;">&#40;</span>encrpt_data<span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">class MyCrypt():
        def __init__(self, key):
            self.key = key
            self.mode = AES.MODE_CBC
            self.padding = '\0'
    
        def encrypt(self, text):
            cryptor = AES.new(self.key, self.mode)
            length = 16
            count = text.count('')
            if count &lt; length:
                add = (length - count) + 1
                text += (self.padding * add)
            elif count &gt; length:
                add = (length - (count % length)) + 1
                text += (self.padding * add)
            self.ciphertext = cryptor.encrypt(text)
            return self.ciphertext
    
        def decrypt(self, text):
            cryptor = AES.new(self.key, self.mode)
            plain_text = cryptor.decrypt(text)
            return plain_text.rstrip(&quot;\0&quot;)
    
    if __name__ == '__main__':
        key = '1234567890abcdef'
        data = '{&quot;a&quot;: &quot;123中文&quot;, sss} '
        ec = MyCrypt(key)
        encrpt_data = ec.encrypt(data)
        decrpt_data = ec.decrypt(encrpt_data)
        print encrpt_data, decrpt_data, decrpt_data == data
    
        from base64 import b64encode, b64decode
        print b64encode(encrpt_data)</p></div>
    ";i:2;s:5116:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="php" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">&lt;?php</span>
    <span style="color: #000088;">$privateKey</span> <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;1234567890abcdef&quot;</span><span style="color: #339933;">;</span>
    <span style="color: #000088;">$iv</span> 	<span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;<span style="color: #660099; font-weight: bold;">\0</span><span style="color: #660099; font-weight: bold;">\0</span><span style="color: #660099; font-weight: bold;">\0</span><span style="color: #660099; font-weight: bold;">\0</span><span style="color: #660099; font-weight: bold;">\0</span><span style="color: #660099; font-weight: bold;">\0</span><span style="color: #660099; font-weight: bold;">\0</span><span style="color: #660099; font-weight: bold;">\0</span><span style="color: #660099; font-weight: bold;">\0</span><span style="color: #660099; font-weight: bold;">\0</span><span style="color: #660099; font-weight: bold;">\0</span><span style="color: #660099; font-weight: bold;">\0</span><span style="color: #660099; font-weight: bold;">\0</span><span style="color: #660099; font-weight: bold;">\0</span><span style="color: #660099; font-weight: bold;">\0</span><span style="color: #660099; font-weight: bold;">\0</span>&quot;</span><span style="color: #339933;">;</span>
    <span style="color: #000088;">$data</span> 	<span style="color: #339933;">=</span> <span style="color: #0000ff;">'{&quot;a&quot;: &quot;123中文&quot;, sss}  '</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #666666; font-style: italic;">//加密</span>
    <span style="color: #000088;">$encrypted</span> <span style="color: #339933;">=</span> <span style="color: #990000;">mcrypt_encrypt</span><span style="color: #009900;">&#40;</span>MCRYPT_RIJNDAEL_128<span style="color: #339933;">,</span> <span style="color: #000088;">$privateKey</span><span style="color: #339933;">,</span> <span style="color: #000088;">$data</span><span style="color: #339933;">,</span> MCRYPT_MODE_CBC<span style="color: #339933;">,</span> <span style="color: #000088;">$iv</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #000088;">$edata</span> <span style="color: #339933;">=</span> <span style="color: #990000;">base64_encode</span><span style="color: #009900;">&#40;</span><span style="color: #000088;">$encrypted</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #b1b100;">echo</span> <span style="color: #000088;">$edata</span><span style="color: #339933;">;</span>
    <span style="color: #b1b100;">echo</span> <span style="color: #0000ff;">'&lt;br/&gt;'</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #666666; font-style: italic;">//解密</span>
    <span style="color: #000088;">$encryptedData</span> <span style="color: #339933;">=</span> <span style="color: #990000;">base64_decode</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">'6PIG4DBcjsDDxY9GtHq2TXjTVE5linoc/7i8CdJNTU0='</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #000088;">$decrypted</span> <span style="color: #339933;">=</span> <span style="color: #990000;">mcrypt_decrypt</span><span style="color: #009900;">&#40;</span>MCRYPT_RIJNDAEL_128<span style="color: #339933;">,</span> <span style="color: #000088;">$privateKey</span><span style="color: #339933;">,</span> <span style="color: #000088;">$encryptedData</span><span style="color: #339933;">,</span> MCRYPT_MODE_CBC<span style="color: #339933;">,</span> <span style="color: #000088;">$iv</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #b1b100;">echo</span><span style="color: #009900;">&#40;</span><span style="color: #990000;">rtrim</span><span style="color: #009900;">&#40;</span><span style="color: #000088;">$decrypted</span><span style="color: #339933;">,</span> <span style="color: #0000ff;">&quot;<span style="color: #660099; font-weight: bold;">\0</span>&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">?&gt;</span></pre></td></tr></table><p class="theCode" style="display:none;">&lt;?php
    $privateKey = &quot;1234567890abcdef&quot;;
    $iv 	= &quot;\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0&quot;;
    $data 	= '{&quot;a&quot;: &quot;123中文&quot;, sss}  ';
    
    //加密
    $encrypted = mcrypt_encrypt(MCRYPT_RIJNDAEL_128, $privateKey, $data, MCRYPT_MODE_CBC, $iv);
    $edata = base64_encode($encrypted);
    echo $edata;
    echo '&lt;br/&gt;';
    
    //解密
    $encryptedData = base64_decode('6PIG4DBcjsDDxY9GtHq2TXjTVE5linoc/7i8CdJNTU0=');
    $decrypted = mcrypt_decrypt(MCRYPT_RIJNDAEL_128, $privateKey, $encryptedData, MCRYPT_MODE_CBC, $iv);
    echo(rtrim($decrypted, &quot;\0&quot;));
    ?&gt;</p></div>
    ";}
categories:
  - python
tags:
  - AES
  - encrypt
  - 加密

---
python版本  
输入的加密字符必须是16的倍数，php的默认补零，所以解密的时候还需要rtrim掉零。python没有自动做这件事情，所以要自己补零。
<pre escaped="true" lang="python">class MyCrypt():
    def __init__(self, key):
        self.key = key
        self.mode = AES.MODE_CBC
        self.padding = '\0'

    def encrypt(self, text):
        cryptor = AES.new(self.key, self.mode)
        length = 16
        count = text.count('')
        if count &lt; length:
            add = (length - count) + 1
            text += (self.padding * add)
        elif count &gt; length:
            add = (length - (count % length)) + 1
            text += (self.padding * add)
        self.ciphertext = cryptor.encrypt(text)
        return self.ciphertext

    def decrypt(self, text):
        cryptor = AES.new(self.key, self.mode)
        plain_text = cryptor.decrypt(text)
        return plain_text.rstrip("\0")

if __name__ == '__main__':
    key = '1234567890abcdef'
    data = '{"a": "123中文", sss} '
    ec = MyCrypt(key)
    encrpt_data = ec.encrypt(data)
    decrpt_data = ec.decrypt(encrpt_data)
    print encrpt_data, decrpt_data, decrpt_data == data

    from base64 import b64encode, b64decode
    print b64encode(encrpt_data)</pre>
PHP版本:
<pre escaped="true" lang="php">&lt;?php
$privateKey = "1234567890abcdef";
$iv 	= "\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0\0";
$data 	= '{"a": "123中文", sss}  ';

//加密
$encrypted = mcrypt_encrypt(MCRYPT_RIJNDAEL_128, $privateKey, $data, MCRYPT_MODE_CBC, $iv);
$edata = base64_encode($encrypted);
echo $edata;
echo '&lt;br/&gt;';

//解密
$encryptedData = base64_decode('6PIG4DBcjsDDxY9GtHq2TXjTVE5linoc/7i8CdJNTU0=');
$decrypted = mcrypt_decrypt(MCRYPT_RIJNDAEL_128, $privateKey, $encryptedData, MCRYPT_MODE_CBC, $iv);
echo(rtrim($decrypted, "\0"));
?&gt;
</pre>