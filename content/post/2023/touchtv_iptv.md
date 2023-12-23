---
title: "Touchtv iptv代码备份"
date: 2023-12-23T17:37:21+08:00
tags: [iptv]
categories: [vps]
author: "fatkun"
draft: false
---

代码来自恩山论坛 wjxgzz

php版本：https://www.right.com.cn/forum/thread-8294817-1-1.html

nodejs版本：https://www.right.com.cn/forum/thread-8294618-1-1.html

```php
<?php
    //触电新闻v3
    $pk = $_GET['pk'];
    $ts = time().'123';
    
    $pubKey = "MFwwDQYJKoZIhvcNAQEBBQADSwAwSAJBALLUiZV6DVmAcJGOsWzftnYxDVpIdTlQynYeTtq5Z1ZzUteINPX24GyeetbYjnIT8pq0IdXGEjjBtngvddR0YaMCAwEAAQ==";
    $pubKey = "-----BEGIN PUBLIC KEY-----\n".wordwrap($pubKey,64,"\n",true)."\n-----END PUBLIC KEY-----";
    $randIMEI = substr(md5(rand(10000000,99999999)),rand(0,15),16);
    
    openssl_public_encrypt("IMEI_".$randIMEI,$encData,$pubKey);

    $headers = [
        "X-ITOUCHTV-Ca-Key: 04039368653554864194910691389924",
        "referer: https://android.itouchtv.cn/".$randIMEI,
        "X-ITOUCHTV-A01: ".base64_encode($encData),
        "X-ITOUCHTV-CLIENT: NEWS_APP",
        "User-Agent: Mozilla/5.0 (Linux; Android 13.1.2;)",
        "X-ITOUCHTV-APP-VERSION: 4.9.2",
        "X-ITOUCHTV-Ca-Timestamp: $ts",
        "X-ITOUCHTV-A05: hFiVdSB9XwdEevy3UZlmj2BFW1o8S6MRLQVj1z7hBU4IfPS4tawaISroHYLgA5d1PcI2rIQCAud1nYH19Ks95A==", // 44
        "X-ITOUCHTV-RESOLUTION: 1920,1080",
        "X-ITOUCHTV-OSVS: 13.1.2"
    ];

    $signkey = "qmiHeB9bKgowHqxRv0prc2cPN2EwXL1HOYu3DPiYCcaYxyxdFIyT5mAfBmr0UKPO";
    $bstrURL = "https://tcdn-api.itouchtv.cn/getParam";
    $sign =base64_encode(hash_hmac("SHA256","GET\n$bstrURL\n$ts\n",$signkey,true));
    $headers[] = "X-ITOUCHTV-Ca-Signature:$sign";
    $ch = curl_init();
    curl_setopt($ch, CURLOPT_URL, $bstrURL);                  
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
    curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, FALSE); 
    curl_setopt($ch, CURLOPT_SSL_VERIFYHOST, FALSE); 
    curl_setopt($ch, CURLOPT_HTTPHEADER,$headers);
    $data = curl_exec($ch);
    curl_close($ch);
    $json = json_decode($data);
    $node = $json->node;
    array_pop($headers);
    
    $bstrURL = "https://api.itouchtv.cn/liveservice/v3/tvChannelList?node=$node";

    $sign = base64_encode(hash_hmac("SHA256","GET\n$bstrURL\n$ts\n",$signkey,true));
    $headers[] = "X-ITOUCHTV-Ca-Signature:$sign";

    $ch = curl_init();
    curl_setopt($ch, CURLOPT_URL, $bstrURL);                  
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
    curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, FALSE); 
    curl_setopt($ch, CURLOPT_SSL_VERIFYHOST, FALSE); 
    curl_setopt($ch, CURLOPT_HTTPHEADER,$headers);
    $data = curl_exec($ch);
    //echo $data;exit;
    curl_close($ch);
        
    if($pk == '')
    {
        $json = json_decode($data);
        foreach($json->tvChannelList as $out)
        {
            echo ($out->name.','.$out->pk.'<br />');
        }
    }
    else
    {
        preg_match('/pk":'.$pk.',.*?"url":"(.*?)"/i',$data,$result);
        $playURL = $result[1];
        header("location:$playURL");
    }
?>
```

