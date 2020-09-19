---
title: 动态注册hive udf
author: fatkun
type: post
date: 2013-12-22T15:07:35+00:00
url: /2013/12/register-udf.html
duoshuo_thread_id:
  - 6300410060946277122
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:2507:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">  <span style="color: #000000; font-weight: bold;">public</span> SessionState<span style="color: #009900;">&#40;</span>HiveConf conf<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    ...
          <span style="color: #006633;">Class</span><span style="color: #339933;">&lt;?&gt;</span> pluginClass <span style="color: #339933;">=</span> <span style="color: #003399;">Utilities</span>.<span style="color: #006633;">getBuiltinUtilsClass</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #003399;">URL</span> jarLocation <span style="color: #339933;">=</span> pluginClass.<span style="color: #006633;">getProtectionDomain</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getCodeSource</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getLocation</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          add_builtin_resource<span style="color: #009900;">&#40;</span>ResourceType.<span style="color: #006633;">JAR</span>, jarLocation.<span style="color: #006633;">toString</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          FunctionRegistry.<span style="color: #006633;">registerFunctionsFromPluginJar</span><span style="color: #009900;">&#40;</span>jarLocation, pluginClass.<span style="color: #006633;">getClassLoader</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    ...
      <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">  public SessionState(HiveConf conf) {
    ...
          Class&lt;?&gt; pluginClass = Utilities.getBuiltinUtilsClass();
          URL jarLocation = pluginClass.getProtectionDomain().getCodeSource().getLocation();
          add_builtin_resource(ResourceType.JAR, jarLocation.toString());
          FunctionRegistry.registerFunctionsFromPluginJar(jarLocation, pluginClass.getClassLoader());
    ...
      }</p></div>
    ";i:2;s:1568:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #666666; font-style: italic;">//我们可以用这两个方法来注册udf</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000066; font-weight: bold;">void</span> registerTemporaryUDF<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> functionName, Class<span style="color: #339933;">&lt;?</span> <span style="color: #000000; font-weight: bold;">extends</span> UDF<span style="color: #339933;">&gt;</span> UDFClass, <span style="color: #000066; font-weight: bold;">boolean</span> isOperator<span style="color: #009900;">&#41;</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000066; font-weight: bold;">void</span> registerFunctionsFromPluginJar<span style="color: #009900;">&#40;</span><span style="color: #003399;">URL</span> jarLocation, <span style="color: #003399;">ClassLoader</span> classLoader<span style="color: #009900;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">//我们可以用这两个方法来注册udf
    public static void registerTemporaryUDF(String functionName, Class&lt;? extends UDF&gt; UDFClass, boolean isOperator)
    public static void registerFunctionsFromPluginJar(URL jarLocation, ClassLoader classLoader)</p></div>
    ";}
categories:
  - hive
tags:
  - hive
  - udf

---
## 目标

可以不重启hive服务端动态增加或更新udf，本文用到动态加载以及hive hook实现。
## 看看原来的代码是怎样写的

我看的是cdh4.3.0代码，目前有两个地方注册udf，
一个是在org.apache.hadoop.hive.ql.exec.FunctionRegistry类里，大部分的内置udf都是在这里注册的，很多网站都是通过修改这里代码重新打包来注册udf。
第二个是最近新增了一个hive-builtins*.jar文件，注册函数是在
<pre lang="java" escaped="true">public SessionState(HiveConf conf) {
...
      Class&lt;?&gt; pluginClass = Utilities.getBuiltinUtilsClass();
      URL jarLocation = pluginClass.getProtectionDomain().getCodeSource().getLocation();
      add_builtin_resource(ResourceType.JAR, jarLocation.toString());
      FunctionRegistry.registerFunctionsFromPluginJar(jarLocation, pluginClass.getClassLoader());
...
  }</pre>
通过找到org.apache.hive.builtins.BuiltinUtils类定位jar的位置，把jar包加入hive.added.jars.path配置里，然后通过FunctionRegistry.registerFunctionsFromPluginJar来注册udf
<pre lang="java" escaped="true">//我们可以用这两个方法来注册udf
public static void registerTemporaryUDF(String functionName, Class&lt;? extends UDF&gt; UDFClass, boolean isOperator)
public static void registerFunctionsFromPluginJar(URL jarLocation, ClassLoader classLoader)</pre>
<!--more-->

## 存在的问题

当我更新jar包时，发现执行的代码没有更新，发生什么问题了？原因是jar是动态加载的，udf.jar都是通过aux.path加入到当前线程里的，当一直都是同一个线程时，只是把jar放到classpath的末端，程序还是找到之前已经加载的代码。代码不能更新怎么办？**使用新的类名**，当找不到这个类名的时候，会到jar文件里面找。注意新jar包不要直接替换，否则jvm会奔溃。
## 最终解决方法

使用一个hook，通过registerFunctionsFromPluginJar来注册udf，hive hook的介绍可以看<a href="http://www.slideshare.net/julingks/apache-hive-hooksminwookim130813" target="_blank">这个PPT</a>
udf的代码可以参考buildin udf那个jar包时怎么做的
hook 代码，在解析hive语句之前注册udf
<pre lang="java" escaped="true">public class AddUdfHook extends AbstractSemanticAnalyzerHook {
	static final private Log LOG = LogFactory
			.getLog(AddUdfHook.class.getName());

	@Override
	public void postAnalyze(HiveSemanticAnalyzerHookContext context,
			List&lt;Task&lt;? extends Serializable&gt;&gt; rootTasks)
			throws SemanticException {
		super.postAnalyze(context, rootTasks);
	}

	@Override
	public ASTNode preAnalyze(HiveSemanticAnalyzerHookContext context,
			ASTNode ast) throws SemanticException {
		LOG.warn("udf register hook");

		try {
			Class&lt;?&gt; pluginClass = Class.forName("cn.uc.udf.CustomUtils");
			URL jarLocation = pluginClass.getProtectionDomain().getCodeSource()
					.getLocation();
			FunctionRegistry.registerFunctionsFromPluginJar(jarLocation,
					pluginClass.getClassLoader());
		} catch (Exception ex) {
			LOG.error("load udf err", ex);
		}
		return super.preAnalyze(context, ast);
	}</pre>
编译好了需要在hive-site.xml加上hook的配置
<pre lang="xml" escaped="true">&lt;property&gt;
    &lt;name&gt;hive.semantic.analyzer.hook&lt;/name&gt;
    &lt;value&gt;cn.uc.hook.AddUdfHook&lt;/value&gt;
  &lt;/property&gt;
 &lt;property&gt;
    &lt;name&gt;hive.aux.jars.path&lt;/name&gt;
    &lt;value&gt;file:///home/xxx/myudf.jar&lt;/value&gt;
  &lt;/property&gt;</pre>
<a href="http://pan.baidu.com/s/1ntnZFap" target="_blank">全部代码下载</a>