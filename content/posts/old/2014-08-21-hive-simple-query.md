---
title: hive简单查询的过程
author: fatkun
type: post
date: 2014-08-21T06:07:21+00:00
url: /2014/08/hive-simple-query.html
duoshuo_thread_id:
  - 6300410318589788930
wp-syntax-cache-content:
  - |
    a:12:{i:1;s:777:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="sql" style="font-family:monospace;"><span style="color: #993333; font-weight: bold;">SELECT</span> fr <span style="color: #993333; font-weight: bold;">FROM</span> xxxxxx <span style="color: #993333; font-weight: bold;">WHERE</span> substr<span style="color: #66cc66;">&#40;</span>fr<span style="color: #66cc66;">,</span> <span style="color: #cc66cc;">1</span><span style="color: #66cc66;">,</span> <span style="color: #cc66cc;">1</span><span style="color: #66cc66;">&#41;</span> <span style="color: #66cc66;">=</span> <span style="color: #ff0000;">'a'</span>;</pre></td></tr></table><p class="theCode" style="display:none;">select fr from xxxxxx where substr(fr, 1, 1) = 'a';</p></div>
    ";i:2;s:528:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="html" style="font-family:monospace;">TableScanOperator  表扫描
      FilterOperator         过滤条件
        SelectOperator       列裁剪，只查询fr出来
          FileSinkOperator   输出到文件</pre></td></tr></table><p class="theCode" style="display:none;">TableScanOperator  表扫描
      FilterOperator         过滤条件
        SelectOperator       列裁剪，只查询fr出来
          FileSinkOperator   输出到文件</p></div>
    ";i:3;s:1244:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">  <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> map<span style="color: #009900;">&#40;</span><span style="color: #003399;">Object</span> key, <span style="color: #003399;">Object</span> value, OutputCollector output,
          Reporter reporter<span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">throws</span> <span style="color: #003399;">IOException</span> <span style="color: #009900;">&#123;</span>
    ...
            <span style="color: #006633;">mo</span>.<span style="color: #006633;">process</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#40;</span>Writable<span style="color: #009900;">&#41;</span>value<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    ...
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">  public void map(Object key, Object value, OutputCollector output,
          Reporter reporter) throws IOException {
    ...
            mo.process((Writable)value);
    ...
    }</p></div>
    ";i:4;s:1083:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">rowWithPart<span style="color: #009900;">&#91;</span><span style="color: #cc66cc;">0</span><span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> deserializer.<span style="color: #006633;">deserialize</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#40;</span>Writable<span style="color: #009900;">&#41;</span> value<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    ...
    <span style="color: #006633;">forward</span><span style="color: #009900;">&#40;</span>rowWithPart, rowObjectInspector<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">// 传递给下一个Operator</span></pre></td></tr></table><p class="theCode" style="display:none;">rowWithPart[0] = deserializer.deserialize((Writable) value);
    ...
    forward(rowWithPart, rowObjectInspector); // 传递给下一个Operator</p></div>
    ";i:5;s:2299:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">    <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> i <span style="color: #339933;">=</span> <span style="color: #cc66cc;">0</span><span style="color: #339933;">;</span> i <span style="color: #339933;">&lt;</span> childOperatorsArray.<span style="color: #006633;">length</span><span style="color: #339933;">;</span> i<span style="color: #339933;">++</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          Operator<span style="color: #339933;">&lt;?</span> <span style="color: #000000; font-weight: bold;">extends</span> OperatorDesc<span style="color: #339933;">&gt;</span> o <span style="color: #339933;">=</span> childOperatorsArray<span style="color: #009900;">&#91;</span>i<span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span>
          <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>o.<span style="color: #006633;">getDone</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            childrenDone<span style="color: #339933;">++;</span>
          <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">else</span> <span style="color: #009900;">&#123;</span>
            o.<span style="color: #006633;">process</span><span style="color: #009900;">&#40;</span>row, childOperatorsTag<span style="color: #009900;">&#91;</span>i<span style="color: #009900;">&#93;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #009900;">&#125;</span>
        <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">    for (int i = 0; i &lt; childOperatorsArray.length; i++) {
          Operator&lt;? extends OperatorDesc&gt; o = childOperatorsArray[i];
          if (o.getDone()) {
            childrenDone++;
          } else {
            o.process(row, childOperatorsTag[i]);
          }
        }</p></div>
    ";i:6;s:1822:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">  <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> processOp<span style="color: #009900;">&#40;</span><span style="color: #003399;">Object</span> row, <span style="color: #000066; font-weight: bold;">int</span> tag<span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">throws</span> HiveException <span style="color: #009900;">&#123;</span>
        <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>conf <span style="color: #339933;">!=</span> <span style="color: #000066; font-weight: bold;">null</span> <span style="color: #339933;">&amp;&amp;</span> conf.<span style="color: #006633;">isGatherStats</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          gatherStats<span style="color: #009900;">&#40;</span>row<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
        forward<span style="color: #009900;">&#40;</span>row, inputObjInspectors<span style="color: #009900;">&#91;</span>tag<span style="color: #009900;">&#93;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
      <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">  public void processOp(Object row, int tag) throws HiveException {
        if (conf != null &amp;&amp; conf.isGatherStats()) {
          gatherStats(row);
        }
        forward(row, inputObjInspectors[tag]);
      }</p></div>
    ";i:7;s:538:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #003399;">Object</span> condition <span style="color: #339933;">=</span> conditionEvaluator.<span style="color: #006633;">evaluate</span><span style="color: #009900;">&#40;</span>row<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span></pre></td></tr></table><p class="theCode" style="display:none;">Object condition = conditionEvaluator.evaluate(row);</p></div>
    ";i:8;s:1874:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">class</span> org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">hadoop</span>.<span style="color: #006633;">hive</span>.<span style="color: #006633;">ql</span>.<span style="color: #006633;">udf</span>.<span style="color: #006633;">generic</span>.<span style="color: #006633;">GenericUDFOPEqual</span><span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">class</span> org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">hadoop</span>.<span style="color: #006633;">hive</span>.<span style="color: #006633;">ql</span>.<span style="color: #006633;">udf</span>.<span style="color: #006633;">generic</span>.<span style="color: #006633;">GenericUDFBridge</span><span style="color: #009900;">&#40;</span>Column<span style="color: #009900;">&#91;</span>fr<span style="color: #009900;">&#93;</span>, <span style="color: #000000; font-weight: bold;">Const</span> <span style="color: #000066; font-weight: bold;">int</span> <span style="color: #cc66cc;">1</span>, <span style="color: #000000; font-weight: bold;">Const</span> <span style="color: #000066; font-weight: bold;">int</span> <span style="color: #cc66cc;">1</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, <span style="color: #000000; font-weight: bold;">Const</span> string a<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">class org.apache.hadoop.hive.ql.udf.generic.GenericUDFOPEqual(class org.apache.hadoop.hive.ql.udf.generic.GenericUDFBridge(Column[fr], Const int 1, Const int 1(), Const string a()</p></div>
    ";i:9;s:3269:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">  @Override
      <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #003399;">Object</span> evaluate<span style="color: #009900;">&#40;</span>DeferredObject<span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> arguments<span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">throws</span> HiveException <span style="color: #009900;">&#123;</span>
        <span style="color: #000000; font-weight: bold;">assert</span> <span style="color: #009900;">&#40;</span>arguments.<span style="color: #006633;">length</span> <span style="color: #339933;">==</span> realArguments.<span style="color: #006633;">length</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #666666; font-style: italic;">// Calculate all the arguments</span>
        <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> i <span style="color: #339933;">=</span> <span style="color: #cc66cc;">0</span><span style="color: #339933;">;</span> i <span style="color: #339933;">&lt;</span> realArguments.<span style="color: #006633;">length</span><span style="color: #339933;">;</span> i<span style="color: #339933;">++</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          realArguments<span style="color: #009900;">&#91;</span>i<span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> arguments<span style="color: #009900;">&#91;</span>i<span style="color: #009900;">&#93;</span>.<span style="color: #006633;">get</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        <span style="color: #666666; font-style: italic;">// Call the function</span>
        <span style="color: #003399;">Object</span> result <span style="color: #339933;">=</span> FunctionRegistry.<span style="color: #006633;">invoke</span><span style="color: #009900;">&#40;</span>udfMethod, udf, conversionHelper
            .<span style="color: #006633;">convertIfNecessary</span><span style="color: #009900;">&#40;</span>realArguments<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">return</span> result<span style="color: #339933;">;</span>
      <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">  @Override
      public Object evaluate(DeferredObject[] arguments) throws HiveException {
        assert (arguments.length == realArguments.length);
    
        // Calculate all the arguments
        for (int i = 0; i &lt; realArguments.length; i++) {
          realArguments[i] = arguments[i].get();
        }
    
        // Call the function
        Object result = FunctionRegistry.invoke(udfMethod, udf, conversionHelper
            .convertIfNecessary(realArguments));
    
        return result;
      }</p></div>
    ";i:10;s:1041:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">    <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>conf.<span style="color: #006633;">isSelStarNoCompute</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          forward<span style="color: #009900;">&#40;</span>row, inputObjInspectors<span style="color: #009900;">&#91;</span>tag<span style="color: #009900;">&#93;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #000000; font-weight: bold;">return</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">    if (conf.isSelStarNoCompute()) {
          forward(row, inputObjInspectors[tag]);
          return;
        }</p></div>
    ";i:11;s:3325:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">    <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> i <span style="color: #339933;">=</span> <span style="color: #cc66cc;">0</span><span style="color: #339933;">;</span> i <span style="color: #339933;">&lt;</span> eval.<span style="color: #006633;">length</span><span style="color: #339933;">;</span> i<span style="color: #339933;">++</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#123;</span>
            output<span style="color: #009900;">&#91;</span>i<span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> eval<span style="color: #009900;">&#91;</span>i<span style="color: #009900;">&#93;</span>.<span style="color: #006633;">evaluate</span><span style="color: #009900;">&#40;</span>row<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span>HiveException e<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">throw</span> e<span style="color: #339933;">;</span>
          <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">RuntimeException</span> e<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">throw</span> <span style="color: #000000; font-weight: bold;">new</span> HiveException<span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Error evaluating &quot;</span>
                <span style="color: #339933;">+</span> conf.<span style="color: #006633;">getColList</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">get</span><span style="color: #009900;">&#40;</span>i<span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getExprString</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, e<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #009900;">&#125;</span>
        <span style="color: #009900;">&#125;</span>
        forward<span style="color: #009900;">&#40;</span>output, outputObjInspector<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span></pre></td></tr></table><p class="theCode" style="display:none;">    for (int i = 0; i &lt; eval.length; i++) {
          try {
            output[i] = eval[i].evaluate(row);
          } catch (HiveException e) {
            throw e;
          } catch (RuntimeException e) {
            throw new HiveException(&quot;Error evaluating &quot;
                + conf.getColList().get(i).getExprString(), e);
          }
        }
        forward(output, outputObjInspector);</p></div>
    ";i:12;s:1036:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">recordValue <span style="color: #339933;">=</span> serializer.<span style="color: #006633;">serialize</span><span style="color: #009900;">&#40;</span>row, inputObjInspectors<span style="color: #009900;">&#91;</span><span style="color: #cc66cc;">0</span><span style="color: #009900;">&#93;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    ...
    <span style="color: #006633;">rowOutWriters</span><span style="color: #009900;">&#91;</span><span style="color: #cc66cc;">0</span><span style="color: #009900;">&#93;</span>.<span style="color: #006633;">write</span><span style="color: #009900;">&#40;</span>recordValue<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span></pre></td></tr></table><p class="theCode" style="display:none;">recordValue = serializer.serialize(row, inputObjInspectors[0]);
    ...
    rowOutWriters[0].write(recordValue);</p></div>
    ";}
categories:
  - hive
tags:
  - hive
  - 代码分析

---
查询以下语句的过程
<pre escaped="true" lang="sql">select fr from xxxxxx where substr(fr, 1, 1) = 'a';</pre>
Hive查询在编译的阶段把语句转换成一个个有层级关系的Operator，然后执行下去。
ExecMapper中mo是一个MapOperator对象，里面有个childOperators存储了一个树形的操作步骤(Operator)，如本次查询的Operator结构如下:
<pre lang="html" escaped="true">TableScanOperator  表扫描
  FilterOperator         过滤条件
    SelectOperator       列裁剪，只查询fr出来
      FileSinkOperator   输出到文件
</pre>
首先第一步是mo.process()，传入的value是整行内容
<pre lang="java" escaped="true">public void map(Object key, Object value, OutputCollector output,
      Reporter reporter) throws IOException {
...
        mo.process((Writable)value);
...
}</pre>
没做什么处理，只是做了个反序列化，放入rowWithPart[0]中
<pre lang="java" escaped="true">rowWithPart[0] = deserializer.deserialize((Writable) value);
...
forward(rowWithPart, rowObjectInspector); // 传递给下一个Operator
</pre>
遍历它的所有子Operator，一个个做
<pre lang="java" escaped="true">for (int i = 0; i &lt; childOperatorsArray.length; i++) {
      Operator&lt;? extends OperatorDesc&gt; o = childOperatorsArray[i];
      if (o.getDone()) {
        childrenDone++;
      } else {
        o.process(row, childOperatorsTag[i]);
      }
    }</pre>
下一个Operator是TableScan，这个只是单纯传给下一个Operator
<pre lang="java" escaped="true">public void processOp(Object row, int tag) throws HiveException {
    if (conf != null && conf.isGatherStats()) {
      gatherStats(row);
    }
    forward(row, inputObjInspectors[tag]);
  }</pre>
下一个Operator是FilterOperator，执行udf和判断条件是否成立，如果成立才传给下一个  
这里有个计数器 PASSED记录通过的， FILTERED记录被过滤掉的。
<pre lang="java" escaped="true">Object condition = conditionEvaluator.evaluate(row);</pre>
从FilterOperator可以看到conditionEvaluator的expr值有
<pre escaped="true" lang="java">class org.apache.hadoop.hive.ql.udf.generic.GenericUDFOPEqual(class org.apache.hadoop.hive.ql.udf.generic.GenericUDFBridge(Column[fr], Const int 1, Const int 1(), Const string a()</pre>
这里面有一个substr的udf，来看一下他是怎么处理的。substr(fr, 1, 1) = &#8216;a&#8217; ，这里很多地方都调用了get()方法，用来获取值。  
udf是通过反射调用的, udf function看起来只实例化一次
<pre lang="java" escaped="true">@Override
  public Object evaluate(DeferredObject[] arguments) throws HiveException {
    assert (arguments.length == realArguments.length);

    // Calculate all the arguments
    for (int i = 0; i &lt; realArguments.length; i++) {
      realArguments[i] = arguments[i].get();
    }

    // Call the function
    Object result = FunctionRegistry.invoke(udfMethod, udf, conversionHelper
        .convertIfNecessary(realArguments));

    return result;
  }</pre>
下一个Operator是SelectOperator，只输出某些列，如果是select *，就原样输出
<pre lang="java" escaped="true">if (conf.isSelStarNoCompute()) {
      forward(row, inputObjInspectors[tag]);
      return;
    }</pre>
我们是只取出fr的，所以有个eval[0]，取出的结果放到output里面，这里输出的是output=[&#8216;android&#8217;]
<pre lang="java" escaped="true">for (int i = 0; i &lt; eval.length; i++) {
      try {
        output[i] = eval[i].evaluate(row);
      } catch (HiveException e) {
        throw e;
      } catch (RuntimeException e) {
        throw new HiveException("Error evaluating "
            + conf.getColList().get(i).getExprString(), e);
      }
    }
    forward(output, outputObjInspector);</pre>
最后一步FileSinkOperator,序列化结果写到磁盘
<pre lang="java" escaped="true">recordValue = serializer.serialize(row, inputObjInspectors[0]);
...
rowOutWriters[0].write(recordValue);</pre>
重复以上步骤，直到所有数据全部读完。