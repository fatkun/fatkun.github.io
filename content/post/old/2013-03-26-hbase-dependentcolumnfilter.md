---
title: Hbase DependentColumnFilter
author: fatkun
type: post
date: 2013-03-25T17:43:05+00:00
url: /2013/03/hbase-dependentcolumnfilter.html
duoshuo_thread_id:
  - 6300410014708269825
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:31894:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">package</span> <span style="color: #006699;">com.fatkun.filter.comparison</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">java.io.IOException</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.conf.Configuration</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.HBaseConfiguration</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.HColumnDescriptor</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.HTableDescriptor</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.KeyValue</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.client.Get</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.client.HBaseAdmin</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.client.HTable</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.client.Put</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.client.Result</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.client.ResultScanner</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.client.Scan</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.filter.BinaryPrefixComparator</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.filter.CompareFilter</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.filter.DependentColumnFilter</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.filter.Filter</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.filter.SubstringComparator</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.filter.ValueFilter</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.filter.WritableByteArrayComparable</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.util.Bytes</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> TestHbaseDependentColumnFilter <span style="color: #009900;">&#123;</span>
        <span style="color: #003399;">String</span> tableName <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;test_value_filter&quot;</span><span style="color: #339933;">;</span>
        Configuration config <span style="color: #339933;">=</span> HBaseConfiguration.<span style="color: #006633;">create</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> filter<span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">boolean</span> drop, CompareFilter.<span style="color: #006633;">CompareOp</span> operator,
                WritableByteArrayComparable comparator<span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">throws</span> <span style="color: #003399;">IOException</span> <span style="color: #009900;">&#123;</span>
    &nbsp;
            HTable table <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> HTable<span style="color: #009900;">&#40;</span>config, tableName<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #666666; font-style: italic;">//</span>
            Filter filter<span style="color: #339933;">;</span>
    &nbsp;
            <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>comparator <span style="color: #339933;">!=</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                <span style="color: #666666; font-style: italic;">// drop为true时，filter表示对&quot;col1&quot;列以外的所有&quot;data1&quot;列族数据做filter操作</span>
                <span style="color: #666666; font-style: italic;">// drop为false时,表示对所有&quot;data1&quot;列族的数据做filter操作</span>
                filter <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> DependentColumnFilter<span style="color: #009900;">&#40;</span>Bytes.<span style="color: #006633;">toBytes</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;data1&quot;</span><span style="color: #009900;">&#41;</span>,
                        Bytes.<span style="color: #006633;">toBytes</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;col1&quot;</span><span style="color: #009900;">&#41;</span>, drop, operator, comparator<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">else</span> <span style="color: #009900;">&#123;</span>
                filter <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> DependentColumnFilter<span style="color: #009900;">&#40;</span>Bytes.<span style="color: #006633;">toBytes</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;data1&quot;</span><span style="color: #009900;">&#41;</span>,
                        Bytes.<span style="color: #006633;">toBytes</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;col1&quot;</span><span style="color: #009900;">&#41;</span>, drop<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
            <span style="color: #666666; font-style: italic;">// filter应用于scan</span>
            Scan scan <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> Scan<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            scan.<span style="color: #006633;">setFilter</span><span style="color: #009900;">&#40;</span>filter<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            ResultScanner scanner <span style="color: #339933;">=</span> table.<span style="color: #006633;">getScanner</span><span style="color: #009900;">&#40;</span>scan<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
            <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span>Result result <span style="color: #339933;">:</span> scanner<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span>KeyValue kv <span style="color: #339933;">:</span> result.<span style="color: #006633;">list</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                    <span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;kv=&quot;</span> <span style="color: #339933;">+</span> kv.<span style="color: #006633;">toString</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot;,value=&quot;</span>
                            <span style="color: #339933;">+</span> Bytes.<span style="color: #006633;">toString</span><span style="color: #009900;">&#40;</span>kv.<span style="color: #006633;">getValue</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #009900;">&#125;</span>
            <span style="color: #009900;">&#125;</span>
            scanner.<span style="color: #006633;">close</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            table.<span style="color: #006633;">close</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        <span style="color: #008000; font-style: italic; font-weight: bold;">/**
         * 部分代码来自hbase权威指南
         * 
         * @throws IOException
         */</span>
        <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> testFilter<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">throws</span> <span style="color: #003399;">IOException</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #666666; font-style: italic;">// The dropDependentColumn parameter is giving you additional control</span>
            <span style="color: #666666; font-style: italic;">// over how the reference column is handled: it is either included or</span>
            <span style="color: #666666; font-style: italic;">// dropped by the filter</span>
    &nbsp;
            <span style="color: #666666; font-style: italic;">// 1.获取整个&quot;data1&quot;列族当前Version中的所有timestamp等于参照列&quot;data1:col1&quot;的数据</span>
            <span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;drop=false&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            filter<span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">false</span>, CompareFilter.<span style="color: #006633;">CompareOp</span>.<span style="color: #006633;">NO_OP</span>, <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #666666; font-style: italic;">// 2.获取除了&quot;col1&quot;列以外的&quot;data1&quot;列族中的所有timestamp等于参照列&quot;data1:col1&quot;的数据</span>
            <span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;drop=true&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            filter<span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">true</span>, CompareFilter.<span style="color: #006633;">CompareOp</span>.<span style="color: #006633;">NO_OP</span>, <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #666666; font-style: italic;">// 3.获取除了&quot;col1&quot;列以外的&quot;data1&quot;列族当前Version中的所有timestamp等于参照列&quot;data1:col1&quot;的,value以&quot;data100&quot;开头的所有数据</span>
            <span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;比较&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            filter<span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">true</span>, CompareFilter.<span style="color: #006633;">CompareOp</span>.<span style="color: #006633;">EQUAL</span>, <span style="color: #000000; font-weight: bold;">new</span> BinaryPrefixComparator<span style="color: #009900;">&#40;</span>
                    Bytes.<span style="color: #006633;">toBytes</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;data100&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        <span style="color: #008000; font-style: italic; font-weight: bold;">/**
         * 初始化数据
         */</span>
        <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> init<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #666666; font-style: italic;">// 创建表和初始化数据</span>
            <span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#123;</span>
                HBaseAdmin admin <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> HBaseAdmin<span style="color: #009900;">&#40;</span>config<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span><span style="color: #339933;">!</span>admin.<span style="color: #006633;">tableExists</span><span style="color: #009900;">&#40;</span>tableName<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                    HTableDescriptor htd <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> HTableDescriptor<span style="color: #009900;">&#40;</span>tableName<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    HColumnDescriptor hcd1 <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> HColumnDescriptor<span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;data1&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    htd.<span style="color: #006633;">addFamily</span><span style="color: #009900;">&#40;</span>hcd1<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    HColumnDescriptor hcd2 <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> HColumnDescriptor<span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;data2&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    htd.<span style="color: #006633;">addFamily</span><span style="color: #009900;">&#40;</span>hcd2<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    HColumnDescriptor hcd3 <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> HColumnDescriptor<span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;data3&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    htd.<span style="color: #006633;">addFamily</span><span style="color: #009900;">&#40;</span>hcd3<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    admin.<span style="color: #006633;">createTable</span><span style="color: #009900;">&#40;</span>htd<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #009900;">&#125;</span>
    &nbsp;
                HTable table <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> HTable<span style="color: #009900;">&#40;</span>config, tableName<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
                table.<span style="color: #006633;">setAutoFlush</span><span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">false</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #000066; font-weight: bold;">int</span> count <span style="color: #339933;">=</span> <span style="color: #cc66cc;">50</span><span style="color: #339933;">;</span>
                <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> i <span style="color: #339933;">=</span> <span style="color: #cc66cc;">1</span><span style="color: #339933;">;</span> i <span style="color: #339933;">&lt;=</span> count<span style="color: #339933;">;</span> <span style="color: #339933;">++</span>i<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                    Put p <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> Put<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span>.<span style="color: #006633;">format</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;row%03d&quot;</span>, i<span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getBytes</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    p.<span style="color: #006633;">add</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;data1&quot;</span>.<span style="color: #006633;">getBytes</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, <span style="color: #003399;">String</span>.<span style="color: #006633;">format</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;col%01d&quot;</span>, i <span style="color: #339933;">%</span> <span style="color: #cc66cc;">10</span><span style="color: #009900;">&#41;</span>
                            .<span style="color: #006633;">getBytes</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, <span style="color: #003399;">String</span>.<span style="color: #006633;">format</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;data1%03d&quot;</span>, i<span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getBytes</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    p.<span style="color: #006633;">add</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;data2&quot;</span>.<span style="color: #006633;">getBytes</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, <span style="color: #003399;">String</span>.<span style="color: #006633;">format</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;col%01d&quot;</span>, i <span style="color: #339933;">%</span> <span style="color: #cc66cc;">10</span><span style="color: #009900;">&#41;</span>
                            .<span style="color: #006633;">getBytes</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, <span style="color: #003399;">String</span>.<span style="color: #006633;">format</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;data2%03d&quot;</span>, i<span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getBytes</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    p.<span style="color: #006633;">add</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;data3&quot;</span>.<span style="color: #006633;">getBytes</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, <span style="color: #003399;">String</span>.<span style="color: #006633;">format</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;col%01d&quot;</span>, i <span style="color: #339933;">%</span> <span style="color: #cc66cc;">10</span><span style="color: #009900;">&#41;</span>
                            .<span style="color: #006633;">getBytes</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, <span style="color: #003399;">String</span>.<span style="color: #006633;">format</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;data3%03d&quot;</span>, i<span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getBytes</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    table.<span style="color: #006633;">put</span><span style="color: #009900;">&#40;</span>p<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #009900;">&#125;</span>
                table.<span style="color: #006633;">close</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
            <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">IOException</span> e<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                e.<span style="color: #006633;">printStackTrace</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        <span style="color: #008000; font-style: italic; font-weight: bold;">/**
         * @param args
         * @throws IOException
         */</span>
        <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000066; font-weight: bold;">void</span> main<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> args<span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">throws</span> <span style="color: #003399;">IOException</span> <span style="color: #009900;">&#123;</span>
            TestHbaseDependentColumnFilter test <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> TestHbaseDependentColumnFilter<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            test.<span style="color: #006633;">init</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            test.<span style="color: #006633;">testFilter</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">package com.fatkun.filter.comparison;
    
    import java.io.IOException;
    
    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.HColumnDescriptor;
    import org.apache.hadoop.hbase.HTableDescriptor;
    import org.apache.hadoop.hbase.KeyValue;
    import org.apache.hadoop.hbase.client.Get;
    import org.apache.hadoop.hbase.client.HBaseAdmin;
    import org.apache.hadoop.hbase.client.HTable;
    import org.apache.hadoop.hbase.client.Put;
    import org.apache.hadoop.hbase.client.Result;
    import org.apache.hadoop.hbase.client.ResultScanner;
    import org.apache.hadoop.hbase.client.Scan;
    import org.apache.hadoop.hbase.filter.BinaryPrefixComparator;
    import org.apache.hadoop.hbase.filter.CompareFilter;
    import org.apache.hadoop.hbase.filter.DependentColumnFilter;
    import org.apache.hadoop.hbase.filter.Filter;
    import org.apache.hadoop.hbase.filter.SubstringComparator;
    import org.apache.hadoop.hbase.filter.ValueFilter;
    import org.apache.hadoop.hbase.filter.WritableByteArrayComparable;
    import org.apache.hadoop.hbase.util.Bytes;
    
    public class TestHbaseDependentColumnFilter {
        String tableName = &quot;test_value_filter&quot;;
        Configuration config = HBaseConfiguration.create();
    
        public void filter(boolean drop, CompareFilter.CompareOp operator,
                WritableByteArrayComparable comparator) throws IOException {
    
            HTable table = new HTable(config, tableName);
            //
            Filter filter;
    
            if (comparator != null) {
                // drop为true时，filter表示对&quot;col1&quot;列以外的所有&quot;data1&quot;列族数据做filter操作
                // drop为false时,表示对所有&quot;data1&quot;列族的数据做filter操作
                filter = new DependentColumnFilter(Bytes.toBytes(&quot;data1&quot;),
                        Bytes.toBytes(&quot;col1&quot;), drop, operator, comparator);
            } else {
                filter = new DependentColumnFilter(Bytes.toBytes(&quot;data1&quot;),
                        Bytes.toBytes(&quot;col1&quot;), drop);
            }
            // filter应用于scan
            Scan scan = new Scan();
            scan.setFilter(filter);
            ResultScanner scanner = table.getScanner(scan);
    
            for (Result result : scanner) {
                for (KeyValue kv : result.list()) {
                    System.out.println(&quot;kv=&quot; + kv.toString() + &quot;,value=&quot;
                            + Bytes.toString(kv.getValue()));
                }
            }
            scanner.close();
            table.close();
        }
    
        /**
         * 部分代码来自hbase权威指南
         * 
         * @throws IOException
         */
        public void testFilter() throws IOException {
            // The dropDependentColumn parameter is giving you additional control
            // over how the reference column is handled: it is either included or
            // dropped by the filter
    
            // 1.获取整个&quot;data1&quot;列族当前Version中的所有timestamp等于参照列&quot;data1:col1&quot;的数据
            System.out.println(&quot;drop=false&quot;);
            filter(false, CompareFilter.CompareOp.NO_OP, null);
            // 2.获取除了&quot;col1&quot;列以外的&quot;data1&quot;列族中的所有timestamp等于参照列&quot;data1:col1&quot;的数据
            System.out.println(&quot;drop=true&quot;);
            filter(true, CompareFilter.CompareOp.NO_OP, null);
            // 3.获取除了&quot;col1&quot;列以外的&quot;data1&quot;列族当前Version中的所有timestamp等于参照列&quot;data1:col1&quot;的,value以&quot;data100&quot;开头的所有数据
            System.out.println(&quot;比较&quot;);
            filter(true, CompareFilter.CompareOp.EQUAL, new BinaryPrefixComparator(
                    Bytes.toBytes(&quot;data100&quot;)));
    
        }
    
        /**
         * 初始化数据
         */
        public void init() {
            // 创建表和初始化数据
            try {
                HBaseAdmin admin = new HBaseAdmin(config);
                if (!admin.tableExists(tableName)) {
                    HTableDescriptor htd = new HTableDescriptor(tableName);
                    HColumnDescriptor hcd1 = new HColumnDescriptor(&quot;data1&quot;);
                    htd.addFamily(hcd1);
                    HColumnDescriptor hcd2 = new HColumnDescriptor(&quot;data2&quot;);
                    htd.addFamily(hcd2);
                    HColumnDescriptor hcd3 = new HColumnDescriptor(&quot;data3&quot;);
                    htd.addFamily(hcd3);
                    admin.createTable(htd);
                }
    
                HTable table = new HTable(config, tableName);
    
                table.setAutoFlush(false);
                int count = 50;
                for (int i = 1; i &lt;= count; ++i) {
                    Put p = new Put(String.format(&quot;row%03d&quot;, i).getBytes());
                    p.add(&quot;data1&quot;.getBytes(), String.format(&quot;col%01d&quot;, i % 10)
                            .getBytes(), String.format(&quot;data1%03d&quot;, i).getBytes());
                    p.add(&quot;data2&quot;.getBytes(), String.format(&quot;col%01d&quot;, i % 10)
                            .getBytes(), String.format(&quot;data2%03d&quot;, i).getBytes());
                    p.add(&quot;data3&quot;.getBytes(), String.format(&quot;col%01d&quot;, i % 10)
                            .getBytes(), String.format(&quot;data3%03d&quot;, i).getBytes());
                    table.put(p);
                }
                table.close();
    
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    
        /**
         * @param args
         * @throws IOException
         */
        public static void main(String[] args) throws IOException {
            TestHbaseDependentColumnFilter test = new TestHbaseDependentColumnFilter();
            test.init();
            test.testFilter();
        }
    
    }</p></div>
    ";}
categories:
  - hbase
tags:
  - filter
  - hbase

---
> Here you have a more complex filter that does not simply filter out data based on  
> directly available information. Rather, it lets you specify a dependent column—or  
> reference column—that controls how other columns are filtered. It uses the timestamp  
> of the reference column and includes all other columns that have the same timestamp.
尝试找到该列所在的每一行，并返回该行具有相同时间戳的全部键值对。如果某一行不包含指定的列，则该行的任何键值对都不返回。  
如果dropDependentColumn=true，则从属列不返回。
via: <a href="http://abloz.com/2012/08/22/the-hbases-content-query-2.html" target="_blank">http://abloz.com/2012/08/22/the-hbases-content-query-2.html</a>
<pre escaped="true" lang="java">package com.fatkun.filter.comparison;

import java.io.IOException;

import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.hbase.HBaseConfiguration;
import org.apache.hadoop.hbase.HColumnDescriptor;
import org.apache.hadoop.hbase.HTableDescriptor;
import org.apache.hadoop.hbase.KeyValue;
import org.apache.hadoop.hbase.client.Get;
import org.apache.hadoop.hbase.client.HBaseAdmin;
import org.apache.hadoop.hbase.client.HTable;
import org.apache.hadoop.hbase.client.Put;
import org.apache.hadoop.hbase.client.Result;
import org.apache.hadoop.hbase.client.ResultScanner;
import org.apache.hadoop.hbase.client.Scan;
import org.apache.hadoop.hbase.filter.BinaryPrefixComparator;
import org.apache.hadoop.hbase.filter.CompareFilter;
import org.apache.hadoop.hbase.filter.DependentColumnFilter;
import org.apache.hadoop.hbase.filter.Filter;
import org.apache.hadoop.hbase.filter.SubstringComparator;
import org.apache.hadoop.hbase.filter.ValueFilter;
import org.apache.hadoop.hbase.filter.WritableByteArrayComparable;
import org.apache.hadoop.hbase.util.Bytes;

public class TestHbaseDependentColumnFilter {
    String tableName = "test_value_filter";
    Configuration config = HBaseConfiguration.create();

    public void filter(boolean drop, CompareFilter.CompareOp operator,
            WritableByteArrayComparable comparator) throws IOException {

        HTable table = new HTable(config, tableName);
        //
        Filter filter;

        if (comparator != null) {
            // drop为true时，filter表示对"col1"列以外的所有"data1"列族数据做filter操作
            // drop为false时,表示对所有"data1"列族的数据做filter操作
            filter = new DependentColumnFilter(Bytes.toBytes("data1"),
                    Bytes.toBytes("col1"), drop, operator, comparator);
        } else {
            filter = new DependentColumnFilter(Bytes.toBytes("data1"),
                    Bytes.toBytes("col1"), drop);
        }
        // filter应用于scan
        Scan scan = new Scan();
        scan.setFilter(filter);
        ResultScanner scanner = table.getScanner(scan);

        for (Result result : scanner) {
            for (KeyValue kv : result.list()) {
                System.out.println("kv=" + kv.toString() + ",value="
                        + Bytes.toString(kv.getValue()));
            }
        }
        scanner.close();
        table.close();
    }

    /**
     * 部分代码来自hbase权威指南
     * 
     * @throws IOException
     */
    public void testFilter() throws IOException {
        // The dropDependentColumn parameter is giving you additional control
        // over how the reference column is handled: it is either included or
        // dropped by the filter

        // 1.获取整个"data1"列族当前Version中的所有timestamp等于参照列"data1:col1"的数据
        System.out.println("drop=false");
        filter(false, CompareFilter.CompareOp.NO_OP, null);
        // 2.获取除了"col1"列以外的"data1"列族中的所有timestamp等于参照列"data1:col1"的数据
        System.out.println("drop=true");
        filter(true, CompareFilter.CompareOp.NO_OP, null);
        // 3.获取除了"col1"列以外的"data1"列族当前Version中的所有timestamp等于参照列"data1:col1"的,value以"data100"开头的所有数据
        System.out.println("比较");
        filter(true, CompareFilter.CompareOp.EQUAL, new BinaryPrefixComparator(
                Bytes.toBytes("data100")));

    }

    /**
     * 初始化数据
     */
    public void init() {
        // 创建表和初始化数据
        try {
            HBaseAdmin admin = new HBaseAdmin(config);
            if (!admin.tableExists(tableName)) {
                HTableDescriptor htd = new HTableDescriptor(tableName);
                HColumnDescriptor hcd1 = new HColumnDescriptor("data1");
                htd.addFamily(hcd1);
                HColumnDescriptor hcd2 = new HColumnDescriptor("data2");
                htd.addFamily(hcd2);
                HColumnDescriptor hcd3 = new HColumnDescriptor("data3");
                htd.addFamily(hcd3);
                admin.createTable(htd);
            }

            HTable table = new HTable(config, tableName);

            table.setAutoFlush(false);
            int count = 50;
            for (int i = 1; i &lt;= count; ++i) {
                Put p = new Put(String.format("row%03d", i).getBytes());
                p.add("data1".getBytes(), String.format("col%01d", i % 10)
                        .getBytes(), String.format("data1%03d", i).getBytes());
                p.add("data2".getBytes(), String.format("col%01d", i % 10)
                        .getBytes(), String.format("data2%03d", i).getBytes());
                p.add("data3".getBytes(), String.format("col%01d", i % 10)
                        .getBytes(), String.format("data3%03d", i).getBytes());
                table.put(p);
            }
            table.close();

        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    /**
     * @param args
     * @throws IOException
     */
    public static void main(String[] args) throws IOException {
        TestHbaseDependentColumnFilter test = new TestHbaseDependentColumnFilter();
        test.init();
        test.testFilter();
    }

}
</pre>