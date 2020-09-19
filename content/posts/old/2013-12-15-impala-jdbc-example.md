---
title: 使用jdbc连接impala例子
author: fatkun
type: post
date: 2013-12-15T12:51:02+00:00
url: /2013/12/impala-jdbc-example.html
duoshuo_thread_id:
  - 6300410060891783937
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:12952:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">java.sql.Connection</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">java.sql.DriverManager</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">java.sql.ResultSet</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">java.sql.SQLException</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">java.sql.Statement</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> ClouderaImpalaJdbcExample <span style="color: #009900;">&#123;</span>
    &nbsp;
    	<span style="color: #666666; font-style: italic;">// here is an example query based on one of the Hue Beeswax sample tables </span>
    	<span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000000; font-weight: bold;">final</span> <span style="color: #003399;">String</span> SQL_STATEMENT <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;SELECT a FROM test limit 10&quot;</span><span style="color: #339933;">;</span>
    &nbsp;
    	<span style="color: #666666; font-style: italic;">// set the impalad host</span>
    	<span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000000; font-weight: bold;">final</span> <span style="color: #003399;">String</span> IMPALAD_HOST <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;192.168.1.106&quot;</span><span style="color: #339933;">;</span>
    &nbsp;
    	<span style="color: #666666; font-style: italic;">// port 21050 is the default impalad JDBC port </span>
    	<span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000000; font-weight: bold;">final</span> <span style="color: #003399;">String</span> IMPALAD_JDBC_PORT <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;21050&quot;</span><span style="color: #339933;">;</span>
    &nbsp;
    	<span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000000; font-weight: bold;">final</span> <span style="color: #003399;">String</span> CONNECTION_URL <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;jdbc:hive2://&quot;</span> <span style="color: #339933;">+</span> IMPALAD_HOST <span style="color: #339933;">+</span> <span style="color: #0000ff;">':'</span> <span style="color: #339933;">+</span> IMPALAD_JDBC_PORT <span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot;/;auth=noSasl&quot;</span><span style="color: #339933;">;</span>
    &nbsp;
    	<span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000000; font-weight: bold;">final</span> <span style="color: #003399;">String</span> JDBC_DRIVER_NAME <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;org.apache.hive.jdbc.HiveDriver&quot;</span><span style="color: #339933;">;</span>
    &nbsp;
    	<span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000066; font-weight: bold;">void</span> main<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> args<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    &nbsp;
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;<span style="color: #000099; font-weight: bold;">\n</span>=============================================&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Cloudera Impala JDBC Example&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Using Connection URL: &quot;</span> <span style="color: #339933;">+</span> CONNECTION_URL<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Running Query: &quot;</span> <span style="color: #339933;">+</span> SQL_STATEMENT<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
    		<span style="color: #003399;">Connection</span> con <span style="color: #339933;">=</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #339933;">;</span>
    &nbsp;
    		<span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#123;</span>
    &nbsp;
    			<span style="color: #000000; font-weight: bold;">Class</span>.<span style="color: #006633;">forName</span><span style="color: #009900;">&#40;</span>JDBC_DRIVER_NAME<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
    			con <span style="color: #339933;">=</span> <span style="color: #003399;">DriverManager</span>.<span style="color: #006633;">getConnection</span><span style="color: #009900;">&#40;</span>CONNECTION_URL<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
    			<span style="color: #003399;">Statement</span> stmt <span style="color: #339933;">=</span> con.<span style="color: #006633;">createStatement</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
    			<span style="color: #003399;">ResultSet</span> rs <span style="color: #339933;">=</span> stmt.<span style="color: #006633;">executeQuery</span><span style="color: #009900;">&#40;</span>SQL_STATEMENT<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
    			<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;<span style="color: #000099; font-weight: bold;">\n</span>== Begin Query Results ======================&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
    			<span style="color: #666666; font-style: italic;">// print the results to the console</span>
    			<span style="color: #000000; font-weight: bold;">while</span> <span style="color: #009900;">&#40;</span>rs.<span style="color: #006633;">next</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    				<span style="color: #666666; font-style: italic;">// the example query returns one String column</span>
    				<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span>rs.<span style="color: #006633;">getString</span><span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">1</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    			<span style="color: #009900;">&#125;</span>
    &nbsp;
    			<span style="color: #003399;">System</span>.<span style="color: #006633;">out</span>.<span style="color: #006633;">println</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;== End Query Results =======================<span style="color: #000099; font-weight: bold;">\n</span><span style="color: #000099; font-weight: bold;">\n</span>&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
    		<span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">SQLException</span> e<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    			e.<span style="color: #006633;">printStackTrace</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">Exception</span> e<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    			e.<span style="color: #006633;">printStackTrace</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    		<span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">finally</span> <span style="color: #009900;">&#123;</span>
    			<span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#123;</span>
    				con.<span style="color: #006633;">close</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    			<span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">Exception</span> e<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    				<span style="color: #666666; font-style: italic;">// swallow</span>
    			<span style="color: #009900;">&#125;</span>
    		<span style="color: #009900;">&#125;</span>
    	<span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">import java.sql.Connection;
    import java.sql.DriverManager;
    import java.sql.ResultSet;
    import java.sql.SQLException;
    import java.sql.Statement;
    
    public class ClouderaImpalaJdbcExample {
    
    	// here is an example query based on one of the Hue Beeswax sample tables 
    	private static final String SQL_STATEMENT = &quot;SELECT a FROM test limit 10&quot;;
    
    	// set the impalad host
    	private static final String IMPALAD_HOST = &quot;192.168.1.106&quot;;
    
    	// port 21050 is the default impalad JDBC port 
    	private static final String IMPALAD_JDBC_PORT = &quot;21050&quot;;
    
    	private static final String CONNECTION_URL = &quot;jdbc:hive2://&quot; + IMPALAD_HOST + ':' + IMPALAD_JDBC_PORT + &quot;/;auth=noSasl&quot;;
    
    	private static final String JDBC_DRIVER_NAME = &quot;org.apache.hive.jdbc.HiveDriver&quot;;
    
    	public static void main(String[] args) {
    
    		System.out.println(&quot;\n=============================================&quot;);
    		System.out.println(&quot;Cloudera Impala JDBC Example&quot;);
    		System.out.println(&quot;Using Connection URL: &quot; + CONNECTION_URL);
    		System.out.println(&quot;Running Query: &quot; + SQL_STATEMENT);
    
    		Connection con = null;
    
    		try {
    
    			Class.forName(JDBC_DRIVER_NAME);
    
    			con = DriverManager.getConnection(CONNECTION_URL);
    
    			Statement stmt = con.createStatement();
    
    			ResultSet rs = stmt.executeQuery(SQL_STATEMENT);
    
    			System.out.println(&quot;\n== Begin Query Results ======================&quot;);
    
    			// print the results to the console
    			while (rs.next()) {
    				// the example query returns one String column
    				System.out.println(rs.getString(1));
    			}
    
    			System.out.println(&quot;== End Query Results =======================\n\n&quot;);
    
    		} catch (SQLException e) {
    			e.printStackTrace();
    		} catch (Exception e) {
    			e.printStackTrace();
    		} finally {
    			try {
    				con.close();
    			} catch (Exception e) {
    				// swallow
    			}
    		}
    	}
    }</p></div>
    ";}
categories:
  - hadoop
tags:
  - impala
  - jdbc

---
来源： <https://github.com/onefoursix/Cloudera-Impala-JDBC-Example>
&nbsp;
需要依赖的lib见这篇文章。
[http://www.cloudera.com/content/cloudera-content/cloudera-docs/Impala/latest/Installing-and-Using-Impala/ciiu\_impala\_jdbc.html][1]
&nbsp;
<pre lang="java" escaped="true">import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class ClouderaImpalaJdbcExample {

	// here is an example query based on one of the Hue Beeswax sample tables 
	private static final String SQL_STATEMENT = "SELECT a FROM test limit 10";

	// set the impalad host
	private static final String IMPALAD_HOST = "192.168.1.106";

	// port 21050 is the default impalad JDBC port 
	private static final String IMPALAD_JDBC_PORT = "21050";

	private static final String CONNECTION_URL = "jdbc:hive2://" + IMPALAD_HOST + ':' + IMPALAD_JDBC_PORT + "/;auth=noSasl";

	private static final String JDBC_DRIVER_NAME = "org.apache.hive.jdbc.HiveDriver";

	public static void main(String[] args) {

		System.out.println("\n=============================================");
		System.out.println("Cloudera Impala JDBC Example");
		System.out.println("Using Connection URL: " + CONNECTION_URL);
		System.out.println("Running Query: " + SQL_STATEMENT);

		Connection con = null;

		try {

			Class.forName(JDBC_DRIVER_NAME);

			con = DriverManager.getConnection(CONNECTION_URL);

			Statement stmt = con.createStatement();

			ResultSet rs = stmt.executeQuery(SQL_STATEMENT);

			System.out.println("\n== Begin Query Results ======================");

			// print the results to the console
			while (rs.next()) {
				// the example query returns one String column
				System.out.println(rs.getString(1));
			}

			System.out.println("== End Query Results =======================\n\n");

		} catch (SQLException e) {
			e.printStackTrace();
		} catch (Exception e) {
			e.printStackTrace();
		} finally {
			try {
				con.close();
			} catch (Exception e) {
				// swallow
			}
		}
	}
}</pre>

 [1]: http://www.cloudera.com/content/cloudera-content/cloudera-docs/Impala/latest/Installing-and-Using-Impala/ciiu_impala_jdbc.html