---
title: Hive On Tez cloudera5.4
author: fatkun
type: post
date: 2017-05-01T10:52:17+00:00
url: /2017/05/hive-on-tez-cloudera5-4.html
wp-syntax-cache-content:
  - |
    a:5:{i:1;s:5410:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;configuration<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>tez.lib.uris<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>${fs.defaultFS}/apps/tez-0.8.5/,${fs.defaultFS}/apps/tez-0.8.5/lib/<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    &nbsp;
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>tez.use.cluster.hadoop-libs<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>true<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    &nbsp;
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>tez.runtime.compress<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>true<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>tez.runtime.compress.codec<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>org.apache.hadoop.io.compress.SnappyCodec<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/configuration<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">&lt;configuration&gt;
      &lt;property&gt;
        &lt;name&gt;tez.lib.uris&lt;/name&gt;
        &lt;value&gt;${fs.defaultFS}/apps/tez-0.8.5/,${fs.defaultFS}/apps/tez-0.8.5/lib/&lt;/value&gt;
      &lt;/property&gt;
    
      &lt;property&gt;
        &lt;name&gt;tez.use.cluster.hadoop-libs&lt;/name&gt;
        &lt;value&gt;true&lt;/value&gt;
      &lt;/property&gt;
    
      &lt;property&gt;
        &lt;name&gt;tez.runtime.compress&lt;/name&gt;
        &lt;value&gt;true&lt;/value&gt;
      &lt;/property&gt;
      &lt;property&gt;
        &lt;name&gt;tez.runtime.compress.codec&lt;/name&gt;
        &lt;value&gt;org.apache.hadoop.io.compress.SnappyCodec&lt;/value&gt;
      &lt;/property&gt;
    &lt;/configuration&gt;</p></div>
    ";i:2;s:1252:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">Caused by: java.lang.ClassNotFoundException: Class com.hadoop.compression.lzo.LzoCodec not found
            at org.apache.hadoop.conf.Configuration.getClassByName<span style="color: #7a0874; font-weight: bold;">&#40;</span>Configuration.java:<span style="color: #000000;">2018</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
            at org.apache.hadoop.io.compress.CompressionCodecFactory.getCodecClasses<span style="color: #7a0874; font-weight: bold;">&#40;</span>CompressionCodecFactory.java:<span style="color: #000000;">128</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
            ... <span style="color: #000000;">23</span> <span style="color: #c20cb9; font-weight: bold;">more</span></pre></td></tr></table><p class="theCode" style="display:none;">Caused by: java.lang.ClassNotFoundException: Class com.hadoop.compression.lzo.LzoCodec not found
            at org.apache.hadoop.conf.Configuration.getClassByName(Configuration.java:2018)
            at org.apache.hadoop.io.compress.CompressionCodecFactory.getCodecClasses(CompressionCodecFactory.java:128)
            ... 23 more</p></div>
    ";i:3;s:400:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">Caused by: java.lang.ClassNotFoundException: org.apache.hadoop.hive.ql.exec.tez.HiveSplitGenerator</pre></td></tr></table><p class="theCode" style="display:none;">Caused by: java.lang.ClassNotFoundException: org.apache.hadoop.hive.ql.exec.tez.HiveSplitGenerator</p></div>
    ";i:4;s:6974:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;"><span style="color: #007800;">errorMessage</span>=Shuffle Runner Failed:org.apache.tez.runtime.library.common.shuffle.orderedgrouped.Shuffle<span style="color: #007800;">$ShuffleError</span>: Error <span style="color: #000000; font-weight: bold;">while</span> doing final merge 
            at org.apache.tez.runtime.library.common.shuffle.orderedgrouped.Shuffle<span style="color: #007800;">$RunShuffleCallable</span>.callInternal<span style="color: #7a0874; font-weight: bold;">&#40;</span>Shuffle.java:<span style="color: #000000;">320</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
            at org.apache.tez.runtime.library.common.shuffle.orderedgrouped.Shuffle<span style="color: #007800;">$RunShuffleCallable</span>.callInternal<span style="color: #7a0874; font-weight: bold;">&#40;</span>Shuffle.java:<span style="color: #000000;">285</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
            at org.apache.tez.common.CallableWithNdc.call<span style="color: #7a0874; font-weight: bold;">&#40;</span>CallableWithNdc.java:<span style="color: #000000;">36</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
            at java.util.concurrent.FutureTask.run<span style="color: #7a0874; font-weight: bold;">&#40;</span>FutureTask.java:<span style="color: #000000;">262</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
            at java.util.concurrent.ThreadPoolExecutor.runWorker<span style="color: #7a0874; font-weight: bold;">&#40;</span>ThreadPoolExecutor.java:<span style="color: #000000;">1145</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
            at java.util.concurrent.ThreadPoolExecutor<span style="color: #007800;">$Worker</span>.run<span style="color: #7a0874; font-weight: bold;">&#40;</span>ThreadPoolExecutor.java:<span style="color: #000000;">615</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
            at java.lang.Thread.run<span style="color: #7a0874; font-weight: bold;">&#40;</span>Thread.java:<span style="color: #000000;">745</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
    Caused by: java.io.IOException: Not a valid ifile header
            at org.apache.tez.runtime.library.common.sort.impl.IFile<span style="color: #007800;">$Reader</span>.verifyHeaderMagic<span style="color: #7a0874; font-weight: bold;">&#40;</span>IFile.java:<span style="color: #000000;">837</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
            at org.apache.tez.runtime.library.common.sort.impl.IFile<span style="color: #007800;">$Reader</span>.isCompressedFlagEnabled<span style="color: #7a0874; font-weight: bold;">&#40;</span>IFile.java:<span style="color: #000000;">844</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
            at org.apache.tez.runtime.library.common.sort.impl.IFile<span style="color: #007800;">$Reader</span>.<span style="color: #000000; font-weight: bold;">&lt;</span>init<span style="color: #000000; font-weight: bold;">&gt;</span><span style="color: #7a0874; font-weight: bold;">&#40;</span>IFile.java:<span style="color: #000000;">547</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
            at org.apache.tez.runtime.library.common.sort.impl.TezMerger<span style="color: #007800;">$DiskSegment</span>.init<span style="color: #7a0874; font-weight: bold;">&#40;</span>TezMerger.java:<span style="color: #000000;">407</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
            at org.apache.tez.runtime.library.common.sort.impl.TezMerger<span style="color: #007800;">$MergeQueue</span>.merge<span style="color: #7a0874; font-weight: bold;">&#40;</span>TezMerger.java:<span style="color: #000000;">753</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
            at org.apache.tez.runtime.library.common.sort.impl.TezMerger.merge<span style="color: #7a0874; font-weight: bold;">&#40;</span>TezMerger.java:<span style="color: #000000;">192</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
            at org.apache.tez.runtime.library.common.shuffle.orderedgrouped.MergeManager.finalMerge<span style="color: #7a0874; font-weight: bold;">&#40;</span>MergeManager.java:<span style="color: #000000;">1203</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
            at org.apache.tez.runtime.library.common.shuffle.orderedgrouped.MergeManager.close<span style="color: #7a0874; font-weight: bold;">&#40;</span>MergeManager.java:<span style="color: #000000;">583</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
            at org.apache.tez.runtime.library.common.shuffle.orderedgrouped.Shuffle<span style="color: #007800;">$RunShuffleCallable</span>.callInternal<span style="color: #7a0874; font-weight: bold;">&#40;</span>Shuffle.java:<span style="color: #000000;">316</span><span style="color: #7a0874; font-weight: bold;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">errorMessage=Shuffle Runner Failed:org.apache.tez.runtime.library.common.shuffle.orderedgrouped.Shuffle$ShuffleError: Error while doing final merge 
            at org.apache.tez.runtime.library.common.shuffle.orderedgrouped.Shuffle$RunShuffleCallable.callInternal(Shuffle.java:320)
            at org.apache.tez.runtime.library.common.shuffle.orderedgrouped.Shuffle$RunShuffleCallable.callInternal(Shuffle.java:285)
            at org.apache.tez.common.CallableWithNdc.call(CallableWithNdc.java:36)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)
            at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)
            at java.lang.Thread.run(Thread.java:745)
    Caused by: java.io.IOException: Not a valid ifile header
            at org.apache.tez.runtime.library.common.sort.impl.IFile$Reader.verifyHeaderMagic(IFile.java:837)
            at org.apache.tez.runtime.library.common.sort.impl.IFile$Reader.isCompressedFlagEnabled(IFile.java:844)
            at org.apache.tez.runtime.library.common.sort.impl.IFile$Reader.&lt;init&gt;(IFile.java:547)
            at org.apache.tez.runtime.library.common.sort.impl.TezMerger$DiskSegment.init(TezMerger.java:407)
            at org.apache.tez.runtime.library.common.sort.impl.TezMerger$MergeQueue.merge(TezMerger.java:753)
            at org.apache.tez.runtime.library.common.sort.impl.TezMerger.merge(TezMerger.java:192)
            at org.apache.tez.runtime.library.common.shuffle.orderedgrouped.MergeManager.finalMerge(MergeManager.java:1203)
            at org.apache.tez.runtime.library.common.shuffle.orderedgrouped.MergeManager.close(MergeManager.java:583)
            at org.apache.tez.runtime.library.common.shuffle.orderedgrouped.Shuffle$RunShuffleCallable.callInternal(Shuffle.java:316)</p></div>
    ";i:5;s:2582:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;">  <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>tez.runtime.compress<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>true<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>tez.runtime.compress.codec<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>org.apache.hadoop.io.compress.SnappyCodec<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">  &lt;property&gt;
        &lt;name&gt;tez.runtime.compress&lt;/name&gt;
        &lt;value&gt;true&lt;/value&gt;
      &lt;/property&gt;
      &lt;property&gt;
        &lt;name&gt;tez.runtime.compress.codec&lt;/name&gt;
        &lt;value&gt;org.apache.hadoop.io.compress.SnappyCodec&lt;/value&gt;
      &lt;/property&gt;</p></div>
    ";}
categories:
  - hadoop
  - hive
tags:
  - hadoop
  - hive
  - tez

---
## 配置

tez-site.xml
<pre escaped="true" lang="xml">&lt;configuration&gt;
  &lt;property&gt;
    &lt;name&gt;tez.lib.uris&lt;/name&gt;
    &lt;value&gt;${fs.defaultFS}/apps/tez-0.8.5/,${fs.defaultFS}/apps/tez-0.8.5/lib/&lt;/value&gt;
  &lt;/property&gt;

  &lt;property&gt;
    &lt;name&gt;tez.use.cluster.hadoop-libs&lt;/name&gt;
    &lt;value&gt;true&lt;/value&gt;
  &lt;/property&gt;

  &lt;property&gt;
    &lt;name&gt;tez.runtime.compress&lt;/name&gt;
    &lt;value&gt;true&lt;/value&gt;
  &lt;/property&gt;
  &lt;property&gt;
    &lt;name&gt;tez.runtime.compress.codec&lt;/name&gt;
    &lt;value&gt;org.apache.hadoop.io.compress.SnappyCodec&lt;/value&gt;
  &lt;/property&gt;
&lt;/configuration&gt;
</pre>
## 调优参数

tez.grouping.min-size 分片最小限制
## 报错处理

找不到lzo
<pre lang="bash" escaped="true">Caused by: java.lang.ClassNotFoundException: Class com.hadoop.compression.lzo.LzoCodec not found
        at org.apache.hadoop.conf.Configuration.getClassByName(Configuration.java:2018)
        at org.apache.hadoop.io.compress.CompressionCodecFactory.getCodecClasses(CompressionCodecFactory.java:128)
        ... 23 more</pre>
LZO包没加载到，我是把lzo.jar放入tez的lib里面，但是这样会导致不能用到native库，暂时没找到解决方法。
找不到org.apache.hadoop.hive.ql.exec.tez.HiveSplitGenerator
<pre escaped="true" lang="bash">Caused by: java.lang.ClassNotFoundException: org.apache.hadoop.hive.ql.exec.tez.HiveSplitGenerator</pre>
同样的解决方法，把hive-exec.jar放进去
<pre escaped="true" lang="bash">errorMessage=Shuffle Runner Failed:org.apache.tez.runtime.library.common.shuffle.orderedgrouped.Shuffle$ShuffleError: Error while doing final merge 
        at org.apache.tez.runtime.library.common.shuffle.orderedgrouped.Shuffle$RunShuffleCallable.callInternal(Shuffle.java:320)
        at org.apache.tez.runtime.library.common.shuffle.orderedgrouped.Shuffle$RunShuffleCallable.callInternal(Shuffle.java:285)
        at org.apache.tez.common.CallableWithNdc.call(CallableWithNdc.java:36)
        at java.util.concurrent.FutureTask.run(FutureTask.java:262)
        at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)
        at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)
        at java.lang.Thread.run(Thread.java:745)
Caused by: java.io.IOException: Not a valid ifile header
        at org.apache.tez.runtime.library.common.sort.impl.IFile$Reader.verifyHeaderMagic(IFile.java:837)
        at org.apache.tez.runtime.library.common.sort.impl.IFile$Reader.isCompressedFlagEnabled(IFile.java:844)
        at org.apache.tez.runtime.library.common.sort.impl.IFile$Reader.&lt;init&gt;(IFile.java:547)
        at org.apache.tez.runtime.library.common.sort.impl.TezMerger$DiskSegment.init(TezMerger.java:407)
        at org.apache.tez.runtime.library.common.sort.impl.TezMerger$MergeQueue.merge(TezMerger.java:753)
        at org.apache.tez.runtime.library.common.sort.impl.TezMerger.merge(TezMerger.java:192)
        at org.apache.tez.runtime.library.common.shuffle.orderedgrouped.MergeManager.finalMerge(MergeManager.java:1203)
        at org.apache.tez.runtime.library.common.shuffle.orderedgrouped.MergeManager.close(MergeManager.java:583)
        at org.apache.tez.runtime.library.common.shuffle.orderedgrouped.Shuffle$RunShuffleCallable.callInternal(Shuffle.java:316)</pre>
我是重新指定了一下压缩算法（tez.runtime.compress.codec），不知道为什么。压缩关掉也可以。
<pre escaped="true" lang="xml">&lt;property&gt;
    &lt;name&gt;tez.runtime.compress&lt;/name&gt;
    &lt;value&gt;true&lt;/value&gt;
  &lt;/property&gt;
  &lt;property&gt;
    &lt;name&gt;tez.runtime.compress.codec&lt;/name&gt;
    &lt;value&gt;org.apache.hadoop.io.compress.SnappyCodec&lt;/value&gt;
  &lt;/property&gt;</pre>
## 写的不错的文章

<a href="http://www.leocook.org/2016/05/09/Tez%E7%B3%BB%E5%88%97%E7%AC%AC%E4%BA%8C%E7%AF%87-hive_on_tez/" target="_blank">Tez系列第二篇 Hive_on_tez</a>