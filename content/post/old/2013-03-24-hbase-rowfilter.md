---
title: hbase RowFilter
author: fatkun
type: post
date: 2013-03-24T13:58:40+00:00
url: /2013/03/hbase-rowfilter.html
duoshuo_thread_id:
  - 6300410014129455873
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:26881:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">java.io.IOException</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.conf.Configuration</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.HBaseConfiguration</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.HColumnDescriptor</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.HTableDescriptor</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.client.HBaseAdmin</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.client.HTable</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.client.Put</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.client.Result</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.client.ResultScanner</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.client.Scan</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.filter.BinaryComparator</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.filter.BinaryPrefixComparator</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.filter.CompareFilter</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.filter.Filter</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.filter.RegexStringComparator</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.filter.RowFilter</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.hbase.filter.SubstringComparator</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> TestHbaseRowFilter <span style="color: #009900;">&#123;</span>
    	<span style="color: #003399;">String</span> tableName <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;test_row_filter&quot;</span><span style="color: #339933;">;</span>
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
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;小于等于row010的行&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		Filter filter1 <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> RowFilter<span style="color: #009900;">&#40;</span>CompareFilter.<span style="color: #006633;">CompareOp</span>.<span style="color: #006633;">LESS_OR_EQUAL</span>,
    				<span style="color: #000000; font-weight: bold;">new</span> BinaryComparator<span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;row010&quot;</span>.<span style="color: #006633;">getBytes</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		scan.<span style="color: #006633;">setFilter</span><span style="color: #009900;">&#40;</span>filter1<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		ResultScanner scanner1 <span style="color: #339933;">=</span> table.<span style="color: #006633;">getScanner</span><span style="color: #009900;">&#40;</span>scan<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span>Result res <span style="color: #339933;">:</span> scanner1<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    			<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>res<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #009900;">&#125;</span>
    		scanner1.<span style="color: #006633;">close</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;正则获取结尾为5的行&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		Filter filter2 <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> RowFilter<span style="color: #009900;">&#40;</span>CompareFilter.<span style="color: #006633;">CompareOp</span>.<span style="color: #006633;">EQUAL</span>,
    				<span style="color: #000000; font-weight: bold;">new</span> RegexStringComparator<span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;.*5$&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		scan.<span style="color: #006633;">setFilter</span><span style="color: #009900;">&#40;</span>filter2<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		ResultScanner scanner2 <span style="color: #339933;">=</span> table.<span style="color: #006633;">getScanner</span><span style="color: #009900;">&#40;</span>scan<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span>Result res <span style="color: #339933;">:</span> scanner2<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    			<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>res<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #009900;">&#125;</span>
    		scanner2.<span style="color: #006633;">close</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;包行有5的行&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		Filter filter3 <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> RowFilter<span style="color: #009900;">&#40;</span>CompareFilter.<span style="color: #006633;">CompareOp</span>.<span style="color: #006633;">EQUAL</span>,
    				<span style="color: #000000; font-weight: bold;">new</span> SubstringComparator<span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;5&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		scan.<span style="color: #006633;">setFilter</span><span style="color: #009900;">&#40;</span>filter3<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		ResultScanner scanner3 <span style="color: #339933;">=</span> table.<span style="color: #006633;">getScanner</span><span style="color: #009900;">&#40;</span>scan<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span>Result res <span style="color: #339933;">:</span> scanner3<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    			<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>res<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #009900;">&#125;</span>
    		scanner3.<span style="color: #006633;">close</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;开头是row01的&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		Filter filter4 <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> RowFilter<span style="color: #009900;">&#40;</span>CompareFilter.<span style="color: #006633;">CompareOp</span>.<span style="color: #006633;">EQUAL</span>,
    				<span style="color: #000000; font-weight: bold;">new</span> BinaryPrefixComparator<span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;row01&quot;</span>.<span style="color: #006633;">getBytes</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		scan.<span style="color: #006633;">setFilter</span><span style="color: #009900;">&#40;</span>filter4<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		ResultScanner scanner4 <span style="color: #339933;">=</span> table.<span style="color: #006633;">getScanner</span><span style="color: #009900;">&#40;</span>scan<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span>Result res <span style="color: #339933;">:</span> scanner4<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    			<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>res<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #009900;">&#125;</span>
    		scanner3.<span style="color: #006633;">close</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
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
    				HColumnDescriptor hcd1 <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> HColumnDescriptor<span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;data&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    				htd.<span style="color: #006633;">addFamily</span><span style="color: #009900;">&#40;</span>hcd1<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    				HColumnDescriptor hcd2 <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> HColumnDescriptor<span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;url&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    				htd.<span style="color: #006633;">addFamily</span><span style="color: #009900;">&#40;</span>hcd2<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
    				admin.<span style="color: #006633;">createTable</span><span style="color: #009900;">&#40;</span>htd<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    			<span style="color: #009900;">&#125;</span>
    &nbsp;
    			HTable table <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> HTable<span style="color: #009900;">&#40;</span>config, tableName<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
    			table.<span style="color: #006633;">setAutoFlush</span><span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">false</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    			<span style="color: #000066; font-weight: bold;">int</span> count <span style="color: #339933;">=</span> <span style="color: #cc66cc;">50</span><span style="color: #339933;">;</span>
    			<span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> i <span style="color: #339933;">=</span> <span style="color: #cc66cc;">1</span><span style="color: #339933;">;</span> i <span style="color: #339933;">&lt;=</span> count<span style="color: #339933;">;</span> <span style="color: #339933;">++</span>i<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    				Put p <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> Put<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span>.<span style="color: #006633;">format</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;row%03d&quot;</span>, i<span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getBytes</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    				p.<span style="color: #006633;">add</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;data&quot;</span>.<span style="color: #006633;">getBytes</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, <span style="color: #003399;">String</span>.<span style="color: #006633;">format</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;col%01d&quot;</span>, i <span style="color: #339933;">%</span> <span style="color: #cc66cc;">10</span><span style="color: #009900;">&#41;</span>
    						.<span style="color: #006633;">getBytes</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, <span style="color: #003399;">String</span>.<span style="color: #006633;">format</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;data%03d&quot;</span>, i<span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getBytes</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    				p.<span style="color: #006633;">add</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;url&quot;</span>.<span style="color: #006633;">getBytes</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, <span style="color: #003399;">String</span>.<span style="color: #006633;">format</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;col%01d&quot;</span>, i <span style="color: #339933;">%</span> <span style="color: #cc66cc;">10</span><span style="color: #009900;">&#41;</span>
    						.<span style="color: #006633;">getBytes</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, <span style="color: #003399;">String</span>.<span style="color: #006633;">format</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;url%03d&quot;</span>, i<span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getBytes</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
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
    		TestHbaseRowFilter test <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> TestHbaseRowFilter<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		test.<span style="color: #006633;">init</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		test.<span style="color: #006633;">testRowFilter</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    	<span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">import java.io.IOException;
    
    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.HColumnDescriptor;
    import org.apache.hadoop.hbase.HTableDescriptor;
    import org.apache.hadoop.hbase.client.HBaseAdmin;
    import org.apache.hadoop.hbase.client.HTable;
    import org.apache.hadoop.hbase.client.Put;
    import org.apache.hadoop.hbase.client.Result;
    import org.apache.hadoop.hbase.client.ResultScanner;
    import org.apache.hadoop.hbase.client.Scan;
    import org.apache.hadoop.hbase.filter.BinaryComparator;
    import org.apache.hadoop.hbase.filter.BinaryPrefixComparator;
    import org.apache.hadoop.hbase.filter.CompareFilter;
    import org.apache.hadoop.hbase.filter.Filter;
    import org.apache.hadoop.hbase.filter.RegexStringComparator;
    import org.apache.hadoop.hbase.filter.RowFilter;
    import org.apache.hadoop.hbase.filter.SubstringComparator;
    
    public class TestHbaseRowFilter {
    	String tableName = &quot;test_row_filter&quot;;
    	Configuration config = HBaseConfiguration.create();
    
    	/**
    	 * 部分代码来自hbase权威指南
    	 * @throws IOException
    	 */
    	public void testRowFilter() throws IOException {
    
    		HTable table = new HTable(config, tableName);
    		Scan scan = new Scan();
    
    		System.out.println(&quot;小于等于row010的行&quot;);
    		Filter filter1 = new RowFilter(CompareFilter.CompareOp.LESS_OR_EQUAL,
    				new BinaryComparator(&quot;row010&quot;.getBytes()));
    		scan.setFilter(filter1);
    		ResultScanner scanner1 = table.getScanner(scan);
    		for (Result res : scanner1) {
    			System.out.println(res);
    		}
    		scanner1.close();
    
    		System.out.println(&quot;正则获取结尾为5的行&quot;);
    		Filter filter2 = new RowFilter(CompareFilter.CompareOp.EQUAL,
    				new RegexStringComparator(&quot;.*5$&quot;));
    		scan.setFilter(filter2);
    		ResultScanner scanner2 = table.getScanner(scan);
    		for (Result res : scanner2) {
    			System.out.println(res);
    		}
    		scanner2.close();
    
    		System.out.println(&quot;包行有5的行&quot;);
    		Filter filter3 = new RowFilter(CompareFilter.CompareOp.EQUAL,
    				new SubstringComparator(&quot;5&quot;));
    		scan.setFilter(filter3);
    		ResultScanner scanner3 = table.getScanner(scan);
    		for (Result res : scanner3) {
    			System.out.println(res);
    		}
    		scanner3.close();
    
    		System.out.println(&quot;开头是row01的&quot;);
    		Filter filter4 = new RowFilter(CompareFilter.CompareOp.EQUAL,
    				new BinaryPrefixComparator(&quot;row01&quot;.getBytes()));
    		scan.setFilter(filter4);
    		ResultScanner scanner4 = table.getScanner(scan);
    		for (Result res : scanner4) {
    			System.out.println(res);
    		}
    		scanner3.close();
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
    				HColumnDescriptor hcd1 = new HColumnDescriptor(&quot;data&quot;);
    				htd.addFamily(hcd1);
    				HColumnDescriptor hcd2 = new HColumnDescriptor(&quot;url&quot;);
    				htd.addFamily(hcd2);
    
    				admin.createTable(htd);
    			}
    
    			HTable table = new HTable(config, tableName);
    
    			table.setAutoFlush(false);
    			int count = 50;
    			for (int i = 1; i &lt;= count; ++i) {
    				Put p = new Put(String.format(&quot;row%03d&quot;, i).getBytes());
    				p.add(&quot;data&quot;.getBytes(), String.format(&quot;col%01d&quot;, i % 10)
    						.getBytes(), String.format(&quot;data%03d&quot;, i).getBytes());
    				p.add(&quot;url&quot;.getBytes(), String.format(&quot;col%01d&quot;, i % 10)
    						.getBytes(), String.format(&quot;url%03d&quot;, i).getBytes());
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
    		TestHbaseRowFilter test = new TestHbaseRowFilter();
    		test.init();
    		test.testRowFilter();
    	}
    
    }</p></div>
    ";i:2;s:6401:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="other" style="font-family:monospace;">小于等于row010的行
    keyvalues={row001/data:col1/1364133382268/Put/vlen=7, row001/url:col1/1364133382268/Put/vlen=6}
    keyvalues={row002/data:col2/1364133382268/Put/vlen=7, row002/url:col2/1364133382268/Put/vlen=6}
    keyvalues={row003/data:col3/1364133382268/Put/vlen=7, row003/url:col3/1364133382268/Put/vlen=6}
    keyvalues={row004/data:col4/1364133382268/Put/vlen=7, row004/url:col4/1364133382268/Put/vlen=6}
    keyvalues={row005/data:col5/1364133382268/Put/vlen=7, row005/url:col5/1364133382268/Put/vlen=6}
    keyvalues={row006/data:col6/1364133382268/Put/vlen=7, row006/url:col6/1364133382268/Put/vlen=6}
    keyvalues={row007/data:col7/1364133382268/Put/vlen=7, row007/url:col7/1364133382268/Put/vlen=6}
    keyvalues={row008/data:col8/1364133382268/Put/vlen=7, row008/url:col8/1364133382268/Put/vlen=6}
    keyvalues={row009/data:col9/1364133382268/Put/vlen=7, row009/url:col9/1364133382268/Put/vlen=6}
    keyvalues={row010/data:col0/1364133382268/Put/vlen=7, row010/url:col0/1364133382268/Put/vlen=6}
    正则获取结尾为5的行
    keyvalues={row005/data:col5/1364133382268/Put/vlen=7, row005/url:col5/1364133382268/Put/vlen=6}
    keyvalues={row015/data:col5/1364133382268/Put/vlen=7, row015/url:col5/1364133382268/Put/vlen=6}
    keyvalues={row025/data:col5/1364133382268/Put/vlen=7, row025/url:col5/1364133382268/Put/vlen=6}
    keyvalues={row035/data:col5/1364133382268/Put/vlen=7, row035/url:col5/1364133382268/Put/vlen=6}
    keyvalues={row045/data:col5/1364133382268/Put/vlen=7, row045/url:col5/1364133382268/Put/vlen=6}
    包行有5的行
    keyvalues={row005/data:col5/1364133382268/Put/vlen=7, row005/url:col5/1364133382268/Put/vlen=6}
    keyvalues={row015/data:col5/1364133382268/Put/vlen=7, row015/url:col5/1364133382268/Put/vlen=6}
    keyvalues={row025/data:col5/1364133382268/Put/vlen=7, row025/url:col5/1364133382268/Put/vlen=6}
    keyvalues={row035/data:col5/1364133382268/Put/vlen=7, row035/url:col5/1364133382268/Put/vlen=6}
    keyvalues={row045/data:col5/1364133382268/Put/vlen=7, row045/url:col5/1364133382268/Put/vlen=6}
    keyvalues={row050/data:col0/1364133382268/Put/vlen=7, row050/url:col0/1364133382268/Put/vlen=6}
    开头是row01的
    keyvalues={row010/data:col0/1364133382268/Put/vlen=7, row010/url:col0/1364133382268/Put/vlen=6}
    keyvalues={row011/data:col1/1364133382268/Put/vlen=7, row011/url:col1/1364133382268/Put/vlen=6}
    keyvalues={row012/data:col2/1364133382268/Put/vlen=7, row012/url:col2/1364133382268/Put/vlen=6}
    keyvalues={row013/data:col3/1364133382268/Put/vlen=7, row013/url:col3/1364133382268/Put/vlen=6}
    keyvalues={row014/data:col4/1364133382268/Put/vlen=7, row014/url:col4/1364133382268/Put/vlen=6}
    keyvalues={row015/data:col5/1364133382268/Put/vlen=7, row015/url:col5/1364133382268/Put/vlen=6}
    keyvalues={row016/data:col6/1364133382268/Put/vlen=7, row016/url:col6/1364133382268/Put/vlen=6}
    keyvalues={row017/data:col7/1364133382268/Put/vlen=7, row017/url:col7/1364133382268/Put/vlen=6}
    keyvalues={row018/data:col8/1364133382268/Put/vlen=7, row018/url:col8/1364133382268/Put/vlen=6}
    keyvalues={row019/data:col9/1364133382268/Put/vlen=7, row019/url:col9/1364133382268/Put/vlen=6}</pre></td></tr></table><p class="theCode" style="display:none;">小于等于row010的行
    keyvalues={row001/data:col1/1364133382268/Put/vlen=7, row001/url:col1/1364133382268/Put/vlen=6}
    keyvalues={row002/data:col2/1364133382268/Put/vlen=7, row002/url:col2/1364133382268/Put/vlen=6}
    keyvalues={row003/data:col3/1364133382268/Put/vlen=7, row003/url:col3/1364133382268/Put/vlen=6}
    keyvalues={row004/data:col4/1364133382268/Put/vlen=7, row004/url:col4/1364133382268/Put/vlen=6}
    keyvalues={row005/data:col5/1364133382268/Put/vlen=7, row005/url:col5/1364133382268/Put/vlen=6}
    keyvalues={row006/data:col6/1364133382268/Put/vlen=7, row006/url:col6/1364133382268/Put/vlen=6}
    keyvalues={row007/data:col7/1364133382268/Put/vlen=7, row007/url:col7/1364133382268/Put/vlen=6}
    keyvalues={row008/data:col8/1364133382268/Put/vlen=7, row008/url:col8/1364133382268/Put/vlen=6}
    keyvalues={row009/data:col9/1364133382268/Put/vlen=7, row009/url:col9/1364133382268/Put/vlen=6}
    keyvalues={row010/data:col0/1364133382268/Put/vlen=7, row010/url:col0/1364133382268/Put/vlen=6}
    正则获取结尾为5的行
    keyvalues={row005/data:col5/1364133382268/Put/vlen=7, row005/url:col5/1364133382268/Put/vlen=6}
    keyvalues={row015/data:col5/1364133382268/Put/vlen=7, row015/url:col5/1364133382268/Put/vlen=6}
    keyvalues={row025/data:col5/1364133382268/Put/vlen=7, row025/url:col5/1364133382268/Put/vlen=6}
    keyvalues={row035/data:col5/1364133382268/Put/vlen=7, row035/url:col5/1364133382268/Put/vlen=6}
    keyvalues={row045/data:col5/1364133382268/Put/vlen=7, row045/url:col5/1364133382268/Put/vlen=6}
    包行有5的行
    keyvalues={row005/data:col5/1364133382268/Put/vlen=7, row005/url:col5/1364133382268/Put/vlen=6}
    keyvalues={row015/data:col5/1364133382268/Put/vlen=7, row015/url:col5/1364133382268/Put/vlen=6}
    keyvalues={row025/data:col5/1364133382268/Put/vlen=7, row025/url:col5/1364133382268/Put/vlen=6}
    keyvalues={row035/data:col5/1364133382268/Put/vlen=7, row035/url:col5/1364133382268/Put/vlen=6}
    keyvalues={row045/data:col5/1364133382268/Put/vlen=7, row045/url:col5/1364133382268/Put/vlen=6}
    keyvalues={row050/data:col0/1364133382268/Put/vlen=7, row050/url:col0/1364133382268/Put/vlen=6}
    开头是row01的
    keyvalues={row010/data:col0/1364133382268/Put/vlen=7, row010/url:col0/1364133382268/Put/vlen=6}
    keyvalues={row011/data:col1/1364133382268/Put/vlen=7, row011/url:col1/1364133382268/Put/vlen=6}
    keyvalues={row012/data:col2/1364133382268/Put/vlen=7, row012/url:col2/1364133382268/Put/vlen=6}
    keyvalues={row013/data:col3/1364133382268/Put/vlen=7, row013/url:col3/1364133382268/Put/vlen=6}
    keyvalues={row014/data:col4/1364133382268/Put/vlen=7, row014/url:col4/1364133382268/Put/vlen=6}
    keyvalues={row015/data:col5/1364133382268/Put/vlen=7, row015/url:col5/1364133382268/Put/vlen=6}
    keyvalues={row016/data:col6/1364133382268/Put/vlen=7, row016/url:col6/1364133382268/Put/vlen=6}
    keyvalues={row017/data:col7/1364133382268/Put/vlen=7, row017/url:col7/1364133382268/Put/vlen=6}
    keyvalues={row018/data:col8/1364133382268/Put/vlen=7, row018/url:col8/1364133382268/Put/vlen=6}
    keyvalues={row019/data:col9/1364133382268/Put/vlen=7, row019/url:col9/1364133382268/Put/vlen=6}</p></div>
    ";}
categories:
  - hbase
tags:
  - filter
  - hbase

---
RowFilter用于过滤row key
<table summary="The possible comparison operators for CompareFilter-based           filters">  <tr>    <th>      Operator    </th>
    <th>      Description    </th>  </tr>
  <tr>    <td>      <code>LESS</code>    </td>
    <td>      小于    </td>  </tr>
  <tr>    <td>      <code>LESS_OR_EQUAL</code>    </td>
    <td>      小于等于    </td>  </tr>
  <tr>    <td>      <code>EQUAL</code>    </td>
    <td>      等于    </td>  </tr>
  <tr>    <td>      <code>NOT_EQUAL</code>    </td>
    <td>      不等于    </td>  </tr>
  <tr>    <td>      <code>GREATER_OR_EQUAL</code>    </td>
    <td>      大于等于    </td>  </tr>
  <tr>    <td>      <code>GREATER</code>    </td>
    <td>      大于    </td>  </tr>
  <tr>    <td>      <code>NO_OP</code>    </td>
    <td>      排除所有    </td>  </tr></table>
&nbsp;
<table summary="The HBase-supplied comparators, used with CompareFilter-based           filters">  <tr>    <th>      Comparator    </th>
    <th>      Description    </th>  </tr>
  <tr>    <td>      <code>BinaryComparator</code>    </td>
    <td>      使用Bytes.compareTo()比较    </td>  </tr>
  <tr>    <td>      <code>BinaryPrefixComparator</code>    </td>
    <td>      和BinaryComparator差不多，从前面开始比较    </td>  </tr>
  <tr>    <td>      <code>NullComparator</code>    </td>
    <td>      Does<a id="I_indexterm4_d1e13563"></a> not compare against an actual value but whether a given one is <code>null</code>, or not <code>null</code>.    </td>  </tr>
  <tr>    <td>      <code>BitComparator</code>    </td>
    <td>      Performs<a id="I_indexterm4_d1e13579"></a> a bitwise comparison, providing a <code>BitwiseOp</code> class with <code>AND</code>, <code>OR</code>, and <code>XOR</code> operators.    </td>  </tr>
  <tr>    <td>      <code>RegexStringComparator</code>    </td>
    <td>      正则表达式    </td>  </tr>
  <tr>    <td>      <code>SubstringComparator</code>    </td>
    <td>      把数据当成字符串，用contains()来判断    </td>  </tr></table>
&nbsp;
&nbsp;
<pre lang="java" escaped="true">import java.io.IOException;

import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.hbase.HBaseConfiguration;
import org.apache.hadoop.hbase.HColumnDescriptor;
import org.apache.hadoop.hbase.HTableDescriptor;
import org.apache.hadoop.hbase.client.HBaseAdmin;
import org.apache.hadoop.hbase.client.HTable;
import org.apache.hadoop.hbase.client.Put;
import org.apache.hadoop.hbase.client.Result;
import org.apache.hadoop.hbase.client.ResultScanner;
import org.apache.hadoop.hbase.client.Scan;
import org.apache.hadoop.hbase.filter.BinaryComparator;
import org.apache.hadoop.hbase.filter.BinaryPrefixComparator;
import org.apache.hadoop.hbase.filter.CompareFilter;
import org.apache.hadoop.hbase.filter.Filter;
import org.apache.hadoop.hbase.filter.RegexStringComparator;
import org.apache.hadoop.hbase.filter.RowFilter;
import org.apache.hadoop.hbase.filter.SubstringComparator;

public class TestHbaseRowFilter {
	String tableName = "test_row_filter";
	Configuration config = HBaseConfiguration.create();

	/**
	 * 部分代码来自hbase权威指南
	 * @throws IOException
	 */
	public void testRowFilter() throws IOException {

		HTable table = new HTable(config, tableName);
		Scan scan = new Scan();

		System.out.println("小于等于row010的行");
		Filter filter1 = new RowFilter(CompareFilter.CompareOp.LESS_OR_EQUAL,
				new BinaryComparator("row010".getBytes()));
		scan.setFilter(filter1);
		ResultScanner scanner1 = table.getScanner(scan);
		for (Result res : scanner1) {
			System.out.println(res);
		}
		scanner1.close();

		System.out.println("正则获取结尾为5的行");
		Filter filter2 = new RowFilter(CompareFilter.CompareOp.EQUAL,
				new RegexStringComparator(".*5$"));
		scan.setFilter(filter2);
		ResultScanner scanner2 = table.getScanner(scan);
		for (Result res : scanner2) {
			System.out.println(res);
		}
		scanner2.close();

		System.out.println("包行有5的行");
		Filter filter3 = new RowFilter(CompareFilter.CompareOp.EQUAL,
				new SubstringComparator("5"));
		scan.setFilter(filter3);
		ResultScanner scanner3 = table.getScanner(scan);
		for (Result res : scanner3) {
			System.out.println(res);
		}
		scanner3.close();

		System.out.println("开头是row01的");
		Filter filter4 = new RowFilter(CompareFilter.CompareOp.EQUAL,
				new BinaryPrefixComparator("row01".getBytes()));
		scan.setFilter(filter4);
		ResultScanner scanner4 = table.getScanner(scan);
		for (Result res : scanner4) {
			System.out.println(res);
		}
		scanner3.close();
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
				HColumnDescriptor hcd1 = new HColumnDescriptor("data");
				htd.addFamily(hcd1);
				HColumnDescriptor hcd2 = new HColumnDescriptor("url");
				htd.addFamily(hcd2);

				admin.createTable(htd);
			}

			HTable table = new HTable(config, tableName);

			table.setAutoFlush(false);
			int count = 50;
			for (int i = 1; i &lt;= count; ++i) {
				Put p = new Put(String.format("row%03d", i).getBytes());
				p.add("data".getBytes(), String.format("col%01d", i % 10)
						.getBytes(), String.format("data%03d", i).getBytes());
				p.add("url".getBytes(), String.format("col%01d", i % 10)
						.getBytes(), String.format("url%03d", i).getBytes());
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
		TestHbaseRowFilter test = new TestHbaseRowFilter();
		test.init();
		test.testRowFilter();
	}

}</pre>
## 输出结果

<pre escaped="true" lang="other">小于等于row010的行
keyvalues={row001/data:col1/1364133382268/Put/vlen=7, row001/url:col1/1364133382268/Put/vlen=6}
keyvalues={row002/data:col2/1364133382268/Put/vlen=7, row002/url:col2/1364133382268/Put/vlen=6}
keyvalues={row003/data:col3/1364133382268/Put/vlen=7, row003/url:col3/1364133382268/Put/vlen=6}
keyvalues={row004/data:col4/1364133382268/Put/vlen=7, row004/url:col4/1364133382268/Put/vlen=6}
keyvalues={row005/data:col5/1364133382268/Put/vlen=7, row005/url:col5/1364133382268/Put/vlen=6}
keyvalues={row006/data:col6/1364133382268/Put/vlen=7, row006/url:col6/1364133382268/Put/vlen=6}
keyvalues={row007/data:col7/1364133382268/Put/vlen=7, row007/url:col7/1364133382268/Put/vlen=6}
keyvalues={row008/data:col8/1364133382268/Put/vlen=7, row008/url:col8/1364133382268/Put/vlen=6}
keyvalues={row009/data:col9/1364133382268/Put/vlen=7, row009/url:col9/1364133382268/Put/vlen=6}
keyvalues={row010/data:col0/1364133382268/Put/vlen=7, row010/url:col0/1364133382268/Put/vlen=6}
正则获取结尾为5的行
keyvalues={row005/data:col5/1364133382268/Put/vlen=7, row005/url:col5/1364133382268/Put/vlen=6}
keyvalues={row015/data:col5/1364133382268/Put/vlen=7, row015/url:col5/1364133382268/Put/vlen=6}
keyvalues={row025/data:col5/1364133382268/Put/vlen=7, row025/url:col5/1364133382268/Put/vlen=6}
keyvalues={row035/data:col5/1364133382268/Put/vlen=7, row035/url:col5/1364133382268/Put/vlen=6}
keyvalues={row045/data:col5/1364133382268/Put/vlen=7, row045/url:col5/1364133382268/Put/vlen=6}
包行有5的行
keyvalues={row005/data:col5/1364133382268/Put/vlen=7, row005/url:col5/1364133382268/Put/vlen=6}
keyvalues={row015/data:col5/1364133382268/Put/vlen=7, row015/url:col5/1364133382268/Put/vlen=6}
keyvalues={row025/data:col5/1364133382268/Put/vlen=7, row025/url:col5/1364133382268/Put/vlen=6}
keyvalues={row035/data:col5/1364133382268/Put/vlen=7, row035/url:col5/1364133382268/Put/vlen=6}
keyvalues={row045/data:col5/1364133382268/Put/vlen=7, row045/url:col5/1364133382268/Put/vlen=6}
keyvalues={row050/data:col0/1364133382268/Put/vlen=7, row050/url:col0/1364133382268/Put/vlen=6}
开头是row01的
keyvalues={row010/data:col0/1364133382268/Put/vlen=7, row010/url:col0/1364133382268/Put/vlen=6}
keyvalues={row011/data:col1/1364133382268/Put/vlen=7, row011/url:col1/1364133382268/Put/vlen=6}
keyvalues={row012/data:col2/1364133382268/Put/vlen=7, row012/url:col2/1364133382268/Put/vlen=6}
keyvalues={row013/data:col3/1364133382268/Put/vlen=7, row013/url:col3/1364133382268/Put/vlen=6}
keyvalues={row014/data:col4/1364133382268/Put/vlen=7, row014/url:col4/1364133382268/Put/vlen=6}
keyvalues={row015/data:col5/1364133382268/Put/vlen=7, row015/url:col5/1364133382268/Put/vlen=6}
keyvalues={row016/data:col6/1364133382268/Put/vlen=7, row016/url:col6/1364133382268/Put/vlen=6}
keyvalues={row017/data:col7/1364133382268/Put/vlen=7, row017/url:col7/1364133382268/Put/vlen=6}
keyvalues={row018/data:col8/1364133382268/Put/vlen=7, row018/url:col8/1364133382268/Put/vlen=6}
keyvalues={row019/data:col9/1364133382268/Put/vlen=7, row019/url:col9/1364133382268/Put/vlen=6}</pre>
## 参考

hbase权威指南