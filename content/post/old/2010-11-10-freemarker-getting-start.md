---
title: FreeMarker简单入门
author: fatkun
type: post
date: 2010-11-09T16:48:30+00:00
url: /2010/11/freemarker-getting-start.html
duoshuo_thread_id:
  - 6300408776851718913
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:10585:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">package</span> <span style="color: #006699;">com.fatkun</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">java.io.IOException</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">java.io.OutputStreamWriter</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">java.io.Writer</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">java.util.HashMap</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">java.util.Map</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">freemarker.cache.ClassTemplateLoader</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">freemarker.template.Configuration</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">freemarker.template.DefaultObjectWrapper</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">freemarker.template.Template</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">freemarker.template.TemplateException</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">freemarker.template.TemplateExceptionHandler</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> TestFM <span style="color: #009900;">&#123;</span>
    &nbsp;
    	<span style="color: #008000; font-style: italic; font-weight: bold;">/**
    	 * @param args
    	 */</span>
    	<span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000066; font-weight: bold;">void</span> main<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> args<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    		<span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#123;</span>
            Configuration cfg <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> Configuration<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #666666; font-style: italic;">//相对于TestFM类目录下的templates目录，</span>
            cfg.<span style="color: #006633;">setTemplateLoader</span><span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">new</span> ClassTemplateLoader<span style="color: #009900;">&#40;</span>TestFM.<span style="color: #000000; font-weight: bold;">class</span>,<span style="color: #0000ff;">&quot;templates&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #666666; font-style: italic;">//cfg.setDirectoryForTemplateLoading(new File(&quot;绝对路径&quot;));</span>
            cfg.<span style="color: #006633;">setObjectWrapper</span><span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">new</span> DefaultObjectWrapper<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #666666; font-style: italic;">//设置异常处理器</span>
            cfg.<span style="color: #006633;">setTemplateExceptionHandler</span><span style="color: #009900;">&#40;</span>TemplateExceptionHandler.<span style="color: #006633;">IGNORE_HANDLER</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
    		Template temp <span style="color: #339933;">=</span> cfg.<span style="color: #006633;">getTemplate</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;test.ftl&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
            <span style="color: #666666; font-style: italic;">/* Create a data-model */</span>
            <span style="color: #003399;">Map</span> root <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">HashMap</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            root.<span style="color: #006633;">put</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;user&quot;</span>, <span style="color: #0000ff;">&quot;Fatkun&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #003399;">Map</span> latest <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">HashMap</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            latest.<span style="color: #006633;">put</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;url&quot;</span>, <span style="color: #0000ff;">&quot;products/greenmouse.html&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            latest.<span style="color: #006633;">put</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;name&quot;</span>, <span style="color: #0000ff;">&quot;green mouse&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            root.<span style="color: #006633;">put</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;latestProduct&quot;</span>, latest<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
            <span style="color: #666666; font-style: italic;">/* Merge data-model with template */</span>
            <span style="color: #003399;">Writer</span> out <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">OutputStreamWriter</span><span style="color: #009900;">&#40;</span><span style="color: #003399;">System</span>.<span style="color: #006633;">out</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            temp.<span style="color: #006633;">process</span><span style="color: #009900;">&#40;</span>root, out<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            out.<span style="color: #006633;">flush</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">IOException</span> e<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    			e.<span style="color: #006633;">printStackTrace</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span>TemplateException e<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    			e.<span style="color: #006633;">printStackTrace</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #009900;">&#125;</span>
    &nbsp;
    	<span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">package com.fatkun;
    import java.io.IOException;
    import java.io.OutputStreamWriter;
    import java.io.Writer;
    import java.util.HashMap;
    import java.util.Map;
    
    import freemarker.cache.ClassTemplateLoader;
    import freemarker.template.Configuration;
    import freemarker.template.DefaultObjectWrapper;
    import freemarker.template.Template;
    import freemarker.template.TemplateException;
    import freemarker.template.TemplateExceptionHandler;
    
    public class TestFM {
    
    	/**
    	 * @param args
    	 */
    	public static void main(String[] args) {
    		try {
            Configuration cfg = new Configuration();
            //相对于TestFM类目录下的templates目录，
            cfg.setTemplateLoader(new ClassTemplateLoader(TestFM.class,&quot;templates&quot;));
            //cfg.setDirectoryForTemplateLoading(new File(&quot;绝对路径&quot;));
            cfg.setObjectWrapper(new DefaultObjectWrapper());
            //设置异常处理器
            cfg.setTemplateExceptionHandler(TemplateExceptionHandler.IGNORE_HANDLER);
    
    		Template temp = cfg.getTemplate(&quot;test.ftl&quot;);
    
            /* Create a data-model */
            Map root = new HashMap();
            root.put(&quot;user&quot;, &quot;Fatkun&quot;);
            Map latest = new HashMap();
            latest.put(&quot;url&quot;, &quot;products/greenmouse.html&quot;);
            latest.put(&quot;name&quot;, &quot;green mouse&quot;);
            root.put(&quot;latestProduct&quot;, latest);
    
            /* Merge data-model with template */
            Writer out = new OutputStreamWriter(System.out);
            temp.process(root, out);
            out.flush();
    		} catch (IOException e) {
    			e.printStackTrace();
    		} catch (TemplateException e) {
    			e.printStackTrace();
    		}
    
    	}
    
    }</p></div>
    ";i:2;s:930:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="html" style="font-family:monospace;">&lt;html&gt;
    &lt;head&gt;
      &lt;title&gt;欢迎!&lt;/title&gt;
    &lt;/head&gt;
    &lt;body&gt;
      &lt;h1&gt;
        欢迎 ${user}&lt;#if user == &quot;Fatkun&quot;&gt;, 你是肥坤啊！&lt;/#if&gt;!
      &lt;/h1&gt;
      &lt;p&gt;我们的最新产品：
      &lt;a href=&quot;${latestProduct.url}&quot;&gt;${latestProduct.name}&lt;/a&gt;!
    &lt;/body&gt;
    &lt;/html&gt;</pre></td></tr></table><p class="theCode" style="display:none;">&lt;html&gt;
    &lt;head&gt;
      &lt;title&gt;欢迎!&lt;/title&gt;
    &lt;/head&gt;
    &lt;body&gt;
      &lt;h1&gt;
        欢迎 ${user}&lt;#if user == &quot;Fatkun&quot;&gt;, 你是肥坤啊！&lt;/#if&gt;!
      &lt;/h1&gt;
      &lt;p&gt;我们的最新产品：
      &lt;a href=&quot;${latestProduct.url}&quot;&gt;${latestProduct.name}&lt;/a&gt;!
    &lt;/body&gt;
    &lt;/html&gt;</p></div>
    ";}
categories:
  - J2EE
tags:
  - FreeMarker
  - 模板

---
freemarker是用来根据模板生成代码的，有强大的模板语言。
项目地址：[http://freemarker.sourceforge.net][1]
TestFM.java 文件，放在com.fatkun目录下
<pre escaped="true" lang="java">package com.fatkun;
import java.io.IOException;
import java.io.OutputStreamWriter;
import java.io.Writer;
import java.util.HashMap;
import java.util.Map;

import freemarker.cache.ClassTemplateLoader;
import freemarker.template.Configuration;
import freemarker.template.DefaultObjectWrapper;
import freemarker.template.Template;
import freemarker.template.TemplateException;
import freemarker.template.TemplateExceptionHandler;

public class TestFM {

	/**
	 * @param args
	 */
	public static void main(String[] args) {
		try {
        Configuration cfg = new Configuration();
        //相对于TestFM类目录下的templates目录，
        cfg.setTemplateLoader(new ClassTemplateLoader(TestFM.class,"templates"));
        //cfg.setDirectoryForTemplateLoading(new File("绝对路径"));
        cfg.setObjectWrapper(new DefaultObjectWrapper());
        //设置异常处理器
        cfg.setTemplateExceptionHandler(TemplateExceptionHandler.IGNORE_HANDLER);

		Template temp = cfg.getTemplate("test.ftl");

        /* Create a data-model */
        Map root = new HashMap();
        root.put("user", "Fatkun");
        Map latest = new HashMap();
        latest.put("url", "products/greenmouse.html");
        latest.put("name", "green mouse");
        root.put("latestProduct", latest);

        /* Merge data-model with template */
        Writer out = new OutputStreamWriter(System.out);
        temp.process(root, out);
        out.flush();
		} catch (IOException e) {
			e.printStackTrace();
		} catch (TemplateException e) {
			e.printStackTrace();
		}

	}

}</pre>
模板文件，放在com.fatkun.templates目录下
<pre escaped="true" lang="html">&lt;html&gt;
&lt;head&gt;
  &lt;title&gt;欢迎!&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
  &lt;h1&gt;
    欢迎 ${user}&lt;#if user == "Fatkun"&gt;, 你是肥坤啊！&lt;/#if&gt;!
  &lt;/h1&gt;
  &lt;p&gt;我们的最新产品：
  &lt;a href="${latestProduct.url}"&gt;${latestProduct.name}&lt;/a&gt;!
&lt;/body&gt;
&lt;/html&gt;</pre>

 [1]: http://freemarker.sourceforge.net/