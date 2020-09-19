---
title: 信息管理实验三-ASP.NET 使用GirdView
author: fatkun
type: post
date: 2009-09-23T09:14:02+00:00
url: /2009/09/信息管理实验三-asp-net-使用girdview.html
views:
  - 4
duoshuo_thread_id:
  - 6300408673705394946
categories:
  - ASP.NET
tags:
  - 信息管理实验

---
使用Gridview控件显示数据库内容  
老 蔡  
Email：cxianfa@126.com  
实验主要步骤：  
1:新建一个数据库名字为EmployDB,在其中添加一张表EmployInfo，字段有Name，Sex，Job，Salary, 并且向其中插入一些数据.  
2: 新建一个ASP.NET程序，在主界面上拖放一个Gridview数据库控件。  
3：添加命名空间：using System.Data.SqlClient;  
Default.aspx  
&#8230;
<!--more-->

  
使用Gridview控件显示数据库内容  
老 蔡  
Email：cxianfa@126.com  
实验主要步骤：  
1:新建一个数据库名字为EmployDB,在其中添加一张表EmployInfo，字段有Name，Sex，Job，Salary, 并且向其中插入一些数据.  
2: 新建一个ASP.NET程序，在主界面上拖放一个Gridview数据库控件。  
3：添加命名空间：using System.Data.SqlClient;  
Default.aspx
<pre class="html">&lt;%@ Page Language="C#" AutoEventWireup="true"  CodeFile="Default.aspx.cs" Inherits="_Default" %&gt;
&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"&gt;
&lt;html xmlns="http://www.w3.org/1999/xhtml" &gt;
&lt;head runat="server"&gt;
&lt;title&gt;无标题页&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;form id="form1" runat="server"&gt;
&lt;div&gt;
&lt;asp:GridView ID="GridView1" runat="server"&gt;
&lt;/asp:GridView&gt;
&lt;/div&gt;
&lt;/form&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>
Default.aspx.cs
<pre class="c#">using System;
using System.Data;
using System.Configuration;
using System.Web;
using System.Web.Security;
using System.Web.UI;
using System.Web.UI.WebControls;
using System.Web.UI.WebControls.WebParts;
using System.Web.UI.HtmlControls;
using System.Data.SqlClient;
public partial class _Default : System.Web.UI.Page
{
SqlConnection sqlcon;
string strCon = "data source=localhost;database=EmployDB;uid=sa;pwd=;";
protected void Page_Load(object sender, EventArgs e)
{
if (!IsPostBack) {
Bind();
}
}
public void Bind() {
string sqlStr = "select TOP 10  * from EmployInfo";
sqlcon = new SqlConnection(strCon);
SqlDataAdapter sda = new SqlDataAdapter(sqlStr, sqlcon);
DataSet ds = new DataSet();
sqlcon.Open();
sda.Fill(ds, "EmployInfo");
GridView1.DataSource = ds;
GridView1.DataBind();
sqlcon.Close();
}
}
</pre>