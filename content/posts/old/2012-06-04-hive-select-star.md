---
title: 'Hive Select * 替换回列字段'
author: fatkun
type: post
date: 2012-06-03T16:11:42+00:00
url: /2012/06/hive-select-star.html
duoshuo_thread_id:
  - 6300408859039105793
wp-syntax-cache-content:
  - |
    a:4:{i:1;s:3083:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">private</span> Operator<span style="color: #339933;">&lt;?&gt;</span> genSelectPlan<span style="color: #009900;">&#40;</span>ASTNode selExprList, QB qb,
          Operator<span style="color: #339933;">&lt;?&gt;</span> input<span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">throws</span> SemanticException <span style="color: #009900;">&#123;</span>
    ...
          <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>expr.<span style="color: #006633;">getType</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">==</span> HiveParser.<span style="color: #006633;">TOK_ALLCOLREF</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            pos <span style="color: #339933;">=</span> genColListRegex<span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;.*&quot;</span>, expr.<span style="color: #006633;">getChildCount</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">==</span> <span style="color: #cc66cc;">0</span> <span style="color: #339933;">?</span> <span style="color: #000066; font-weight: bold;">null</span>
                <span style="color: #339933;">:</span> getUnescapedName<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#40;</span>ASTNode<span style="color: #009900;">&#41;</span>expr.<span style="color: #006633;">getChild</span><span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">0</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">toLowerCase</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>,
                expr, col_list, inputRR, pos, out_rwsch, qb.<span style="color: #006633;">getAliases</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            selectStar <span style="color: #339933;">=</span> <span style="color: #000066; font-weight: bold;">true</span><span style="color: #339933;">;</span>
          <span style="color: #009900;">&#125;</span>
    ...
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">private Operator&lt;?&gt; genSelectPlan(ASTNode selExprList, QB qb,
          Operator&lt;?&gt; input) throws SemanticException {
    ...
          if (expr.getType() == HiveParser.TOK_ALLCOLREF) {
            pos = genColListRegex(&quot;.*&quot;, expr.getChildCount() == 0 ? null
                : getUnescapedName((ASTNode)expr.getChild(0)).toLowerCase(),
                expr, col_list, inputRR, pos, out_rwsch, qb.getAliases());
            selectStar = true;
          }
    ...
    }</p></div>
    ";i:2;s:458:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">Operator bodyOpInfo <span style="color: #339933;">=</span> genBodyPlan<span style="color: #009900;">&#40;</span>qb, srcOpInfo<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span></pre></td></tr></table><p class="theCode" style="display:none;">Operator bodyOpInfo = genBodyPlan(qb, srcOpInfo);</p></div>
    ";i:3;s:1340:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">    <span style="color: #666666; font-style: italic;">// Recurse over all the source tables</span>
        <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> alias <span style="color: #339933;">:</span> qb.<span style="color: #006633;">getTabAliases</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          Operator op <span style="color: #339933;">=</span> genTablePlan<span style="color: #009900;">&#40;</span>alias, qb<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          aliasToOpInfo.<span style="color: #006633;">put</span><span style="color: #009900;">&#40;</span>alias, op<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">    // Recurse over all the source tables
        for (String alias : qb.getTabAliases()) {
          Operator op = genTablePlan(alias, qb);
          aliasToOpInfo.put(alias, op);
        }</p></div>
    ";i:4;s:9644:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">  <span style="color: #000000; font-weight: bold;">private</span> Operator genTablePlan<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> alias, QB qb<span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">throws</span> SemanticException <span style="color: #009900;">&#123;</span>
    &nbsp;
        <span style="color: #003399;">String</span> alias_id <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span>qb.<span style="color: #006633;">getId</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">==</span> <span style="color: #000066; font-weight: bold;">null</span> <span style="color: #339933;">?</span> alias <span style="color: #339933;">:</span> qb.<span style="color: #006633;">getId</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot;:&quot;</span> <span style="color: #339933;">+</span> alias<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        Table tab <span style="color: #339933;">=</span> qb.<span style="color: #006633;">getMetaData</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getSrcForAlias</span><span style="color: #009900;">&#40;</span>alias<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        RowResolver rwsch<span style="color: #339933;">;</span>
    &nbsp;
        ........................
          <span style="color: #006633;">rwsch</span> <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> RowResolver<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #666666; font-style: italic;">// 先从Table中取到所有字段，加入RowResolver中</span>
            StructObjectInspector rowObjectInspector <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span>StructObjectInspector<span style="color: #009900;">&#41;</span> tab
                .<span style="color: #006633;">getDeserializer</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getObjectInspector</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            List<span style="color: #339933;">&lt;?</span> <span style="color: #000000; font-weight: bold;">extends</span> StructField<span style="color: #339933;">&gt;</span> fields <span style="color: #339933;">=</span> rowObjectInspector
                .<span style="color: #006633;">getAllStructFieldRefs</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> i <span style="color: #339933;">=</span> <span style="color: #cc66cc;">0</span><span style="color: #339933;">;</span> i <span style="color: #339933;">&lt;</span> fields.<span style="color: #006633;">size</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> i<span style="color: #339933;">++</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
              rwsch.<span style="color: #006633;">put</span><span style="color: #009900;">&#40;</span>alias, fields.<span style="color: #006633;">get</span><span style="color: #009900;">&#40;</span>i<span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getFieldName</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, <span style="color: #000000; font-weight: bold;">new</span> ColumnInfo<span style="color: #009900;">&#40;</span>fields
                  .<span style="color: #006633;">get</span><span style="color: #009900;">&#40;</span>i<span style="color: #009900;">&#41;</span>.<span style="color: #006633;">getFieldName</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, TypeInfoUtils
                  .<span style="color: #006633;">getTypeInfoFromObjectInspector</span><span style="color: #009900;">&#40;</span>fields.<span style="color: #006633;">get</span><span style="color: #009900;">&#40;</span>i<span style="color: #009900;">&#41;</span>
                  .<span style="color: #006633;">getFieldObjectInspector</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span>, alias, <span style="color: #000066; font-weight: bold;">false</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
          <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span>SerDeException e<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">throw</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">RuntimeException</span><span style="color: #009900;">&#40;</span>e<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #009900;">&#125;</span>
    <span style="color: #666666; font-style: italic;">// 这里再把Partition的字段给补上</span>
          <span style="color: #666666; font-style: italic;">// Hack!! - refactor once the metadata APIs with types are ready</span>
          <span style="color: #666666; font-style: italic;">// Finally add the partitioning columns</span>
          <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span>FieldSchema part_col <span style="color: #339933;">:</span> tab.<span style="color: #006633;">getPartCols</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            LOG.<span style="color: #006633;">trace</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Adding partition col: &quot;</span> <span style="color: #339933;">+</span> part_col<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #666666; font-style: italic;">// TODO: use the right type by calling part_col.getType() instead of</span>
            <span style="color: #666666; font-style: italic;">// String.class</span>
            rwsch.<span style="color: #006633;">put</span><span style="color: #009900;">&#40;</span>alias, part_col.<span style="color: #006633;">getName</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, <span style="color: #000000; font-weight: bold;">new</span> ColumnInfo<span style="color: #009900;">&#40;</span>part_col.<span style="color: #006633;">getName</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>,
                TypeInfoFactory.<span style="color: #006633;">stringTypeInfo</span>, alias, <span style="color: #000066; font-weight: bold;">true</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">  private Operator genTablePlan(String alias, QB qb) throws SemanticException {
    
        String alias_id = (qb.getId() == null ? alias : qb.getId() + &quot;:&quot; + alias);
        Table tab = qb.getMetaData().getSrcForAlias(alias);
        RowResolver rwsch;
    
        ........................
          rwsch = new RowResolver();
          try {
    // 先从Table中取到所有字段，加入RowResolver中
            StructObjectInspector rowObjectInspector = (StructObjectInspector) tab
                .getDeserializer().getObjectInspector();
            List&lt;? extends StructField&gt; fields = rowObjectInspector
                .getAllStructFieldRefs();
            for (int i = 0; i &lt; fields.size(); i++) {
              rwsch.put(alias, fields.get(i).getFieldName(), new ColumnInfo(fields
                  .get(i).getFieldName(), TypeInfoUtils
                  .getTypeInfoFromObjectInspector(fields.get(i)
                  .getFieldObjectInspector()), alias, false));
            }
          } catch (SerDeException e) {
            throw new RuntimeException(e);
          }
    // 这里再把Partition的字段给补上
          // Hack!! - refactor once the metadata APIs with types are ready
          // Finally add the partitioning columns
          for (FieldSchema part_col : tab.getPartCols()) {
            LOG.trace(&quot;Adding partition col: &quot; + part_col);
            // TODO: use the right type by calling part_col.getType() instead of
            // String.class
            rwsch.put(alias, part_col.getName(), new ColumnInfo(part_col.getName(),
                TypeInfoFactory.stringTypeInfo, alias, true));
          }</p></div>
    ";}
categories:
  - hive
tags:
  - hive
  - 云计算

---
Hive中会把TOK_ALLCOLREF替换成各个列名称，来看看代码中是如何做到的。  
我以TOK_ALLCOLREF入手看代码，执行顺序不是这样的，这算是倒叙？=。=
来看SemanticAnalyzer.class这个类，这是查询中用得最多了。  
首先看到genSelectPlan()方法
<pre escaped="true" lang="java">private Operator&lt;?&gt; genSelectPlan(ASTNode selExprList, QB qb,
      Operator&lt;?&gt; input) throws SemanticException {
...
      if (expr.getType() == HiveParser.TOK_ALLCOLREF) {
        pos = genColListRegex(".*", expr.getChildCount() == 0 ? null
            : getUnescapedName((ASTNode)expr.getChild(0)).toLowerCase(),
            expr, col_list, inputRR, pos, out_rwsch, qb.getAliases());
        selectStar = true;
      }
...
}</pre>
咱们的列名称就在col_list存着，继续看genColListRegex()方法。可以发现它是由传入的inputRR字段获取的。  
这inputRR是从调用这个方法就传过来了。。继续往上看。  
genBodyPlan(QB qb, Operator input)  
还是传过来的。。
<pre escaped="true" lang="java">Operator bodyOpInfo = genBodyPlan(qb, srcOpInfo);</pre>
srcOpInfo就是从这里来的，看一下genTablePlan
<pre escaped="true" lang="java">// Recurse over all the source tables
    for (String alias : qb.getTabAliases()) {
      Operator op = genTablePlan(alias, qb);
      aliasToOpInfo.put(alias, op);
    }</pre>
<pre escaped="true" lang="java">private Operator genTablePlan(String alias, QB qb) throws SemanticException {

    String alias_id = (qb.getId() == null ? alias : qb.getId() + ":" + alias);
    Table tab = qb.getMetaData().getSrcForAlias(alias);
    RowResolver rwsch;

    ........................
      rwsch = new RowResolver();
      try {
// 先从Table中取到所有字段，加入RowResolver中
        StructObjectInspector rowObjectInspector = (StructObjectInspector) tab
            .getDeserializer().getObjectInspector();
        List&lt;? extends StructField&gt; fields = rowObjectInspector
            .getAllStructFieldRefs();
        for (int i = 0; i &lt; fields.size(); i++) {
          rwsch.put(alias, fields.get(i).getFieldName(), new ColumnInfo(fields
              .get(i).getFieldName(), TypeInfoUtils
              .getTypeInfoFromObjectInspector(fields.get(i)
              .getFieldObjectInspector()), alias, false));
        }
      } catch (SerDeException e) {
        throw new RuntimeException(e);
      }
// 这里再把Partition的字段给补上
      // Hack!! - refactor once the metadata APIs with types are ready
      // Finally add the partitioning columns
      for (FieldSchema part_col : tab.getPartCols()) {
        LOG.trace("Adding partition col: " + part_col);
        // TODO: use the right type by calling part_col.getType() instead of
        // String.class
        rwsch.put(alias, part_col.getName(), new ColumnInfo(part_col.getName(),
            TypeInfoFactory.stringTypeInfo, alias, true));
      }
</pre>
可以看到RowResolver存的值是列字段+分区字段。  
最终select * 会得到这些值。。