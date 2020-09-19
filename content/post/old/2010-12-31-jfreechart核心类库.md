---
title: JFreeChart核心类库介绍
author: fatkun
type: post
date: 2010-12-31T05:54:44+00:00
url: /2010/12/jfreechart核心类库.html
duoshuo_thread_id:
  - 6300408796523004674
categories:
  - J2EE
tags:
  - jfreechart
  - XY轴

---
以下内容包括了如何调整XY轴数值间隔
原文来自：<http://hi.baidu.com/baileyfu/blog/item/8e75b212b47fea54f819b808.html>
<!--more-->

jfreechart主要由两个大的包组成：org.jfree.chart,org.jfree.data。其中前者主要与图形
<div>  &nbsp;</div>
<div>  本身有关，后者与图形显示的数据有关。</div>
<div>  &nbsp;</div>
## 核心类主要有：

<div>  &nbsp;</div>
<div>  org.jfree.chart.JFreeChart：图表对象，任何类型的图表的最终表现形式都是在该对象进行一些属性的定制。JFreeChart引擎本身提供了一个工厂类用于创建不同类型的图表对象</div>
<div>  &nbsp;</div>
<div>  org.jfree.data.category.XXXDataSet:数据集对象，用于提供显示图表所用的数据。根据不同类型的图表对应着很多类型的数据集对象类</div>
<div>  &nbsp;</div>
<div>  org.jfree.chart.plot.XXXPlot：图表区域对象，基本上这个对象决定着什么样式的图表，创建该对象的时候需要Axis、Renderer以及数据集对象的支持</div>
<div>  &nbsp;</div>
<div>  org.jfree.chart.axis.XXXAxis：用于处理图表的两个轴：纵轴和横轴</div>
<div>  &nbsp;</div>
<div>  org.jfree.chart.render.XXXRender：负责如何显示一个图表对象</div>
<div>  &nbsp;</div>
<div>  org.jfree.chart.urls.XXXURLGenerator:用于生成Web图表中每个项目的鼠标点击链接</div>
<div>  &nbsp;</div>
<div>  XXXXXToolTipGenerator:用于生成图象的帮助提示，不同类型图表对应不同类型的工具提示类</div>
<div>  &nbsp;</div>
<div>  对于常用的饼图阖柱状图，比较简单而且网上有很多的文章介绍，在这里就不再一一复述了，</div>
<div>  &nbsp;</div>
<div>  主要说明下另一种常见的报表，时序图，首先声明一个曲线数据集合对象和曲线对象</div>
<div>  &nbsp;</div>
<div>  TimePeriodValuesCollection timeseriescollection = new TimePeriodValuesCollection();</div>
<div>  &nbsp;</div>
<div>  //声明具体是曲线对象，(可根据实际情况在同一张图中显示多条曲线进行数据比对，根据实际应用情况当超过4条曲线时，就会有些乱。)</div>
<div>  &nbsp;</div>
<div>  TimePeriodValues timeperiod1 = new TimePeriodValues("服务器A在线用户数量");</div>
<div>  &nbsp;</div>
<div>  TimePeriodValues timeperiod2 = new TimePeriodValues("服务器B在线用户数量");</div>
<div>  &nbsp;</div>
<div>  我在使用TimeSeriesCollection tsc = new TimeSeriesCollection();</div>
<div>  &nbsp;</div>
<div>  TimeSeries ts = new TimeSeries();</div>
<div>  &nbsp;</div>
<div>  在生成数据集时（ts.add(new Day(day, month, year),10))）只能生成最小单位为天的横轴所以改用了TimePeriodValuesCollection</div>
<div>  &nbsp;</div>
<div>  //根据当前时间取得横轴坐标，时间间隔为1小时</div>
<div>  &nbsp;</div>
<div>  Calendar cal = Calendar.getInstance();</div>
<div>  &nbsp;</div>
<div>  int year = cal.get(Calendar.YEAR);</div>
<div>  &nbsp;</div>
<div>  int month = cal.get(Calendar.MONTH) + 1;</div>
<div>  &nbsp;</div>
<div>  int day = cal.get(Calendar.DAY_OF_MONTH);</div>
<div>  &nbsp;</div>
<div>  //这里改为根据自己程序得到的需要显示的时间点和对应的数据的集合;</div>
<div>  &nbsp;</div>
<div>  List objectList1 = dao.getList1();</div>
<div>  &nbsp;</div>
<div>  List objectList2 = dao.getList2();</div>
<div>  &nbsp;</div>
<div>  //使用循环，把x轴，y轴的值赋给timeseries1</div>
<div>  &nbsp;</div>
<div>  for (int i =0;i<objecthash1.size();i++) {</div>
<div>  &nbsp;</div>
<div>  &nbsp;&nbsp; &nbsp; int hour = objecthash1[i].getHours();</div>
<div>  &nbsp;</div>
<div>  &nbsp;&nbsp; &nbsp; int count = objecthash1[i].getCount();</div>
<div>  &nbsp;</div>
<div>  //将每一对数据（时间，数值）添加到数据集合1(曲线对象1)中</div>
<div>  &nbsp;</div>
<div>  &nbsp;&nbsp; &nbsp; timeseries1.add(new Hour(hour, day, month, year),count);</div>
<div>  &nbsp;</div>
<div>  }</div>
<div>  &nbsp;</div>
<div>  for (int i =0;i<objecthash2.size();i++) {</div>
<div>  &nbsp;</div>
<div>  &nbsp;&nbsp; &nbsp; int hour = objecthash2[i].getHours();</div>
<div>  &nbsp;</div>
<div>  &nbsp;&nbsp; &nbsp; int count = objecthash2[i].getCount();</div>
<div>  &nbsp;</div>
<div>  //将每一对数据（时间，数值）添加到数据集合2(曲线对象2)中</div>
<div>  &nbsp;</div>
<div>  &nbsp;&nbsp; &nbsp; timeseries2.add(new Hour(hour, day, month, year),count);</div>
<div>  &nbsp;</div>
<div>  }</div>
<div>  &nbsp;</div>
<div>  //将曲线对象添加到曲线数据集合对象中</div>
<div>  &nbsp;</div>
<div>  timeseriescollection.addSeries(timeseries1);</div>
<div>  &nbsp;</div>
<div>  timeseriescollection.addSeries(timeseries2);</div>
<div>  &nbsp;</div>
<div>  //绘制报表</div>
<div>  &nbsp;</div>
<div>  String title = "日在线用户统计"; //报表标题</div>
<div>  &nbsp;</div>
<div>  String domain = "时间"; &nbsp; &nbsp; //x轴</div>
<div>  &nbsp;</div>
<div>  String range = "用户在线数量"; &nbsp; &nbsp;//y轴</div>
<div>  &nbsp;</div>
<div>  //创建时间序列图对象</div>
<div>  &nbsp;</div>
<div>  JFreeChart chart = ChartFactory.createTimeSeriesChart(</div>
<div>  &nbsp;</div>
<div>  title, &nbsp; //报表标题</div>
<div>  &nbsp;</div>
<div>  domain, //报表横轴标签</div>
<div>  &nbsp;</div>
<div>  range, &nbsp; //报表纵轴标签</div>
<div>  &nbsp;</div>
<div>  timeseriescollection, //数据集合</div>
<div>  &nbsp;</div>
<div>  true, &nbsp; //是否显示图例,在这里如果为true则会在图表的下方显示各条数据曲线的名称和颜色</div>
<div>  &nbsp;</div>
<div>  false, // 是否生成工具</div>
<div>  &nbsp;</div>
<div>  false &nbsp; &nbsp;// 是否生成URL链接);</div>
<div>  &nbsp;</div>
<div>  //将报表保存为jpg文件</div>
<div>  &nbsp;</div>
<div>  ChartUtilities.saveChartAsJPEG(file, //文件保存物理路径包括路径和文件名</div>
<div>  &nbsp;</div>
<div>  100, &nbsp; &nbsp;//图片质量</div>
<div>  &nbsp;</div>
<div>  chart, //图表对象</div>
<div>  &nbsp;</div>
<div>  1024, &nbsp; //图像宽度</div>
<div>  &nbsp;</div>
<div>  768, &nbsp; &nbsp;//图像高度</div>
<div>  &nbsp;</div>
<div>  null); //显示信息</div>
<div>  &nbsp;</div>
<div>  //将报表直接在页面输出</div>
<div>  &nbsp;</div>
<div>  ChartUtilities.writeChartAsJPEG(res.getOutputStream(),100,chart,1024,768,null);</div>
<div>  &nbsp;</div>
<div>  String title="月在线用户统计"; &nbsp; //标题</div>
<div>  &nbsp;</div>
<div>  String domain="时间(天)";//x轴</div>
<div>  &nbsp;</div>
<div>  String range="用户在线数量";//y轴</div>
<div>  &nbsp;</div>
<div>  TimePeriodValuesCollection &nbsp; &nbsp;timeseriescollection &nbsp; &nbsp;= &nbsp; &nbsp;new &nbsp; &nbsp;TimePeriodValuesCollection();</div>
<div>  &nbsp;</div>
<div>  TimePeriodValues timeseries = new TimePeriodValues( "用户数量");</div>
<div>  &nbsp;</div>
<div>  timeseries.add(new Minute(0, 1, 1, 1, 2006), 100);</div>
<div>  &nbsp;</div>
<div>  timeseries.add(new Minute(10, 1, 1, 1, 2006), 500);</div>
<div>  &nbsp;</div>
<div>  timeseries.add(new Minute(20, 1, 1, 1, 2006), 300);</div>
<div>  &nbsp;</div>
<div>  timeseries.add(new Minute(30, 1, 1, 1, 2006), 800);</div>
<div>  &nbsp;</div>
<div>  JFreeChart chart =ChartFactory.createTimeSeriesChart(title,domain,range,timeseriescollection,true,false,false);</div>
<div>  &nbsp;</div>
<div>  当我们生成了一个报表对象时，可能需要根据实际情况来决定报表的横轴和纵轴的数值间隔，显示方式等。</div>
<div>  &nbsp;</div>
<div>  可以用XYPlot xyplot = (XYPlot)chart.getPlot();来得到所有数据点的集合。（其它形状图表得到的数据集对象根据实际情况造型）</div>
<div>  &nbsp;</div>
<div>  得到数据点集合后，我们就可以设置各条曲线的颜色，和坐标轴的距离，x轴、y轴的显示方式等等属性</div>
<div>  &nbsp;</div>
<div>  xyplot.setBackgroundPaint(Color.lightGray); //设定图表数据显示部分背景色</div>
<div>  &nbsp;</div>
<div>  xyplot.setAxisOffset(new RectangleInsets(5D, 5D, 5D, 5D)); //设定坐标轴与图表数据显示部分距离</div>
<div>  &nbsp;</div>
<div>  xyplot.setDomainGridlinePaint(Color.white); //网格线纵向颜色</div>
<div>  &nbsp;</div>
<div>  xyplot.setRangeGridlinePaint(Color.white); //网格线横向颜色</div>
<div>  &nbsp;</div>
## 数据点的调整

<div>  &nbsp;</div>
<div>  XYLineAndShapeRenderer xylineandshaperenderer = (XYLineAndShapeRenderer)xyplot.getRenderer();</div>
<div>  &nbsp;</div>
<div>  xylineandshaperenderer.setDefaultShapesVisible(true); &nbsp; //数据点可见</div>
<div>  &nbsp;</div>
<div>  xylineandshaperenderer.setSeriesFillPaint(0, Color.red); &nbsp; //设置第一条曲线数据点填充为红色，如果一个图表有多条曲线可分别设置</div>
<div>  &nbsp;</div>
<div>  xylineandshaperenderer.setUseFillPaint(true); &nbsp; &nbsp; //应用</div>
<div>  &nbsp;</div>
<div>  使用xyplot.getRangeAxis()得到纵轴，xyplot.getDomainAxis()得到横轴，得到后可以根据实际情况造型为自己所需要的类型。</div>
<div>  &nbsp;</div>
<div>  我的图表纵轴为数值类型，横轴为时间类型，使用如下方式</div>
<div>  &nbsp;</div>
<div>  NumberAxis numAxis = (NumberAxis)xyplot.getRangeAxis();</div>
<div>  &nbsp;</div>
<div>  DateAxis &nbsp; dateaxis = &nbsp; &nbsp;(DateAxis)xyplot.getDomainAxis();</div>
<div>  &nbsp;</div>
<div>  //设置y显示方式</div>
<div>  &nbsp;</div>
<div>  numAxis.setAutoTickUnitSelection(false);//数据轴的数据标签是否自动确定</div>
<div>  &nbsp;</div>
<div>  double &nbsp; rangetick = 0.1D;</div>
<div>  &nbsp;</div>
<div>  numAxis.setTickUnit(new NumberTickUnit(rangetick)); &nbsp; //y轴单位间隔为0.1</div>
<div>  &nbsp;</div>
<div>  //设置x轴显示方式</div>
<div>  &nbsp;</div>
<div>  dateaxis.setAutoTickUnitSelection(false);//数据轴的数据标签是否自动确定</div>
<div>  &nbsp;</div>
<div>  dateaxis.setTickUnit(new DateTickUnit(DateTickUnit.DAY,1));//x轴单位间隔为1天</div>
<div>  &nbsp;</div>
<div>  我们还可以是将数据格式化以后显示，比如y轴显示百分比（10%～100%）,x轴显示为&times;月&times;日</div>
<div>  &nbsp;</div>
<div>  NumberFormat nf =NumberFormat.getPercentInstance();</div>
<div>  &nbsp;</div>
<div>  numAxis.setNumberFormatOverride(nf);//设置y轴以百分比方式显示</div>
<div>  &nbsp;</div>
<div>  SimpleDateFormat format = new SimpleDateFormat("MM月dd");</div>
<div>  &nbsp;</div>
<div>  dateaxis.setDateFormatOverride(format);//设置x轴数据单位以&times;月&times;日方式显示</div>
<div>  &nbsp;</div>
<div>  时序图中还有一个很重要的方法</div>
<div>  &nbsp;</div>
<div>  timeseriescollection.setDomainIsPointsInTime(true); //x轴上的刻度点代表的是时间点而不是时间段</div>
<div>  &nbsp;</div>
<div>  最开始我没有设置这个属性,结果画出来的图，老是差半格不能在这个刻度的时候准确显示，往后移了半格，就是因为JFreeChart默认这个刻度是</div>
<div>  &nbsp;</div>
<div>  一个时间段，它把这个刻度和下个刻度的中间点认为是显示数据点最佳位置。</div>
<div>  &nbsp;</div>
<div>  其他一些关于AXIS类的方法：</div>
<div>  &nbsp;</div>
## Axis类：

<div>  &nbsp;</div>
<div>  void setVisible(boolean flag)坐标轴是否可见</div>
<div>  &nbsp;</div>
<div>  void setAxisLinePaint(Paint paint)坐标轴线条颜色（3D轴无效）</div>
<div>  &nbsp;</div>
<div>  void setAxisLineStroke(Stroke stroke)坐标轴线条笔触（3D轴无效）</div>
<div>  &nbsp;</div>
<div>  void setAxisLineVisible(boolean visible)坐标轴线条是否可见（3D轴无效）</div>
<div>  &nbsp;</div>
<div>  void setFixedDimension(double dimension)（用于复合表中对多坐标轴的设置）</div>
<div>  &nbsp;</div>
<div>  void setLabel(String label)坐标轴标题</div>
<div>  &nbsp;</div>
<div>  void setLabelFont(Font font)坐标轴标题字体</div>
<div>  &nbsp;</div>
<div>  void setLabelPaint(Paint paint)坐标轴标题颜色</div>
<div>  &nbsp;</div>
<div>  void setLabelAngle(double angle)`坐标轴标题旋转角度（纵坐标可以旋转）</div>
<div>  &nbsp;</div>
<div>  void setTickLabelFont(Font font)坐标轴标尺值字体</div>
<div>  &nbsp;</div>
<div>  void setTickLabelPaint(Paint paint)坐标轴标尺值颜色</div>
<div>  &nbsp;</div>
<div>  void setTickLabelsVisible(boolean flag)坐标轴标尺值是否显示</div>
<div>  &nbsp;</div>
<div>  void setTickMarkPaint(Paint paint)坐标轴标尺颜色</div>
<div>  &nbsp;</div>
<div>  void setTickMarkStroke(Stroke stroke)坐标轴标尺笔触</div>
<div>  &nbsp;</div>
<div>  void setTickMarksVisible(boolean flag)坐标轴标尺是否显示</div>
<div>  &nbsp;</div>
<div>  ValueAxis(Axis)类：</div>
<div>  &nbsp;</div>
<div>  void setAutoRange(boolean auto)自动设置数据轴数据范围</div>
<div>  &nbsp;</div>
<div>  void setAutoRangeMinimumSize(double size)自动设置数据轴数据范围时数据范围的最小跨度</div>
<div>  &nbsp;</div>
<div>  void setAutoTickUnitSelection(boolean flag)数据轴的数据标签是否自动确定（默认为true）</div>
<div>  &nbsp;</div>
<div>  void setFixedAutoRange(double length)数据轴固定数据范围（设置100的话就是显示MAXVALUE到MAXVALUE-100那段数据范围）</div>
<div>  &nbsp;</div>
<div>  void setInverted(boolean flag)数据轴是否反向（默认为false）</div>
<div>  &nbsp;</div>
<div>  void setLowerMargin(double margin)数据轴下（左）边距</div>
<div>  &nbsp;</div>
<div>  void setUpperMargin(double margin)数据轴上（右）边距</div>
<div>  &nbsp;</div>
<div>  void setLowerBound(double min)数据轴上的显示最小值</div>
<div>  &nbsp;</div>
<div>  void setUpperBound(double max)数据轴上的显示最大值</div>
<div>  &nbsp;</div>
<div>  void setPositiveArrowVisible(boolean visible)是否显示正向箭头（3D轴无效）</div>
<div>  &nbsp;</div>
<div>  void setNegativeArrowVisible(boolean visible)是否显示反向箭头（3D轴无效）</div>
<div>  &nbsp;</div>
<div>  void setVerticalTickLabels(boolean flag)数据轴数据标签是否旋转到垂直</div>
<div>  &nbsp;</div>
<div>  void setStandardTickUnits(TickUnitSource source)数据轴的数据标签（可以只显示整数标签，需要将AutoTickUnitSelection设false）</div>
<div>  &nbsp;</div>
<div>  NumberAxis(ValueAxis)类：</div>
<div>  &nbsp;</div>
<div>  void setAutoRangeIncludesZero(boolean flag)是否强制在自动选择的数据范围中包含0</div>
<div>  &nbsp;</div>
<div>  void setAutoRangeStickyZero(boolean flag)是否强制在整个数据轴中包含0，即使0不在数据范围中</div>
<div>  &nbsp;</div>
<div>  void setNumberFormatOverride(NumberFormat formatter)数据轴数据标签的显示格式</div>
<div>  &nbsp;</div>
<div>  void setTickUnit(NumberTickUnit unit)数据轴的数据标签（需要将AutoTickUnitSelection设false）</div>
<div>  &nbsp;</div>
<div>  DateAxis(ValueAxis)类：</div>
<div>  &nbsp;</div>
<div>  void setMaximumDate(Date maximumDate)日期轴上的最小日期</div>
<div>  &nbsp;</div>
<div>  void setMinimumDate(Date minimumDate)日期轴上的最大日期</div>
<div>  &nbsp;</div>
<div>  void setRange(Date lower,Date upper)日期轴范围</div>
<div>  &nbsp;</div>
<div>  void setDateFormatOverride(DateFormat formatter)日期轴日期标签的显示格式</div>
<div>  &nbsp;</div>
<div>  void setTickUnit(DateTickUnit unit)日期轴的日期标签（需要将AutoTickUnitSelection设false）</div>
<div>  &nbsp;</div>
<div>  void setTickMarkPosition(DateTickMarkPosition position)日期标签位置（参数常量在org.jfree.chart.axis.DateTickMarkPosition类中定义）</div>
<div>  &nbsp;</div>
<div>  CategoryAxis(Axis)类：</div>
<div>  &nbsp;</div>
<div>  void setCategoryMargin(double margin)分类轴边距</div>
<div>  &nbsp;</div>
<div>  void setLowerMargin(double margin)分类轴下（左）边距</div>
<div>  &nbsp;</div>
<div>  void setUpperMargin(double margin)分类轴上（右）边距</div>
<div>  &nbsp;</div>
<div>  void setVerticalCategoryLabels(boolean flag)分类轴标题是否旋转到垂直</div>
<div>  &nbsp;</div>
<div>  void setMaxCategoryLabelWidthRatio(float ratio)分类轴分类标签的最大宽度</div>