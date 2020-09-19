---
title: hadoop wordcount新API例子
author: fatkun
type: post
date: 2013-10-27T16:26:48+00:00
url: /2013/10/hadoop-wordcount-new-api.html
duoshuo_thread_id:
  - 6300410041925108481
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:26077:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">package</span> <span style="color: #006699;">com.fatkun</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">java.io.IOException</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">java.util.ArrayList</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">java.util.List</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">java.util.StringTokenizer</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.commons.logging.Log</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.commons.logging.LogFactory</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.conf.Configuration</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.conf.Configured</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.fs.Path</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.io.IntWritable</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.io.LongWritable</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.io.Text</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.mapreduce.Job</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.mapreduce.Mapper</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.mapreduce.Reducer</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.mapreduce.lib.input.FileInputFormat</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.mapreduce.lib.output.FileOutputFormat</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.util.Tool</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">org.apache.hadoop.util.ToolRunner</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> WordCount <span style="color: #000000; font-weight: bold;">extends</span> Configured <span style="color: #000000; font-weight: bold;">implements</span> Tool <span style="color: #009900;">&#123;</span>
        <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000000; font-weight: bold;">enum</span> Counters <span style="color: #009900;">&#123;</span>
            INPUT_WORDS <span style="color: #666666; font-style: italic;">// 计数器</span>
        <span style="color: #009900;">&#125;</span> 
    &nbsp;
        <span style="color: #000000; font-weight: bold;">static</span> Log logger <span style="color: #339933;">=</span> LogFactory.<span style="color: #006633;">getLog</span><span style="color: #009900;">&#40;</span>WordCount.<span style="color: #000000; font-weight: bold;">class</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000000; font-weight: bold;">class</span> CountMapper <span style="color: #000000; font-weight: bold;">extends</span>
                Mapper<span style="color: #339933;">&lt;</span>LongWritable, Text, Text, IntWritable<span style="color: #339933;">&gt;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000000; font-weight: bold;">final</span> IntWritable one <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> IntWritable<span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">1</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #000000; font-weight: bold;">private</span> Text word <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> Text<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000066; font-weight: bold;">boolean</span> caseSensitive <span style="color: #339933;">=</span> <span style="color: #000066; font-weight: bold;">true</span><span style="color: #339933;">;</span>
    &nbsp;
            @Override
            <span style="color: #000000; font-weight: bold;">protected</span> <span style="color: #000066; font-weight: bold;">void</span> setup<span style="color: #009900;">&#40;</span><span style="color: #003399;">Context</span> context<span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">throws</span> <span style="color: #003399;">IOException</span>,
                    <span style="color: #003399;">InterruptedException</span> <span style="color: #009900;">&#123;</span>
                <span style="color: #666666; font-style: italic;">// 读取配置</span>
                Configuration conf <span style="color: #339933;">=</span> context.<span style="color: #006633;">getConfiguration</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                caseSensitive <span style="color: #339933;">=</span> conf.<span style="color: #006633;">getBoolean</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;wordcount.case.sensitive&quot;</span>, <span style="color: #000066; font-weight: bold;">true</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #000000; font-weight: bold;">super</span>.<span style="color: #006633;">setup</span><span style="color: #009900;">&#40;</span>context<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
    &nbsp;
            @Override
            <span style="color: #000000; font-weight: bold;">protected</span> <span style="color: #000066; font-weight: bold;">void</span> map<span style="color: #009900;">&#40;</span>LongWritable key, Text value, <span style="color: #003399;">Context</span> context<span style="color: #009900;">&#41;</span>
                    <span style="color: #000000; font-weight: bold;">throws</span> <span style="color: #003399;">IOException</span>, <span style="color: #003399;">InterruptedException</span> <span style="color: #009900;">&#123;</span>
                <span style="color: #003399;">StringTokenizer</span> itr <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">StringTokenizer</span><span style="color: #009900;">&#40;</span>value.<span style="color: #006633;">toString</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #000000; font-weight: bold;">while</span> <span style="color: #009900;">&#40;</span>itr.<span style="color: #006633;">hasMoreTokens</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                    <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>caseSensitive<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span> <span style="color: #666666; font-style: italic;">// 是否大小写敏感</span>
                        word.<span style="color: #006633;">set</span><span style="color: #009900;">&#40;</span>itr.<span style="color: #006633;">nextToken</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">else</span> <span style="color: #009900;">&#123;</span>
                        word.<span style="color: #006633;">set</span><span style="color: #009900;">&#40;</span>itr.<span style="color: #006633;">nextToken</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">toLowerCase</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    <span style="color: #009900;">&#125;</span>
                    context.<span style="color: #006633;">write</span><span style="color: #009900;">&#40;</span>word, one<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    context.<span style="color: #006633;">getCounter</span><span style="color: #009900;">&#40;</span>Counters.<span style="color: #006633;">INPUT_WORDS</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">increment</span><span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">1</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #009900;">&#125;</span>
            <span style="color: #009900;">&#125;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000000; font-weight: bold;">class</span> CountReducer <span style="color: #000000; font-weight: bold;">extends</span>
                Reducer<span style="color: #339933;">&lt;</span>Text, IntWritable, Text, IntWritable<span style="color: #339933;">&gt;</span> <span style="color: #009900;">&#123;</span>
    &nbsp;
            @Override
            <span style="color: #000000; font-weight: bold;">protected</span> <span style="color: #000066; font-weight: bold;">void</span> reduce<span style="color: #009900;">&#40;</span>Text text, Iterable<span style="color: #339933;">&lt;</span>IntWritable<span style="color: #339933;">&gt;</span> values,
                    <span style="color: #003399;">Context</span> context<span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">throws</span> <span style="color: #003399;">IOException</span>, <span style="color: #003399;">InterruptedException</span> <span style="color: #009900;">&#123;</span>
                <span style="color: #000066; font-weight: bold;">int</span> sum <span style="color: #339933;">=</span> <span style="color: #cc66cc;">0</span><span style="color: #339933;">;</span>
                <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span>IntWritable value <span style="color: #339933;">:</span> values<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                    sum <span style="color: #339933;">+=</span> value.<span style="color: #006633;">get</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #009900;">&#125;</span>
                context.<span style="color: #006633;">write</span><span style="color: #009900;">&#40;</span>text, <span style="color: #000000; font-weight: bold;">new</span> IntWritable<span style="color: #009900;">&#40;</span>sum<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
    &nbsp;
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        @Override
        <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">int</span> run<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> args<span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">throws</span> <span style="color: #003399;">Exception</span> <span style="color: #009900;">&#123;</span>
            Configuration conf <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> Configuration<span style="color: #009900;">&#40;</span>getConf<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            Job job <span style="color: #339933;">=</span> Job.<span style="color: #006633;">getInstance</span><span style="color: #009900;">&#40;</span>conf, <span style="color: #0000ff;">&quot;Example Hadoop WordCount&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            job.<span style="color: #006633;">setJarByClass</span><span style="color: #009900;">&#40;</span>WordCount.<span style="color: #000000; font-weight: bold;">class</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            job.<span style="color: #006633;">setMapperClass</span><span style="color: #009900;">&#40;</span>CountMapper.<span style="color: #000000; font-weight: bold;">class</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            job.<span style="color: #006633;">setCombinerClass</span><span style="color: #009900;">&#40;</span>CountReducer.<span style="color: #000000; font-weight: bold;">class</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            job.<span style="color: #006633;">setReducerClass</span><span style="color: #009900;">&#40;</span>CountReducer.<span style="color: #000000; font-weight: bold;">class</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
            job.<span style="color: #006633;">setOutputKeyClass</span><span style="color: #009900;">&#40;</span>Text.<span style="color: #000000; font-weight: bold;">class</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            job.<span style="color: #006633;">setOutputValueClass</span><span style="color: #009900;">&#40;</span>IntWritable.<span style="color: #000000; font-weight: bold;">class</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
            List<span style="color: #339933;">&lt;</span>String<span style="color: #339933;">&gt;</span> other_args <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> ArrayList<span style="color: #339933;">&lt;</span>String<span style="color: #339933;">&gt;</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> i <span style="color: #339933;">=</span> <span style="color: #cc66cc;">0</span><span style="color: #339933;">;</span> i <span style="color: #339933;">&lt;</span> args.<span style="color: #006633;">length</span><span style="color: #339933;">;</span> <span style="color: #339933;">++</span>i<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                other_args.<span style="color: #006633;">add</span><span style="color: #009900;">&#40;</span>args<span style="color: #009900;">&#91;</span>i<span style="color: #009900;">&#93;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
    &nbsp;
            FileInputFormat.<span style="color: #006633;">addInputPath</span><span style="color: #009900;">&#40;</span>job, <span style="color: #000000; font-weight: bold;">new</span> Path<span style="color: #009900;">&#40;</span>other_args.<span style="color: #006633;">get</span><span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">0</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            FileOutputFormat.<span style="color: #006633;">setOutputPath</span><span style="color: #009900;">&#40;</span>job, <span style="color: #000000; font-weight: bold;">new</span> Path<span style="color: #009900;">&#40;</span>other_args.<span style="color: #006633;">get</span><span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">1</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #000066; font-weight: bold;">int</span> ret <span style="color: #339933;">=</span> job.<span style="color: #006633;">waitForCompletion</span><span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">true</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">?</span> <span style="color: #cc66cc;">0</span> <span style="color: #339933;">:</span> <span style="color: #cc66cc;">1</span><span style="color: #339933;">;</span>
    &nbsp;
            <span style="color: #000066; font-weight: bold;">long</span> inputWord <span style="color: #339933;">=</span> job.<span style="color: #006633;">getCounters</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">findCounter</span><span style="color: #009900;">&#40;</span>Counters.<span style="color: #006633;">INPUT_WORDS</span><span style="color: #009900;">&#41;</span>
                    .<span style="color: #006633;">getValue</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;INPUT_WORDS:&quot;</span> <span style="color: #339933;">+</span> inputWord<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            logger.<span style="color: #006633;">info</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;test log: &quot;</span> <span style="color: #339933;">+</span> inputWord<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #000000; font-weight: bold;">return</span> ret<span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000066; font-weight: bold;">void</span> main<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> args<span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">throws</span> <span style="color: #003399;">Exception</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000066; font-weight: bold;">int</span> res <span style="color: #339933;">=</span> ToolRunner.<span style="color: #006633;">run</span><span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">new</span> Configuration<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, <span style="color: #000000; font-weight: bold;">new</span> WordCount<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, args<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
            <span style="color: #003399;">System</span>.<span style="color: #006633;">exit</span><span style="color: #009900;">&#40;</span>res<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">package com.fatkun;
    
    import java.io.IOException;
    import java.util.ArrayList;
    import java.util.List;
    import java.util.StringTokenizer;
    
    import org.apache.commons.logging.Log;
    import org.apache.commons.logging.LogFactory;
    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.conf.Configured;
    import org.apache.hadoop.fs.Path;
    import org.apache.hadoop.io.IntWritable;
    import org.apache.hadoop.io.LongWritable;
    import org.apache.hadoop.io.Text;
    import org.apache.hadoop.mapreduce.Job;
    import org.apache.hadoop.mapreduce.Mapper;
    import org.apache.hadoop.mapreduce.Reducer;
    import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
    import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
    import org.apache.hadoop.util.Tool;
    import org.apache.hadoop.util.ToolRunner;
    
    public class WordCount extends Configured implements Tool {
        static enum Counters {
            INPUT_WORDS // 计数器
        } 
    
        static Log logger = LogFactory.getLog(WordCount.class);
    
        public static class CountMapper extends
                Mapper&lt;LongWritable, Text, Text, IntWritable&gt; {
            private final IntWritable one = new IntWritable(1);
            private Text word = new Text();
            private boolean caseSensitive = true;
    
            @Override
            protected void setup(Context context) throws IOException,
                    InterruptedException {
                // 读取配置
                Configuration conf = context.getConfiguration();
                caseSensitive = conf.getBoolean(&quot;wordcount.case.sensitive&quot;, true);
                super.setup(context);
            }
    
            @Override
            protected void map(LongWritable key, Text value, Context context)
                    throws IOException, InterruptedException {
                StringTokenizer itr = new StringTokenizer(value.toString());
                while (itr.hasMoreTokens()) {
                    if (caseSensitive) { // 是否大小写敏感
                        word.set(itr.nextToken());
                    } else {
                        word.set(itr.nextToken().toLowerCase());
                    }
                    context.write(word, one);
                    context.getCounter(Counters.INPUT_WORDS).increment(1);
                }
            }
        }
    
        public static class CountReducer extends
                Reducer&lt;Text, IntWritable, Text, IntWritable&gt; {
    
            @Override
            protected void reduce(Text text, Iterable&lt;IntWritable&gt; values,
                    Context context) throws IOException, InterruptedException {
                int sum = 0;
                for (IntWritable value : values) {
                    sum += value.get();
                }
                context.write(text, new IntWritable(sum));
            }
    
        }
    
        @Override
        public int run(String[] args) throws Exception {
            Configuration conf = new Configuration(getConf());
            Job job = Job.getInstance(conf, &quot;Example Hadoop WordCount&quot;);
            job.setJarByClass(WordCount.class);
            job.setMapperClass(CountMapper.class);
            job.setCombinerClass(CountReducer.class);
            job.setReducerClass(CountReducer.class);
    
            job.setOutputKeyClass(Text.class);
            job.setOutputValueClass(IntWritable.class);
    
            List&lt;String&gt; other_args = new ArrayList&lt;String&gt;();
            for (int i = 0; i &lt; args.length; ++i) {
                other_args.add(args[i]);
            }
    
            FileInputFormat.addInputPath(job, new Path(other_args.get(0)));
            FileOutputFormat.setOutputPath(job, new Path(other_args.get(1)));
            int ret = job.waitForCompletion(true) ? 0 : 1;
    
            long inputWord = job.getCounters().findCounter(Counters.INPUT_WORDS)
                    .getValue();
            System.out.println(&quot;INPUT_WORDS:&quot; + inputWord);
            logger.info(&quot;test log: &quot; + inputWord);
            return ret;
        }
    
        public static void main(String[] args) throws Exception {
            int res = ToolRunner.run(new Configuration(), new WordCount(), args);
    
            System.exit(res);
        }
    
    }</p></div>
    ";i:2;s:886:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="bash" style="font-family:monospace;">hadoop <span style="color: #c20cb9; font-weight: bold;">jar</span> wordcount.jar com.fatkun.WordCount -Dwordcount.case.sensitive=<span style="color: #c20cb9; font-weight: bold;">false</span> <span style="color: #000000; font-weight: bold;">/</span>user<span style="color: #000000; font-weight: bold;">/</span>fatkun<span style="color: #000000; font-weight: bold;">/</span>input <span style="color: #000000; font-weight: bold;">/</span>user<span style="color: #000000; font-weight: bold;">/</span>fatkun<span style="color: #000000; font-weight: bold;">/</span>output</pre></td></tr></table><p class="theCode" style="display:none;">hadoop jar wordcount.jar com.fatkun.WordCount -Dwordcount.case.sensitive=false /user/fatkun/input /user/fatkun/output</p></div>
    ";}
categories:
  - hadoop
tags:
  - example
  - hadoop
  - wordcount

---
## 准备

准备一些输入文件，可以用hdfs dfs -put xxx/* /user/fatkun/input上传文件
## 代码

<pre lang="java" escaped="true">package com.fatkun;

import java.io.IOException;
import java.util.ArrayList;
import java.util.List;
import java.util.StringTokenizer;

import org.apache.commons.logging.Log;
import org.apache.commons.logging.LogFactory;
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.conf.Configured;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.LongWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.Mapper;
import org.apache.hadoop.mapreduce.Reducer;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
import org.apache.hadoop.util.Tool;
import org.apache.hadoop.util.ToolRunner;

public class WordCount extends Configured implements Tool {
    static enum Counters {
        INPUT_WORDS // 计数器
    } 

    static Log logger = LogFactory.getLog(WordCount.class);

    public static class CountMapper extends
            Mapper&lt;LongWritable, Text, Text, IntWritable&gt; {
        private final IntWritable one = new IntWritable(1);
        private Text word = new Text();
        private boolean caseSensitive = true;

        @Override
        protected void setup(Context context) throws IOException,
                InterruptedException {
            // 读取配置
            Configuration conf = context.getConfiguration();
            caseSensitive = conf.getBoolean("wordcount.case.sensitive", true);
            super.setup(context);
        }

        @Override
        protected void map(LongWritable key, Text value, Context context)
                throws IOException, InterruptedException {
            StringTokenizer itr = new StringTokenizer(value.toString());
            while (itr.hasMoreTokens()) {
                if (caseSensitive) { // 是否大小写敏感
                    word.set(itr.nextToken());
                } else {
                    word.set(itr.nextToken().toLowerCase());
                }
                context.write(word, one);
                context.getCounter(Counters.INPUT_WORDS).increment(1);
            }
        }
    }

    public static class CountReducer extends
            Reducer&lt;Text, IntWritable, Text, IntWritable&gt; {

        @Override
        protected void reduce(Text text, Iterable&lt;IntWritable&gt; values,
                Context context) throws IOException, InterruptedException {
            int sum = 0;
            for (IntWritable value : values) {
                sum += value.get();
            }
            context.write(text, new IntWritable(sum));
        }

    }

    @Override
    public int run(String[] args) throws Exception {
        Configuration conf = new Configuration(getConf());
        Job job = Job.getInstance(conf, "Example Hadoop WordCount");
        job.setJarByClass(WordCount.class);
        job.setMapperClass(CountMapper.class);
        job.setCombinerClass(CountReducer.class);
        job.setReducerClass(CountReducer.class);

        job.setOutputKeyClass(Text.class);
        job.setOutputValueClass(IntWritable.class);

        List&lt;String&gt; other_args = new ArrayList&lt;String&gt;();
        for (int i = 0; i &lt; args.length; ++i) {
            other_args.add(args[i]);
        }

        FileInputFormat.addInputPath(job, new Path(other_args.get(0)));
        FileOutputFormat.setOutputPath(job, new Path(other_args.get(1)));
        int ret = job.waitForCompletion(true) ? 0 : 1;

        long inputWord = job.getCounters().findCounter(Counters.INPUT_WORDS)
                .getValue();
        System.out.println("INPUT_WORDS:" + inputWord);
        logger.info("test log: " + inputWord);
        return ret;
    }

    public static void main(String[] args) throws Exception {
        int res = ToolRunner.run(new Configuration(), new WordCount(), args);

        System.exit(res);
    }

}</pre>
## 运行

在eclipse导出jar包，执行以下命令
<pre lang="bash" escaped="true">hadoop jar wordcount.jar com.fatkun.WordCount -Dwordcount.case.sensitive=false /user/fatkun/input /user/fatkun/output</pre>
&nbsp;
## 参考

<http://cxwangyi.blogspot.com/2009/12/wordcount-tutorial-for-hadoop-0201.html>
<http://hadoop.apache.org/docs/r1.2.1/mapred_tutorial.html#Example%3A+WordCount+v2.0>