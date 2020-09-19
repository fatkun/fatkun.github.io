---
title: Hbase QualifierFilter
author: fatkun
type: post
date: 2013-03-25T16:40:53+00:00
url: /2013/03/hbase-qualifierfilter.html
duoshuo_thread_id:
  - 6300410014485971713
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:23476:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">package</span> <span style="color: #006699;">com.fatkun.filter.comparison</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">java.io.IOException</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.conf.Configuration</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.HBaseConfiguration</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.HColumnDescriptor</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.HTableDescriptor</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.client.Get</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.client.HBaseAdmin</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.client.HTable</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.client.Put</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.client.Result</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.client.ResultScanner</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.client.Scan</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.filter.BinaryComparator</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.filter.CompareFilter</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.filter.FamilyFilter</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.filter.Filter</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.filter.QualifierFilter</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.util.Bytes</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> TestHbaseQualifierFilter <span style="color: #009900;">&#123;</span>
    	<span style="color: #003399;">String</span> tableName <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;test_qualifier_filter&quot;</span><span style="color: #339933;">;</span>
    	Configuration config <span style="color: #339933;">=</span> HBaseConfiguration.<span style="color: #006633;">create</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
    	<span style="color: #008000; font-style: italic; font-weight: bold;">/**
    	 * 部分代码来自hbase权威指南
    	 * @throws IOException
    	 */</span>
    	<span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> testRowFilter<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">throws</span> <span style="color: #003399;">IOException</span> <span style="color: #009900;">&#123;</span>
    &nbsp;
    		HTable table <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> HTable<span style="color: #009900;">&#40;</span>config, tableName<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		Scan scan <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> Scan<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;只列出小于col5的列&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		Filter filter1 <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> QualifierFilter<span style="color: #009900;">&#40;</span>CompareFilter.<span style="color: #006633;">CompareOp</span>.<span style="color: #006633;">LESS</span>, 
    			      <span style="color: #000000; font-weight: bold;">new</span> BinaryComparator<span style="color: #009900;">&#40;</span>Bytes.<span style="color: #006633;">toBytes</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;col5&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		scan.<span style="color: #006633;">setFilter</span><span style="color: #009900;">&#40;</span>filter1<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		ResultScanner scanner1 <span style="color: #339933;">=</span> table.<span style="color: #006633;">getScanner</span><span style="color: #009900;">&#40;</span>scan<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span>Result res <span style="color: #339933;">:</span> scanner1<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    			<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>res<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #009900;">&#125;</span>
    		scanner1.<span style="color: #006633;">close</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;get也可以设置filter&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		Get get1 <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> Get<span style="color: #009900;">&#40;</span>Bytes.<span style="color: #006633;">toBytes</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;row003&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	    get1.<span style="color: #006633;">setFilter</span><span style="color: #009900;">&#40;</span>filter1<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	    Result result1 <span style="color: #339933;">=</span> table.<span style="color: #006633;">get</span><span style="color: #009900;">&#40;</span>get1<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> 
    	    <span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Result of get(): &quot;</span> <span style="color: #339933;">+</span> result1<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
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
    		TestHbaseQualifierFilter test <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> TestHbaseQualifierFilter<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		test.<span style="color: #006633;">init</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		test.<span style="color: #006633;">testRowFilter</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">package com.fatkun.filter.comparison;
    import java.io.IOException;
    
    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.HColumnDescriptor;
    import org.apache.hadoop.hbase.HTableDescriptor;
    import org.apache.hadoop.hbase.client.Get;
    import org.apache.hadoop.hbase.client.HBaseAdmin;
    import org.apache.hadoop.hbase.client.HTable;
    import org.apache.hadoop.hbase.client.Put;
    import org.apache.hadoop.hbase.client.Result;
    import org.apache.hadoop.hbase.client.ResultScanner;
    import org.apache.hadoop.hbase.client.Scan;
    import org.apache.hadoop.hbase.filter.BinaryComparator;
    import org.apache.hadoop.hbase.filter.CompareFilter;
    import org.apache.hadoop.hbase.filter.FamilyFilter;
    import org.apache.hadoop.hbase.filter.Filter;
    import org.apache.hadoop.hbase.filter.QualifierFilter;
    import org.apache.hadoop.hbase.util.Bytes;
    
    public class TestHbaseQualifierFilter {
    	String tableName = &quot;test_qualifier_filter&quot;;
    	Configuration config = HBaseConfiguration.create();
    
    	/**
    	 * 部分代码来自hbase权威指南
    	 * @throws IOException
    	 */
    	public void testRowFilter() throws IOException {
    		
    		HTable table = new HTable(config, tableName);
    		Scan scan = new Scan();
    		
    		System.out.println(&quot;只列出小于col5的列&quot;);
    		Filter filter1 = new QualifierFilter(CompareFilter.CompareOp.LESS, 
    			      new BinaryComparator(Bytes.toBytes(&quot;col5&quot;)));
    		scan.setFilter(filter1);
    		ResultScanner scanner1 = table.getScanner(scan);
    		for (Result res : scanner1) {
    			System.out.println(res);
    		}
    		scanner1.close();
    		
    		System.out.println(&quot;get也可以设置filter&quot;);
    		Get get1 = new Get(Bytes.toBytes(&quot;row003&quot;));
    	    get1.setFilter(filter1);
    	    Result result1 = table.get(get1); 
    	    System.out.println(&quot;Result of get(): &quot; + result1);
    
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
    		TestHbaseQualifierFilter test = new TestHbaseQualifierFilter();
    		test.init();
    		test.testRowFilter();
    	}
    
    }</p></div>
    ";}
categories:
  - hbase
tags:
  - filter
  - hbase

---
Hbase QualifierFilter用于过滤qualifier，也就是一个列族里面data:xxx，冒号后面的字符串。 =。=
<pre escaped="true" lang="java">package com.fatkun.filter.comparison;
import java.io.IOException;

import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.hbase.HBaseConfiguration;
import org.apache.hadoop.hbase.HColumnDescriptor;
import org.apache.hadoop.hbase.HTableDescriptor;
import org.apache.hadoop.hbase.client.Get;
import org.apache.hadoop.hbase.client.HBaseAdmin;
import org.apache.hadoop.hbase.client.HTable;
import org.apache.hadoop.hbase.client.Put;
import org.apache.hadoop.hbase.client.Result;
import org.apache.hadoop.hbase.client.ResultScanner;
import org.apache.hadoop.hbase.client.Scan;
import org.apache.hadoop.hbase.filter.BinaryComparator;
import org.apache.hadoop.hbase.filter.CompareFilter;
import org.apache.hadoop.hbase.filter.FamilyFilter;
import org.apache.hadoop.hbase.filter.Filter;
import org.apache.hadoop.hbase.filter.QualifierFilter;
import org.apache.hadoop.hbase.util.Bytes;

public class TestHbaseQualifierFilter {
	String tableName = "test_qualifier_filter";
	Configuration config = HBaseConfiguration.create();

	/**
	 * 部分代码来自hbase权威指南
	 * @throws IOException
	 */
	public void testRowFilter() throws IOException {
		
		HTable table = new HTable(config, tableName);
		Scan scan = new Scan();
		
		System.out.println("只列出小于col5的列");
		Filter filter1 = new QualifierFilter(CompareFilter.CompareOp.LESS, 
			      new BinaryComparator(Bytes.toBytes("col5")));
		scan.setFilter(filter1);
		ResultScanner scanner1 = table.getScanner(scan);
		for (Result res : scanner1) {
			System.out.println(res);
		}
		scanner1.close();
		
		System.out.println("get也可以设置filter");
		Get get1 = new Get(Bytes.toBytes("row003"));
	    get1.setFilter(filter1);
	    Result result1 = table.get(get1); 
	    System.out.println("Result of get(): " + result1);

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
		TestHbaseQualifierFilter test = new TestHbaseQualifierFilter();
		test.init();
		test.testRowFilter();
	}

}

</pre>