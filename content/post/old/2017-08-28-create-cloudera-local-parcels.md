---
title: 构建cloudera自定义parcels
author: fatkun
type: post
date: 2017-08-28T10:15:54+00:00
url: /2017/08/create-cloudera-local-parcels.html
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:622:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #c20cb9; font-weight: bold;">tar</span> zcvf GPLEXTRAS-5.0.0-gplextras5b2.p0.32-el6.parcel GPLEXTRAS-5.0.0-gplextras5b2.p0.32<span style="color: #000000; font-weight: bold;">/</span> <span style="color: #660033;">--owner</span>=root <span style="color: #660033;">--group</span>=root</pre></td></tr></table><p class="theCode" style="display:none;">tar zcvf GPLEXTRAS-5.0.0-gplextras5b2.p0.32-el6.parcel GPLEXTRAS-5.0.0-gplextras5b2.p0.32/ --owner=root --group=root</p></div>
    ";i:2;s:1400:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #660033;">-rw-r--r--</span> <span style="color: #000000;">1</span> kpi kpi <span style="color: #000000;">15509175</span> Jul <span style="color: #000000;">19</span> <span style="color: #000000;">15</span>:<span style="color: #000000;">34</span> CUSTOM-5.4.0-<span style="color: #000000;">1</span>.cdh5.4.0.p2.5-el6.parcel
    <span style="color: #660033;">-rw-rw-r--</span> <span style="color: #000000;">1</span> kpi kpi       <span style="color: #000000;">41</span> Jul <span style="color: #000000;">19</span> <span style="color: #000000;">15</span>:<span style="color: #000000;">41</span> CUSTOM-5.4.0-<span style="color: #000000;">1</span>.cdh5.4.0.p2.5-el6.parcel.sha1
    <span style="color: #660033;">-rw-r--r--</span> <span style="color: #000000;">1</span> kpi kpi      <span style="color: #000000;">500</span> Jul <span style="color: #000000;">19</span> <span style="color: #000000;">15</span>:<span style="color: #000000;">52</span> manifest.json</pre></td></tr></table><p class="theCode" style="display:none;">-rw-r--r-- 1 kpi kpi 15509175 Jul 19 15:34 CUSTOM-5.4.0-1.cdh5.4.0.p2.5-el6.parcel
    -rw-rw-r-- 1 kpi kpi       41 Jul 19 15:41 CUSTOM-5.4.0-1.cdh5.4.0.p2.5-el6.parcel.sha1
    -rw-r--r-- 1 kpi kpi      500 Jul 19 15:52 manifest.json</p></div>
    ";i:3;s:1556:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="js" style="font-family:monospace;">{
        &quot;lastUpdated&quot;: 14993731500000,
        &quot;parcels&quot;: [
            {
                &quot;parcelName&quot;: &quot;CUSTOM-5.4.0-1.cdh5.4.0.p2.5-el6.parcel&quot;,
                &quot;components&quot;: [
                    {
                        &quot;pkg_version&quot;: &quot;2.5+cdh5.4.0+0&quot;,
                        &quot;name&quot;: &quot;hadoop-custom&quot;,
                        &quot;version&quot;: &quot;2.5+cdh5.4.0+0&quot;
                    }
                ],
                &quot;conflicts&quot;: &quot;CDH (&lt;&lt; 5.4.0), CDH (&gt;&gt; 5.12.0.)&quot;,
                &quot;hash&quot;: &quot;fba901a470aedc7f0e83248a989f7dcd04b5dafb&quot;
            }
        ]
    }</pre></td></tr></table><p class="theCode" style="display:none;">{
        &quot;lastUpdated&quot;: 14993731500000,
        &quot;parcels&quot;: [
            {
                &quot;parcelName&quot;: &quot;CUSTOM-5.4.0-1.cdh5.4.0.p2.5-el6.parcel&quot;,
                &quot;components&quot;: [
                    {
                        &quot;pkg_version&quot;: &quot;2.5+cdh5.4.0+0&quot;,
                        &quot;name&quot;: &quot;hadoop-custom&quot;,
                        &quot;version&quot;: &quot;2.5+cdh5.4.0+0&quot;
                    }
                ],
                &quot;conflicts&quot;: &quot;CDH (&lt;&lt; 5.4.0), CDH (&gt;&gt; 5.12.0.)&quot;,
                &quot;hash&quot;: &quot;fba901a470aedc7f0e83248a989f7dcd04b5dafb&quot;
            }
        ]
    }</p></div>
    ";}
categories:
  - hadoop
tags:
  - cloudera
  - parcel

---
构建命令：
<pre lang="bash" escaped="true">tar zcvf GPLEXTRAS-5.0.0-gplextras5b2.p0.32-el6.parcel GPLEXTRAS-5.0.0-gplextras5b2.p0.32/ --owner=root --group=root</pre>
把文件都放到一个http可访问的目录下，然后在“Parcel 设置”里面配置URL
目录结构
<pre lang="bash" escaped="true">-rw-r--r-- 1 kpi kpi 15509175 Jul 19 15:34 CUSTOM-5.4.0-1.cdh5.4.0.p2.5-el6.parcel
-rw-rw-r-- 1 kpi kpi       41 Jul 19 15:41 CUSTOM-5.4.0-1.cdh5.4.0.p2.5-el6.parcel.sha1
-rw-r--r-- 1 kpi kpi      500 Jul 19 15:52 manifest.json</pre>
manifest.json 文件如下，里面的hash值要对应上，components里面随便填，不要和原来的冲突
<pre lang="js" escaped="true">{
    "lastUpdated": 14993731500000,
    "parcels": [
        {
            "parcelName": "CUSTOM-5.4.0-1.cdh5.4.0.p2.5-el6.parcel",
            "components": [
                {
                    "pkg_version": "2.5+cdh5.4.0+0",
                    "name": "hadoop-custom",
                    "version": "2.5+cdh5.4.0+0"
                }
            ],
            "conflicts": "CDH (&lt;&lt; 5.4.0), CDH (&gt;&gt; 5.12.0.)",
            "hash": "fba901a470aedc7f0e83248a989f7dcd04b5dafb"
        }
    ]
}</pre>