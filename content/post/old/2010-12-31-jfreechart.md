---
title: JFreeChart使用方法(代码备忘)
author: fatkun
type: post
date: 2010-12-31T05:50:31+00:00
url: /2010/12/jfreechart.html
duoshuo_thread_id:
  - 6300408796401369857
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:11677:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #666666; font-style: italic;">//图片标题</span>
    <span style="color: #003399;">String</span> title <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;空调2002年市场占有率&quot;</span><span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">//设定数据源</span>
    DefaultPieDataset piedata <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> DefaultPieDataset<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">//第一个参数为名称，第二个参数是double数</span>
    piedata.<span style="color: #006633;">setValue</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;联想&quot;</span>, <span style="color: #cc66cc;">27.3</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    piedata.<span style="color: #006633;">setValue</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;长城&quot;</span>, <span style="color: #cc66cc;">12.2</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    piedata.<span style="color: #006633;">setValue</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;海尔&quot;</span>, <span style="color: #cc66cc;">5.5</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    piedata.<span style="color: #006633;">setValue</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;美的&quot;</span>, <span style="color: #cc66cc;">17.1</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    piedata.<span style="color: #006633;">setValue</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;松下&quot;</span>, <span style="color: #cc66cc;">9.0</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    piedata.<span style="color: #006633;">setValue</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;科龙&quot;</span>, <span style="color: #cc66cc;">19.0</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">//创建JFreeChart，都使用ChartFactory来创建JFreeChart,很标准的工厂设计模式</span>
    JFreeChart chart <span style="color: #339933;">=</span>
    ChartFactory.<span style="color: #006633;">createPieChart</span><span style="color: #009900;">&#40;</span>title, piedata, <span style="color: #000066; font-weight: bold;">true</span>, <span style="color: #000066; font-weight: bold;">true</span>, <span style="color: #000066; font-weight: bold;">true</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">//设定图片标题</span>
    chart.<span style="color: #006633;">setTitle</span><span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">new</span> TextTitle<span style="color: #009900;">&#40;</span>title, <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">Font</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;隶书&quot;</span>, <span style="color: #003399;">Font</span>.<span style="color: #006633;">ITALIC</span>, <span style="color: #cc66cc;">15</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">//chart.addSubtitle(new TextTitle(&quot;2002财年分析&quot;, new Font(&quot;隶书&quot;, Font.ITALIC, 12)));</span>
    <span style="color: #666666; font-style: italic;">//设定背景</span>
    chart.<span style="color: #006633;">setBackgroundPaint</span><span style="color: #009900;">&#40;</span><span style="color: #003399;">Color</span>.<span style="color: #006633;">white</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">//chart.s</span>
    <span style="color: #666666; font-style: italic;">//饼图使用一个PiePlot </span>
    PiePlot pie <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span>PiePlot<span style="color: #009900;">&#41;</span>chart.<span style="color: #006633;">getPlot</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">//pie.setSectionLabelType(PiePlot.NAME_AND_PERCENT_LABELS);</span>
    pie.<span style="color: #006633;">setSectionLabelType</span><span style="color: #009900;">&#40;</span>PiePlot.<span style="color: #006633;">NAME_AND_VALUE_LABELS</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">//设定显示格式(名称加百分比或数值)</span>
    pie.<span style="color: #006633;">setPercentFormatString</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;#,###0.0#%&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">//设定百分比显示格式</span>
    pie.<span style="color: #006633;">setBackgroundPaint</span><span style="color: #009900;">&#40;</span><span style="color: #003399;">Color</span>.<span style="color: #006633;">white</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    pie.<span style="color: #006633;">setSectionLabelFont</span><span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">Font</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;黑体&quot;</span>, <span style="color: #003399;">Font</span>.<span style="color: #006633;">TRUETYPE_FONT</span>, <span style="color: #cc66cc;">12</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">//设定背景透明度（0-1.0之间）</span>
    pie.<span style="color: #006633;">setBackgroundAlpha</span><span style="color: #009900;">&#40;</span>0.6f<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">//设定前景透明度（0-1.0之间）</span>
    pie.<span style="color: #006633;">setForegroundAlpha</span><span style="color: #009900;">&#40;</span>0.90f<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">//输出文件到指定目录</span>
    <span style="color: #003399;">String</span> rfname <span style="color: #339933;">=</span> MathUtil.<span style="color: #006633;">getRoundCode</span><span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">12</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot;.jpeg&quot;</span><span style="color: #339933;">;</span>
    <span style="color: #003399;">String</span> fileName <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;d:/test/&quot;</span> <span style="color: #339933;">+</span> rfname<span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #666666; font-style: italic;">//可以保存文件为jpg或png格式。</span>
    ChartUtilities.<span style="color: #006633;">saveChartAsJPEG</span><span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">File</span><span style="color: #009900;">&#40;</span>fileName<span style="color: #009900;">&#41;</span>, <span style="color: #cc66cc;">100</span>, chart, <span style="color: #cc66cc;">600</span>, <span style="color: #cc66cc;">600</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">//第一个参数为文件名</span>
    <span style="color: #666666; font-style: italic;">//第二个参数质量</span>
    <span style="color: #666666; font-style: italic;">//第三个参数为哪个chart创建图片</span>
    <span style="color: #666666; font-style: italic;">//第四个宽度</span>
    <span style="color: #666666; font-style: italic;">//第五个高度</span>
    <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">IOException</span> exz<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">print</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;....Cant't Create image File&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">//图片标题
    String title = &quot;空调2002年市场占有率&quot;;
    //设定数据源
    DefaultPieDataset piedata = new DefaultPieDataset();
    //第一个参数为名称，第二个参数是double数
    piedata.setValue(&quot;联想&quot;, 27.3);
    piedata.setValue(&quot;长城&quot;, 12.2);
    piedata.setValue(&quot;海尔&quot;, 5.5);
    piedata.setValue(&quot;美的&quot;, 17.1);
    piedata.setValue(&quot;松下&quot;, 9.0);
    piedata.setValue(&quot;科龙&quot;, 19.0);
    //创建JFreeChart，都使用ChartFactory来创建JFreeChart,很标准的工厂设计模式
    JFreeChart chart =
    ChartFactory.createPieChart(title, piedata, true, true, true);
    //设定图片标题
    chart.setTitle(new TextTitle(title, new Font(&quot;隶书&quot;, Font.ITALIC, 15)));
    //chart.addSubtitle(new TextTitle(&quot;2002财年分析&quot;, new Font(&quot;隶书&quot;, Font.ITALIC, 12)));
    //设定背景
    chart.setBackgroundPaint(Color.white);
    //chart.s
    //饼图使用一个PiePlot 
    PiePlot pie = (PiePlot)chart.getPlot();
    //pie.setSectionLabelType(PiePlot.NAME_AND_PERCENT_LABELS);
    pie.setSectionLabelType(PiePlot.NAME_AND_VALUE_LABELS);
    //设定显示格式(名称加百分比或数值)
    pie.setPercentFormatString(&quot;#,###0.0#%&quot;);
    //设定百分比显示格式
    pie.setBackgroundPaint(Color.white);
    pie.setSectionLabelFont(new Font(&quot;黑体&quot;, Font.TRUETYPE_FONT, 12));
    //设定背景透明度（0-1.0之间）
    pie.setBackgroundAlpha(0.6f);
    //设定前景透明度（0-1.0之间）
    pie.setForegroundAlpha(0.90f);
    //输出文件到指定目录
    String rfname = MathUtil.getRoundCode(12) + &quot;.jpeg&quot;;
    String fileName = &quot;d:/test/&quot; + rfname;
    try {
    //可以保存文件为jpg或png格式。
    ChartUtilities.saveChartAsJPEG(new File(fileName), 100, chart, 600, 600);
    //第一个参数为文件名
    //第二个参数质量
    //第三个参数为哪个chart创建图片
    //第四个宽度
    //第五个高度
    } catch (IOException exz) {
    System.out.print(&quot;....Cant't Create image File&quot;);
    }</p></div>
    ";i:2;s:18763:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #666666; font-style: italic;">// create a default chart based on some sample data...</span>
    <span style="color: #666666; font-style: italic;">//曲线图标题</span>
    <span style="color: #003399;">String</span> title <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;趋势分析&quot;</span><span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">//曲线图X轴提示</span>
    <span style="color: #003399;">String</span> domain <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;月份走势&quot;</span><span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">//曲线图Y轴提示</span>
    <span style="color: #003399;">String</span> range <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;应收余额&quot;</span><span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">//曲线图自标题</span>
    <span style="color: #003399;">String</span> subtitleStr <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;2003财年分析&quot;</span><span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">//创建时间数据源</span>
    <span style="color: #666666; font-style: italic;">//每一个TimeSeries在图上是一条曲线</span>
    TimeSeries ca <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> TimeSeries<span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;用友&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> i <span style="color: #339933;">=</span> <span style="color: #cc66cc;">1999</span><span style="color: #339933;">;</span> i <span style="color: #339933;">&lt;</span> <span style="color: #cc66cc;">2005</span><span style="color: #339933;">;</span> i<span style="color: #339933;">++</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> mon <span style="color: #339933;">=</span> <span style="color: #cc66cc;">0</span><span style="color: #339933;">;</span> mon <span style="color: #339933;">&lt;</span> <span style="color: #cc66cc;">12</span><span style="color: #339933;">;</span> mon<span style="color: #339933;">++</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #666666; font-style: italic;">//ca.add(new Month(mon + 1, i), new Double(500 + Math.random() * 100));</span>
    <span style="color: #666666; font-style: italic;">//TimeSeriesDataPair是一个时间点的数值体现</span>
    ca.<span style="color: #006633;">add</span><span style="color: #009900;">&#40;</span>
    <span style="color: #000000; font-weight: bold;">new</span> TimeSeriesDataPair<span style="color: #009900;">&#40;</span>
    <span style="color: #000000; font-weight: bold;">new</span> Day<span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">1</span>, mon <span style="color: #339933;">+</span> <span style="color: #cc66cc;">1</span>, i<span style="color: #009900;">&#41;</span>,
    <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">Double</span><span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">500</span> <span style="color: #339933;">+</span> <span style="color: #003399;">Math</span>.<span style="color: #006633;">random</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">*</span> <span style="color: #cc66cc;">100</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span>
    &nbsp;
    TimeSeries ibm <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> TimeSeries<span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;金碟&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> i <span style="color: #339933;">=</span> <span style="color: #cc66cc;">1999</span><span style="color: #339933;">;</span> i <span style="color: #339933;">&lt;</span> <span style="color: #cc66cc;">2005</span><span style="color: #339933;">;</span> i<span style="color: #339933;">++</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> mon <span style="color: #339933;">=</span> <span style="color: #cc66cc;">0</span><span style="color: #339933;">;</span> mon <span style="color: #339933;">&lt;</span> <span style="color: #cc66cc;">12</span><span style="color: #339933;">;</span> mon<span style="color: #339933;">++</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #666666; font-style: italic;">//ibm.add(new Month(mon+1,i),new Double(400-Math.random()*100));</span>
    ibm.<span style="color: #006633;">add</span><span style="color: #009900;">&#40;</span>
    <span style="color: #000000; font-weight: bold;">new</span> TimeSeriesDataPair<span style="color: #009900;">&#40;</span>
    <span style="color: #000000; font-weight: bold;">new</span> Day<span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">1</span>, mon <span style="color: #339933;">+</span> <span style="color: #cc66cc;">1</span>, i<span style="color: #009900;">&#41;</span>,
    <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">Double</span><span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">400</span> <span style="color: #339933;">-</span> <span style="color: #003399;">Math</span>.<span style="color: #006633;">random</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">*</span> <span style="color: #cc66cc;">100</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span>
    &nbsp;
    TimeSeries king <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> TimeSeries<span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;东软&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> i <span style="color: #339933;">=</span> <span style="color: #cc66cc;">1999</span><span style="color: #339933;">;</span> i <span style="color: #339933;">&lt;</span> <span style="color: #cc66cc;">2005</span><span style="color: #339933;">;</span> i<span style="color: #339933;">++</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> mon <span style="color: #339933;">=</span> <span style="color: #cc66cc;">0</span><span style="color: #339933;">;</span> mon <span style="color: #339933;">&lt;</span> <span style="color: #cc66cc;">12</span><span style="color: #339933;">;</span> mon<span style="color: #339933;">++</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #666666; font-style: italic;">//ibm.add(new Month(mon+1,i),new Double(400-Math.random()*100));</span>
    king.<span style="color: #006633;">add</span><span style="color: #009900;">&#40;</span>
    <span style="color: #000000; font-weight: bold;">new</span> TimeSeriesDataPair<span style="color: #009900;">&#40;</span>
    <span style="color: #000000; font-weight: bold;">new</span> Day<span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">1</span>, mon <span style="color: #339933;">+</span> <span style="color: #cc66cc;">1</span>, i<span style="color: #009900;">&#41;</span>,
    <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">Double</span><span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">300</span> <span style="color: #339933;">-</span> <span style="color: #003399;">Math</span>.<span style="color: #006633;">random</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">*</span> <span style="color: #cc66cc;">100</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span>
    <span style="color: #666666; font-style: italic;">//时间曲线数据集合</span>
    TimeSeriesCollection dataset <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> TimeSeriesCollection<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    dataset.<span style="color: #006633;">addSeries</span><span style="color: #009900;">&#40;</span>ca<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    dataset.<span style="color: #006633;">addSeries</span><span style="color: #009900;">&#40;</span>ibm<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    dataset.<span style="color: #006633;">addSeries</span><span style="color: #009900;">&#40;</span>king<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">//dataset.addSeries(jpy);</span>
    <span style="color: #666666; font-style: italic;">//dataset.addSeries(mav);</span>
    <span style="color: #666666; font-style: italic;">//时间曲线元素</span>
    JFreeChart chart <span style="color: #339933;">=</span>
    ChartFactory.<span style="color: #006633;">createTimeSeriesChart</span><span style="color: #009900;">&#40;</span>
    title,
    domain,
    range,
    dataset,
    <span style="color: #000066; font-weight: bold;">true</span>,
    <span style="color: #000066; font-weight: bold;">true</span>,
    <span style="color: #000066; font-weight: bold;">false</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">// then customise it a little...</span>
    TextTitle subtitle <span style="color: #339933;">=</span>
    <span style="color: #000000; font-weight: bold;">new</span> TextTitle<span style="color: #009900;">&#40;</span>subtitleStr, <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">Font</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;黑体&quot;</span>, <span style="color: #003399;">Font</span>.<span style="color: #006633;">BOLD</span>, <span style="color: #cc66cc;">12</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    chart.<span style="color: #006633;">addSubtitle</span><span style="color: #009900;">&#40;</span>subtitle<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    chart.<span style="color: #006633;">setTitle</span><span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">new</span> TextTitle<span style="color: #009900;">&#40;</span>title, <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">Font</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;隶书&quot;</span>, <span style="color: #003399;">Font</span>.<span style="color: #006633;">ITALIC</span>, <span style="color: #cc66cc;">15</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">//pie.setSeriesLabelFont(new Font(&quot;黑体&quot;, Font.BOLD, 15));</span>
    chart.<span style="color: #006633;">setBackgroundPaint</span><span style="color: #009900;">&#40;</span>
    <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">GradientPaint</span><span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">0</span>, <span style="color: #cc66cc;">0</span>, <span style="color: #003399;">Color</span>.<span style="color: #006633;">white</span>, <span style="color: #cc66cc;">0</span>, <span style="color: #cc66cc;">1000</span>, <span style="color: #003399;">Color</span>.<span style="color: #006633;">blue</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">//sysout</span>
    <span style="color: #666666; font-style: italic;">//输出文件到指定目录</span>
    <span style="color: #003399;">String</span> rfname <span style="color: #339933;">=</span> MathUtil.<span style="color: #006633;">getRoundCode</span><span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">22</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot;.jpeg&quot;</span><span style="color: #339933;">;</span>
    <span style="color: #003399;">String</span> fileName <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;d:/test/&quot;</span> <span style="color: #339933;">+</span> rfname<span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #666666; font-style: italic;">//for</span>
    <span style="color: #666666; font-style: italic;">//System.out.println();</span>
    ChartUtilities.<span style="color: #006633;">saveChartAsJPEG</span><span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">File</span><span style="color: #009900;">&#40;</span>fileName<span style="color: #009900;">&#41;</span>, <span style="color: #cc66cc;">100</span>, chart, <span style="color: #cc66cc;">600</span>, <span style="color: #cc66cc;">600</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">// log.info(&quot;....Create image File:&quot; + fileName);</span>
    <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">IOException</span> exz<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">print</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;....Cant't Create image File&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">// create a default chart based on some sample data...
    //曲线图标题
    String title = &quot;趋势分析&quot;;
    //曲线图X轴提示
    String domain = &quot;月份走势&quot;;
    //曲线图Y轴提示
    String range = &quot;应收余额&quot;;
    //曲线图自标题
    String subtitleStr = &quot;2003财年分析&quot;;
    //创建时间数据源
    //每一个TimeSeries在图上是一条曲线
    TimeSeries ca = new TimeSeries(&quot;用友&quot;);
    for (int i = 1999; i &lt; 2005; i++) {
    for (int mon = 0; mon &lt; 12; mon++) {
    //ca.add(new Month(mon + 1, i), new Double(500 + Math.random() * 100));
    //TimeSeriesDataPair是一个时间点的数值体现
    ca.add(
    new TimeSeriesDataPair(
    new Day(1, mon + 1, i),
    new Double(500 + Math.random() * 100)));
    }
    }
    
    TimeSeries ibm = new TimeSeries(&quot;金碟&quot;);
    for (int i = 1999; i &lt; 2005; i++) {
    for (int mon = 0; mon &lt; 12; mon++) {
    //ibm.add(new Month(mon+1,i),new Double(400-Math.random()*100));
    ibm.add(
    new TimeSeriesDataPair(
    new Day(1, mon + 1, i),
    new Double(400 - Math.random() * 100)));
    }
    }
    
    TimeSeries king = new TimeSeries(&quot;东软&quot;);
    for (int i = 1999; i &lt; 2005; i++) {
    for (int mon = 0; mon &lt; 12; mon++) {
    //ibm.add(new Month(mon+1,i),new Double(400-Math.random()*100));
    king.add(
    new TimeSeriesDataPair(
    new Day(1, mon + 1, i),
    new Double(300 - Math.random() * 100)));
    }
    }
    //时间曲线数据集合
    TimeSeriesCollection dataset = new TimeSeriesCollection();
    dataset.addSeries(ca);
    dataset.addSeries(ibm);
    dataset.addSeries(king);
    //dataset.addSeries(jpy);
    //dataset.addSeries(mav);
    //时间曲线元素
    JFreeChart chart =
    ChartFactory.createTimeSeriesChart(
    title,
    domain,
    range,
    dataset,
    true,
    true,
    false);
    // then customise it a little...
    TextTitle subtitle =
    new TextTitle(subtitleStr, new Font(&quot;黑体&quot;, Font.BOLD, 12));
    chart.addSubtitle(subtitle);
    chart.setTitle(new TextTitle(title, new Font(&quot;隶书&quot;, Font.ITALIC, 15)));
    //pie.setSeriesLabelFont(new Font(&quot;黑体&quot;, Font.BOLD, 15));
    chart.setBackgroundPaint(
    new GradientPaint(0, 0, Color.white, 0, 1000, Color.blue));
    //sysout
    //输出文件到指定目录
    String rfname = MathUtil.getRoundCode(22) + &quot;.jpeg&quot;;
    String fileName = &quot;d:/test/&quot; + rfname;
    try {
    //for
    //System.out.println();
    ChartUtilities.saveChartAsJPEG(new File(fileName), 100, chart, 600, 600);
    // log.info(&quot;....Create image File:&quot; + fileName);
    } catch (IOException exz) {
    System.out.print(&quot;....Cant't Create image File&quot;);
    }</p></div>
    ";i:3;s:11756:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #003399;">String</span> title <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;柱状图测试&quot;</span><span style="color: #339933;">;</span>
    <span style="color: #003399;">String</span> domain <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;单位比较&quot;</span><span style="color: #339933;">;</span>
    <span style="color: #003399;">String</span> range <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;数值&quot;</span><span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">//CategoryDataset data = DemoDatasetFactory.createCategoryDataset();</span>
    DefaultCategoryDataset data <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> DefaultCategoryDataset<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> r <span style="color: #339933;">=</span> <span style="color: #cc66cc;">0</span><span style="color: #339933;">;</span> r <span style="color: #339933;">&lt;</span> <span style="color: #cc66cc;">5</span><span style="color: #339933;">;</span> r<span style="color: #339933;">++</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #003399;">String</span> rowKey <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;单位 [&quot;</span> <span style="color: #339933;">+</span> <span style="color: #009900;">&#40;</span>r <span style="color: #339933;">+</span> <span style="color: #cc66cc;">1</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">+</span><span style="color: #0000ff;">&quot;]&quot;</span> <span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">//第一层循环：分析对象</span>
    <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> c <span style="color: #339933;">=</span> <span style="color: #cc66cc;">0</span><span style="color: #339933;">;</span> c <span style="color: #339933;">&lt;</span> <span style="color: #cc66cc;">6</span><span style="color: #339933;">;</span> c<span style="color: #339933;">++</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #666666; font-style: italic;">//第二层循环：分析对象在时间点上的数据</span>
    <span style="color: #003399;">String</span> columnKey <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;2001年&quot;</span> <span style="color: #339933;">+</span> <span style="color: #009900;">&#40;</span>c <span style="color: #339933;">+</span> <span style="color: #cc66cc;">1</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot;月&quot;</span><span style="color: #339933;">;</span>
    data.<span style="color: #006633;">addValue</span><span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">Double</span><span style="color: #009900;">&#40;</span>r <span style="color: #339933;">*</span> c <span style="color: #339933;">+</span> <span style="color: #cc66cc;">5</span><span style="color: #009900;">&#41;</span>, rowKey, columnKey<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span>
    &nbsp;
    JFreeChart chart <span style="color: #339933;">=</span>
    ChartFactory.<span style="color: #006633;">createVerticalBarChart</span><span style="color: #009900;">&#40;</span>
    title,
    domain,
    range,
    data,
    <span style="color: #000066; font-weight: bold;">true</span>,
    <span style="color: #000066; font-weight: bold;">true</span>,
    <span style="color: #000066; font-weight: bold;">false</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">// then customise it a little...</span>
    chart.<span style="color: #006633;">setBackgroundPaint</span><span style="color: #009900;">&#40;</span>
    <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">GradientPaint</span><span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">0</span>, <span style="color: #cc66cc;">0</span>, <span style="color: #003399;">Color</span>.<span style="color: #006633;">white</span>, <span style="color: #cc66cc;">1000</span>, <span style="color: #cc66cc;">0</span>, <span style="color: #003399;">Color</span>.<span style="color: #006633;">red</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    chart.<span style="color: #006633;">setTitle</span><span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">new</span> TextTitle<span style="color: #009900;">&#40;</span>title, <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">Font</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;隶书&quot;</span>, <span style="color: #003399;">Font</span>.<span style="color: #006633;">ITALIC</span>, <span style="color: #cc66cc;">15</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    CategoryPlot plot <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span>CategoryPlot<span style="color: #009900;">&#41;</span>chart.<span style="color: #006633;">getPlot</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    plot.<span style="color: #006633;">setForegroundAlpha</span><span style="color: #009900;">&#40;</span>0.9f<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    plot.<span style="color: #006633;">setValueLabelFont</span><span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">Font</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;黑体&quot;</span>, <span style="color: #003399;">Font</span>.<span style="color: #006633;">TRUETYPE_FONT</span>, <span style="color: #cc66cc;">12</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">//plot.setSectionLabelFont(new Font(&quot;黑体&quot;, Font.TRUETYPE_FONT, 12));</span>
    <span style="color: #666666; font-style: italic;">//注意以下代码</span>
    NumberAxis verticalAxis <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span>NumberAxis<span style="color: #009900;">&#41;</span>plot.<span style="color: #006633;">getRangeAxis</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    verticalAxis.<span style="color: #006633;">setStandardTickUnits</span><span style="color: #009900;">&#40;</span>NumberAxis.<span style="color: #006633;">createIntegerTickUnits</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">// 输出文件到指定目录</span>
    <span style="color: #003399;">String</span> rfname <span style="color: #339933;">=</span> MathUtil.<span style="color: #006633;">getRoundCode</span><span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">22</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot;b.jpeg&quot;</span><span style="color: #339933;">;</span>
    <span style="color: #003399;">String</span> fileName <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;d:/test/&quot;</span> <span style="color: #339933;">+</span> rfname<span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#123;</span>
    ChartUtilities.<span style="color: #006633;">saveChartAsJPEG</span><span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">File</span><span style="color: #009900;">&#40;</span>fileName<span style="color: #009900;">&#41;</span>, <span style="color: #cc66cc;">100</span>, chart, <span style="color: #cc66cc;">600</span>, <span style="color: #cc66cc;">600</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #666666; font-style: italic;">// log.info(&quot;....Create image File:&quot; + fileName);</span>
    <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">IOException</span> exz<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">print</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;....Cant't Create image File&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">String title = &quot;柱状图测试&quot;;
    String domain = &quot;单位比较&quot;;
    String range = &quot;数值&quot;;
    //CategoryDataset data = DemoDatasetFactory.createCategoryDataset();
    DefaultCategoryDataset data = new DefaultCategoryDataset();
    for (int r = 0; r &lt; 5; r++) {
    String rowKey = &quot;单位 [&quot; + (r + 1)+&quot;]&quot; ;
    //第一层循环：分析对象
    for (int c = 0; c &lt; 6; c++) {
    //第二层循环：分析对象在时间点上的数据
    String columnKey = &quot;2001年&quot; + (c + 1) + &quot;月&quot;;
    data.addValue(new Double(r * c + 5), rowKey, columnKey);
    }
    }
    
    JFreeChart chart =
    ChartFactory.createVerticalBarChart(
    title,
    domain,
    range,
    data,
    true,
    true,
    false);
    // then customise it a little...
    chart.setBackgroundPaint(
    new GradientPaint(0, 0, Color.white, 1000, 0, Color.red));
    chart.setTitle(new TextTitle(title, new Font(&quot;隶书&quot;, Font.ITALIC, 15)));
    CategoryPlot plot = (CategoryPlot)chart.getPlot();
    plot.setForegroundAlpha(0.9f);
    plot.setValueLabelFont(new Font(&quot;黑体&quot;, Font.TRUETYPE_FONT, 12));
    //plot.setSectionLabelFont(new Font(&quot;黑体&quot;, Font.TRUETYPE_FONT, 12));
    //注意以下代码
    NumberAxis verticalAxis = (NumberAxis)plot.getRangeAxis();
    verticalAxis.setStandardTickUnits(NumberAxis.createIntegerTickUnits());
    // 输出文件到指定目录
    String rfname = MathUtil.getRoundCode(22) + &quot;b.jpeg&quot;;
    String fileName = &quot;d:/test/&quot; + rfname;
    try {
    ChartUtilities.saveChartAsJPEG(new File(fileName), 100, chart, 600, 600);
    // log.info(&quot;....Create image File:&quot; + fileName);
    } catch (IOException exz) {
    System.out.print(&quot;....Cant't Create image File&quot;);
    }</p></div>
    ";}
categories:
  - J2EE
tags:
  - jfreechart

---
以下文章介绍JFreeChart的使用方法。  
文章来源：http://hi.baidu.com/baileyfu/blog/item/8e75b212b47fea54f819b808.html  
<!--more-->

一：jfreechart介绍  
jfreechart是一个免费创建图片的java工具.可以创建如下图形：  
饼图(pie charts;)  
曲线图(line charts )  
柱状图(horizontal/vertical bar charts)  
甘特图(Gantt charts; )  
XY plots and scatter plots;  
time series, high/low/open/close charts and candle stick charts;  
combination charts;  
Pareto charts;  
bubble charts;  
wind plots, meter charts and symbol charts;  
从以下地址可以看到jfreechart可以创建的图形类型  
http://www.jfree.org/jfreechart/samples.html  
sourceforge有一个基于jfreechart的项目Cewolf可以很方便的在jsp/servlet中创建图片  
jfreechart目前(2003-05-08)版本为0.98  
希望得到详细的信息或下载jfreechart请访问如下站点:  
http://www.jfree.org/jfreechart/
二：特别说明:  
jfreechart是一个开源项目，但是文档是需要40美金去购买的。  
还有一个很重要的问题,jfreechart如果使用中文，他使用的默认字体  
显示出来的中文会很模糊，你可能需要修改源代码。  
下面我就举几个简单的例子说明一下如何使用jfreechart创建图片  
在开发中有可能会导入以下的类  
import com.jrefinery.chart.ChartFactory;  
import com.jrefinery.chart.ChartUtilities;  
import com.jrefinery.chart.JFreeChart;  
import com.jrefinery.chart.TextTitle;  
import com.jrefinery.chart.axis.NumberAxis;  
import com.jrefinery.chart.plot.CategoryPlot;  
import com.jrefinery.chart.plot.PiePlot;  
import com.jrefinery.data.Day;  
import com.jrefinery.data.DefaultCategoryDataset;  
import com.jrefinery.data.DefaultPieDataset;  
import com.jrefinery.data.TimeSeries;  
import com.jrefinery.data.TimeSeriesCollection;  
import com.jrefinery.data.TimeSeriesDataPair;  
在0.98以后包由com.jrefinery.*改变为:org.jfree
三：创建饼图
<pre escaped="true" lang="java">//图片标题
String title = "空调2002年市场占有率";
//设定数据源
DefaultPieDataset piedata = new DefaultPieDataset();
//第一个参数为名称，第二个参数是double数
piedata.setValue("联想", 27.3);
piedata.setValue("长城", 12.2);
piedata.setValue("海尔", 5.5);
piedata.setValue("美的", 17.1);
piedata.setValue("松下", 9.0);
piedata.setValue("科龙", 19.0);
//创建JFreeChart，都使用ChartFactory来创建JFreeChart,很标准的工厂设计模式
JFreeChart chart =
ChartFactory.createPieChart(title, piedata, true, true, true);
//设定图片标题
chart.setTitle(new TextTitle(title, new Font("隶书", Font.ITALIC, 15)));
//chart.addSubtitle(new TextTitle("2002财年分析", new Font("隶书", Font.ITALIC, 12)));
//设定背景
chart.setBackgroundPaint(Color.white);
//chart.s
//饼图使用一个PiePlot 
PiePlot pie = (PiePlot)chart.getPlot();
//pie.setSectionLabelType(PiePlot.NAME_AND_PERCENT_LABELS);
pie.setSectionLabelType(PiePlot.NAME_AND_VALUE_LABELS);
//设定显示格式(名称加百分比或数值)
pie.setPercentFormatString("#,###0.0#%");
//设定百分比显示格式
pie.setBackgroundPaint(Color.white);
pie.setSectionLabelFont(new Font("黑体", Font.TRUETYPE_FONT, 12));
//设定背景透明度（0-1.0之间）
pie.setBackgroundAlpha(0.6f);
//设定前景透明度（0-1.0之间）
pie.setForegroundAlpha(0.90f);
//输出文件到指定目录
String rfname = MathUtil.getRoundCode(12) + ".jpeg";
String fileName = "d:/test/" + rfname;
try {
//可以保存文件为jpg或png格式。
ChartUtilities.saveChartAsJPEG(new File(fileName), 100, chart, 600, 600);
//第一个参数为文件名
//第二个参数质量
//第三个参数为哪个chart创建图片
//第四个宽度
//第五个高度
} catch (IOException exz) {
System.out.print("....Cant't Create image File");
}
</pre>
其实使用JFreeChart创建图片很简单，不同的的图片类型区别在于设置数据集
四：创建曲线图
<pre escaped="true" lang="java">// create a default chart based on some sample data...
//曲线图标题
String title = "趋势分析";
//曲线图X轴提示
String domain = "月份走势";
//曲线图Y轴提示
String range = "应收余额";
//曲线图自标题
String subtitleStr = "2003财年分析";
//创建时间数据源
//每一个TimeSeries在图上是一条曲线
TimeSeries ca = new TimeSeries("用友");
for (int i = 1999; i &lt; 2005; i++) {
for (int mon = 0; mon &lt; 12; mon++) {
//ca.add(new Month(mon + 1, i), new Double(500 + Math.random() * 100));
//TimeSeriesDataPair是一个时间点的数值体现
ca.add(
new TimeSeriesDataPair(
new Day(1, mon + 1, i),
new Double(500 + Math.random() * 100)));
}
}

TimeSeries ibm = new TimeSeries("金碟");
for (int i = 1999; i &lt; 2005; i++) {
for (int mon = 0; mon &lt; 12; mon++) {
//ibm.add(new Month(mon+1,i),new Double(400-Math.random()*100));
ibm.add(
new TimeSeriesDataPair(
new Day(1, mon + 1, i),
new Double(400 - Math.random() * 100)));
}
}

TimeSeries king = new TimeSeries("东软");
for (int i = 1999; i &lt; 2005; i++) {
for (int mon = 0; mon &lt; 12; mon++) {
//ibm.add(new Month(mon+1,i),new Double(400-Math.random()*100));
king.add(
new TimeSeriesDataPair(
new Day(1, mon + 1, i),
new Double(300 - Math.random() * 100)));
}
}
//时间曲线数据集合
TimeSeriesCollection dataset = new TimeSeriesCollection();
dataset.addSeries(ca);
dataset.addSeries(ibm);
dataset.addSeries(king);
//dataset.addSeries(jpy);
//dataset.addSeries(mav);
//时间曲线元素
JFreeChart chart =
ChartFactory.createTimeSeriesChart(
title,
domain,
range,
dataset,
true,
true,
false);
// then customise it a little...
TextTitle subtitle =
new TextTitle(subtitleStr, new Font("黑体", Font.BOLD, 12));
chart.addSubtitle(subtitle);
chart.setTitle(new TextTitle(title, new Font("隶书", Font.ITALIC, 15)));
//pie.setSeriesLabelFont(new Font("黑体", Font.BOLD, 15));
chart.setBackgroundPaint(
new GradientPaint(0, 0, Color.white, 0, 1000, Color.blue));
//sysout
//输出文件到指定目录
String rfname = MathUtil.getRoundCode(22) + ".jpeg";
String fileName = "d:/test/" + rfname;
try {
//for
//System.out.println();
ChartUtilities.saveChartAsJPEG(new File(fileName), 100, chart, 600, 600);
// log.info("....Create image File:" + fileName);
} catch (IOException exz) {
System.out.print("....Cant't Create image File");
}</pre>
五：创建柱状图
<pre escaped="true" lang="java">String title = "柱状图测试";
String domain = "单位比较";
String range = "数值";
//CategoryDataset data = DemoDatasetFactory.createCategoryDataset();
DefaultCategoryDataset data = new DefaultCategoryDataset();
for (int r = 0; r &lt; 5; r++) {
String rowKey = "单位 [" + (r + 1)+"]" ;
//第一层循环：分析对象
for (int c = 0; c &lt; 6; c++) {
//第二层循环：分析对象在时间点上的数据
String columnKey = "2001年" + (c + 1) + "月";
data.addValue(new Double(r * c + 5), rowKey, columnKey);
}
}

JFreeChart chart =
ChartFactory.createVerticalBarChart(
title,
domain,
range,
data,
true,
true,
false);
// then customise it a little...
chart.setBackgroundPaint(
new GradientPaint(0, 0, Color.white, 1000, 0, Color.red));
chart.setTitle(new TextTitle(title, new Font("隶书", Font.ITALIC, 15)));
CategoryPlot plot = (CategoryPlot)chart.getPlot();
plot.setForegroundAlpha(0.9f);
plot.setValueLabelFont(new Font("黑体", Font.TRUETYPE_FONT, 12));
//plot.setSectionLabelFont(new Font("黑体", Font.TRUETYPE_FONT, 12));
//注意以下代码
NumberAxis verticalAxis = (NumberAxis)plot.getRangeAxis();
verticalAxis.setStandardTickUnits(NumberAxis.createIntegerTickUnits());
// 输出文件到指定目录
String rfname = MathUtil.getRoundCode(22) + "b.jpeg";
String fileName = "d:/test/" + rfname;
try {
ChartUtilities.saveChartAsJPEG(new File(fileName), 100, chart, 600, 600);
// log.info("....Create image File:" + fileName);
} catch (IOException exz) {
System.out.print("....Cant't Create image File");
}
</pre>
六：结束语  
个人感觉JFreeChart可以满足大部分图片创建的需要，美中不足的是：对字体的设置做的  
不 够好，特别是使用中文的时候字体很不清晰。因为这个原因建议你自己去修改他的源代码,最好使用properties文件去设置字体.还有就是文档要钱所以 要多花点时间去看源代码。或多上社区.因为时间等原因我只介绍了三种图片的创建，其他类型的图片可以参考jfreechart提供的例子。