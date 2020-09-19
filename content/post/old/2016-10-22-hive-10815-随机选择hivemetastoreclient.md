---
title: HIVE-10815 随机选择HiveMetaStoreClient
author: fatkun
type: post
date: 2016-10-22T03:04:03+00:00
url: /2016/10/hive-10815-随机选择hivemetastoreclient.html
duoshuo_thread_id:
  - 6344120662709240577
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:6780:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">    <span style="color: #666666; font-style: italic;">// user wants file store based configuration</span>
        <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>conf.<span style="color: #006633;">getVar</span><span style="color: #009900;">&#40;</span>HiveConf.<span style="color: #006633;">ConfVars</span>.<span style="color: #006633;">METASTOREURIS</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">!=</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #003399;">String</span> metastoreUrisString<span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> conf.<span style="color: #006633;">getVar</span><span style="color: #009900;">&#40;</span>
              HiveConf.<span style="color: #006633;">ConfVars</span>.<span style="color: #006633;">METASTOREURIS</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">split</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;,&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          metastoreUris <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> URI<span style="color: #009900;">&#91;</span>metastoreUrisString.<span style="color: #006633;">length</span><span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span>
          <span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000066; font-weight: bold;">int</span> i <span style="color: #339933;">=</span> <span style="color: #cc66cc;">0</span><span style="color: #339933;">;</span>
            <span style="color: #000000; font-weight: bold;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> s <span style="color: #339933;">:</span> metastoreUrisString<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
              URI tmpUri <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> URI<span style="color: #009900;">&#40;</span>s<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
              <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>tmpUri.<span style="color: #006633;">getScheme</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">==</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                <span style="color: #000000; font-weight: bold;">throw</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">IllegalArgumentException</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;URI: &quot;</span> <span style="color: #339933;">+</span> s
                    <span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot; does not have a scheme&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
              <span style="color: #009900;">&#125;</span>
              metastoreUris<span style="color: #009900;">&#91;</span>i<span style="color: #339933;">++</span><span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> tmpUri<span style="color: #339933;">;</span>
    &nbsp;
            <span style="color: #009900;">&#125;</span>
          <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">IllegalArgumentException</span> e<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">throw</span> <span style="color: #009900;">&#40;</span>e<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">Exception</span> e<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            MetaStoreUtils.<span style="color: #006633;">logAndThrowMetaException</span><span style="color: #009900;">&#40;</span>e<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #009900;">&#125;</span>
        <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">else</span> <span style="color: #009900;">&#123;</span>
          LOG.<span style="color: #006633;">error</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;NOT getting uris from conf&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #000000; font-weight: bold;">throw</span> <span style="color: #000000; font-weight: bold;">new</span> MetaException<span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;MetaStoreURIs not found in conf file&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">    // user wants file store based configuration
        if (conf.getVar(HiveConf.ConfVars.METASTOREURIS) != null) {
          String metastoreUrisString[] = conf.getVar(
              HiveConf.ConfVars.METASTOREURIS).split(&quot;,&quot;);
          metastoreUris = new URI[metastoreUrisString.length];
          try {
            int i = 0;
            for (String s : metastoreUrisString) {
              URI tmpUri = new URI(s);
              if (tmpUri.getScheme() == null) {
                throw new IllegalArgumentException(&quot;URI: &quot; + s
                    + &quot; does not have a scheme&quot;);
              }
              metastoreUris[i++] = tmpUri;
    
            }
          } catch (IllegalArgumentException e) {
            throw (e);
          } catch (Exception e) {
            MetaStoreUtils.logAndThrowMetaException(e);
          }
        } else {
          LOG.error(&quot;NOT getting uris from conf&quot;);
          throw new MetaException(&quot;MetaStoreURIs not found in conf file&quot;);
        }</p></div>
    ";i:2;s:2875:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">  <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000066; font-weight: bold;">void</span> promoteRandomMetaStoreURI<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
        <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>metastoreUris.<span style="color: #006633;">length</span> <span style="color: #339933;">&lt;=</span> <span style="color: #cc66cc;">1</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #000000; font-weight: bold;">return</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
        <span style="color: #003399;">Random</span> rng <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">Random</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #000066; font-weight: bold;">int</span> index <span style="color: #339933;">=</span> rng.<span style="color: #006633;">nextInt</span><span style="color: #009900;">&#40;</span>metastoreUris.<span style="color: #006633;">length</span> <span style="color: #339933;">-</span> <span style="color: #cc66cc;">1</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">+</span> <span style="color: #cc66cc;">1</span><span style="color: #339933;">;</span>
        URI tmp <span style="color: #339933;">=</span> metastoreUris<span style="color: #009900;">&#91;</span><span style="color: #cc66cc;">0</span><span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span>
        metastoreUris<span style="color: #009900;">&#91;</span><span style="color: #cc66cc;">0</span><span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> metastoreUris<span style="color: #009900;">&#91;</span>index<span style="color: #009900;">&#93;</span><span style="color: #339933;">;</span>
        metastoreUris<span style="color: #009900;">&#91;</span>index<span style="color: #009900;">&#93;</span> <span style="color: #339933;">=</span> tmp<span style="color: #339933;">;</span>
      <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">  private void promoteRandomMetaStoreURI() {
        if (metastoreUris.length &lt;= 1) {
          return;
        }
        Random rng = new Random();
        int index = rng.nextInt(metastoreUris.length - 1) + 1;
        URI tmp = metastoreUris[0];
        metastoreUris[0] = metastoreUris[index];
        metastoreUris[index] = tmp;
      }</p></div>
    ";}
categories:
  - hive
tags:
  - hive
  - improve

---
https://issues.apache.org/jira/browse/HIVE-10815
&nbsp;
目前cdh5.4.0版本的hive第一次连接的时候，固定是使用第一个，只有连接失败后，才随机选择。
<pre>HiveMetaStoreClient.java</pre>
<pre lang="java" escaped="true">// user wants file store based configuration
    if (conf.getVar(HiveConf.ConfVars.METASTOREURIS) != null) {
      String metastoreUrisString[] = conf.getVar(
          HiveConf.ConfVars.METASTOREURIS).split(",");
      metastoreUris = new URI[metastoreUrisString.length];
      try {
        int i = 0;
        for (String s : metastoreUrisString) {
          URI tmpUri = new URI(s);
          if (tmpUri.getScheme() == null) {
            throw new IllegalArgumentException("URI: " + s
                + " does not have a scheme");
          }
          metastoreUris[i++] = tmpUri;

        }
      } catch (IllegalArgumentException e) {
        throw (e);
      } catch (Exception e) {
        MetaStoreUtils.logAndThrowMetaException(e);
      }
    } else {
      LOG.error("NOT getting uris from conf");
      throw new MetaException("MetaStoreURIs not found in conf file");
    }</pre>
&nbsp;  
在重连的时候，随机把后面的交换到第一个
<pre escaped="true" lang="java">private void promoteRandomMetaStoreURI() {
    if (metastoreUris.length &lt;= 1) {
      return;
    }
    Random rng = new Random();
    int index = rng.nextInt(metastoreUris.length - 1) + 1;
    URI tmp = metastoreUris[0];
    metastoreUris[0] = metastoreUris[index];
    metastoreUris[index] = tmp;
  }</pre>
HIVE-10815让metastore初始化的时候先打乱顺序