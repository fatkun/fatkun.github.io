---
title: hdfs complete file 超时
author: fatkun
type: post
date: 2016-04-25T02:48:00+00:00
url: /2016/04/hdfs-complete-file-timeout.html
duoshuo_thread_id:
  - 6300421658565935873
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:10084:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">  <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000066; font-weight: bold;">void</span> completeFile<span style="color: #009900;">&#40;</span>ExtendedBlock last<span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">throws</span> <span style="color: #003399;">IOException</span> <span style="color: #009900;">&#123;</span>
        <span style="color: #000066; font-weight: bold;">long</span> localstart <span style="color: #339933;">=</span> <span style="color: #003399;">Time</span>.<span style="color: #006633;">now</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #000066; font-weight: bold;">long</span> localTimeout <span style="color: #339933;">=</span> <span style="color: #cc66cc;">400</span><span style="color: #339933;">;</span>
        <span style="color: #000066; font-weight: bold;">boolean</span> fileComplete <span style="color: #339933;">=</span> <span style="color: #000066; font-weight: bold;">false</span><span style="color: #339933;">;</span>
        <span style="color: #000066; font-weight: bold;">int</span> retries <span style="color: #339933;">=</span> dfsClient.<span style="color: #006633;">getConf</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">nBlockWriteLocateFollowingRetry</span><span style="color: #339933;">;</span>
        <span style="color: #000000; font-weight: bold;">while</span> <span style="color: #009900;">&#40;</span><span style="color: #339933;">!</span>fileComplete<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          fileComplete <span style="color: #339933;">=</span>
              dfsClient.<span style="color: #006633;">namenode</span>.<span style="color: #006633;">complete</span><span style="color: #009900;">&#40;</span>src, dfsClient.<span style="color: #006633;">clientName</span>, last, fileId<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span><span style="color: #339933;">!</span>fileComplete<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">final</span> <span style="color: #000066; font-weight: bold;">int</span> hdfsTimeout <span style="color: #339933;">=</span> dfsClient.<span style="color: #006633;">getHdfsTimeout</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span><span style="color: #339933;">!</span>dfsClient.<span style="color: #006633;">clientRunning</span> <span style="color: #339933;">&amp;</span>brvbar<span style="color: #339933;">;&amp;</span>brvbar<span style="color: #339933;">;</span>
                  <span style="color: #009900;">&#40;</span>hdfsTimeout <span style="color: #339933;">&gt;</span> <span style="color: #cc66cc;">0</span> <span style="color: #339933;">&amp;&amp;</span> localstart <span style="color: #339933;">+</span> hdfsTimeout <span style="color: #339933;">&lt;</span> <span style="color: #003399;">Time</span>.<span style="color: #006633;">now</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                <span style="color: #003399;">String</span> msg <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;Unable to close file because dfsclient &quot;</span> <span style="color: #339933;">+</span>
                              <span style="color: #0000ff;">&quot; was unable to contact the HDFS servers.&quot;</span> <span style="color: #339933;">+</span>
                              <span style="color: #0000ff;">&quot; clientRunning &quot;</span> <span style="color: #339933;">+</span> dfsClient.<span style="color: #006633;">clientRunning</span> <span style="color: #339933;">+</span>
                              <span style="color: #0000ff;">&quot; hdfsTimeout &quot;</span> <span style="color: #339933;">+</span> hdfsTimeout<span style="color: #339933;">;</span>
                DFSClient.<span style="color: #006633;">LOG</span>.<span style="color: #006633;">info</span><span style="color: #009900;">&#40;</span>msg<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #000000; font-weight: bold;">throw</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">IOException</span><span style="color: #009900;">&#40;</span>msg<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
            <span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#123;</span>
              <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>retries <span style="color: #339933;">==</span> <span style="color: #cc66cc;">0</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                <span style="color: #000000; font-weight: bold;">throw</span> <span style="color: #000000; font-weight: bold;">new</span> <span style="color: #003399;">IOException</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Unable to close file because the last block&quot;</span>
                    <span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot; does not have enough number of replicas.&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
              <span style="color: #009900;">&#125;</span>
              retries<span style="color: #339933;">--;</span>
              <span style="color: #003399;">Thread</span>.<span style="color: #006633;">sleep</span><span style="color: #009900;">&#40;</span>localTimeout<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
              localTimeout <span style="color: #339933;">*=</span> <span style="color: #cc66cc;">2</span><span style="color: #339933;">;</span>
              <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">Time</span>.<span style="color: #006633;">now</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">-</span> localstart <span style="color: #339933;">&gt;</span> <span style="color: #cc66cc;">5000</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                DFSClient.<span style="color: #006633;">LOG</span>.<span style="color: #006633;">info</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Could not complete &quot;</span> <span style="color: #339933;">+</span> src <span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot; retrying...&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
              <span style="color: #009900;">&#125;</span>
            <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span><span style="color: #003399;">InterruptedException</span> ie<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
              DFSClient.<span style="color: #006633;">LOG</span>.<span style="color: #006633;">warn</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Caught exception &quot;</span>, ie<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
          <span style="color: #009900;">&#125;</span>
        <span style="color: #009900;">&#125;</span>
      <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">  private void completeFile(ExtendedBlock last) throws IOException {
        long localstart = Time.now();
        long localTimeout = 400;
        boolean fileComplete = false;
        int retries = dfsClient.getConf().nBlockWriteLocateFollowingRetry;
        while (!fileComplete) {
          fileComplete =
              dfsClient.namenode.complete(src, dfsClient.clientName, last, fileId);
          if (!fileComplete) {
            final int hdfsTimeout = dfsClient.getHdfsTimeout();
            if (!dfsClient.clientRunning &amp;brvbar;&amp;brvbar;
                  (hdfsTimeout &gt; 0 &amp;&amp; localstart + hdfsTimeout &lt; Time.now())) {
                String msg = &quot;Unable to close file because dfsclient &quot; +
                              &quot; was unable to contact the HDFS servers.&quot; +
                              &quot; clientRunning &quot; + dfsClient.clientRunning +
                              &quot; hdfsTimeout &quot; + hdfsTimeout;
                DFSClient.LOG.info(msg);
                throw new IOException(msg);
            }
            try {
              if (retries == 0) {
                throw new IOException(&quot;Unable to close file because the last block&quot;
                    + &quot; does not have enough number of replicas.&quot;);
              }
              retries--;
              Thread.sleep(localTimeout);
              localTimeout *= 2;
              if (Time.now() - localstart &gt; 5000) {
                DFSClient.LOG.info(&quot;Could not complete &quot; + src + &quot; retrying...&quot;);
              }
            } catch (InterruptedException ie) {
              DFSClient.LOG.warn(&quot;Caught exception &quot;, ie);
            }
          }
        }
      }</p></div>
    ";i:2;s:1390:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>dfs.client.block.write.locateFollowingBlock.retries<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>10<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">&lt;property&gt;
      &lt;name&gt;dfs.client.block.write.locateFollowingBlock.retries&lt;/name&gt;
      &lt;value&gt;10&lt;/value&gt;
    &lt;/property&gt;</p></div>
    ";}
categories:
  - hadoop
tags:
  - hadoop
  - hdfs

---
修改一下超时次数，具体代码在 DFSOutputStream.java
<pre escaped="true" lang="java">private void completeFile(ExtendedBlock last) throws IOException {
    long localstart = Time.now();
    long localTimeout = 400;
    boolean fileComplete = false;
    int retries = dfsClient.getConf().nBlockWriteLocateFollowingRetry;
    while (!fileComplete) {
      fileComplete =
          dfsClient.namenode.complete(src, dfsClient.clientName, last, fileId);
      if (!fileComplete) {
        final int hdfsTimeout = dfsClient.getHdfsTimeout();
        if (!dfsClient.clientRunning &brvbar;&brvbar;
              (hdfsTimeout &gt; 0 && localstart + hdfsTimeout &lt; Time.now())) {
            String msg = "Unable to close file because dfsclient " +
                          " was unable to contact the HDFS servers." +
                          " clientRunning " + dfsClient.clientRunning +
                          " hdfsTimeout " + hdfsTimeout;
            DFSClient.LOG.info(msg);
            throw new IOException(msg);
        }
        try {
          if (retries == 0) {
            throw new IOException("Unable to close file because the last block"
                + " does not have enough number of replicas.");
          }
          retries--;
          Thread.sleep(localTimeout);
          localTimeout *= 2;
          if (Time.now() - localstart &gt; 5000) {
            DFSClient.LOG.info("Could not complete " + src + " retrying...");
          }
        } catch (InterruptedException ie) {
          DFSClient.LOG.warn("Caught exception ", ie);
        }
      }
    }
  }
</pre>
<pre lang="xml" escaped="true">&lt;property&gt;
  &lt;name&gt;dfs.client.block.write.locateFollowingBlock.retries&lt;/name&gt;
  &lt;value&gt;10&lt;/value&gt;
&lt;/property&gt;</pre>