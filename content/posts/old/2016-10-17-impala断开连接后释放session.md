---
title: impala断开连接后释放session
author: fatkun
type: post
date: 2016-10-17T02:38:58+00:00
url: /2016/10/impala断开连接后释放session.html
duoshuo_thread_id:
  - 6342258704364077825
wp-syntax-cache-content:
  - |
    a:1:{i:1;s:6130:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="csharp" style="font-family:monospace;"><span style="color: #6666cc; font-weight: bold;">void</span> ImpalaServer<span style="color: #008000;">::</span><span style="color: #0000FF;">ConnectionEnd</span><span style="color: #008000;">&#40;</span>
        <span style="color: #0600FF; font-weight: bold;">const</span> ThriftServer<span style="color: #008000;">::</span><span style="color: #0000FF;">ConnectionContext</span><span style="color: #008000;">&amp;</span> connection_context<span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
      <span style="color: #0600FF; font-weight: bold;">return</span><span style="color: #008000;">;</span>
      unique_lock<span style="color: #008000;">&lt;</span>mutex<span style="color: #008000;">&gt;</span> l<span style="color: #008000;">&#40;</span>connection_to_sessions_map_lock_<span style="color: #008000;">&#41;</span><span style="color: #008000;">;</span>
      ConnectionToSessionMap<span style="color: #008000;">::</span><span style="color: #0000FF;">iterator</span> it <span style="color: #008000;">=</span>
          connection_to_sessions_map_<span style="color: #008000;">.</span><span style="color: #0000FF;">find</span><span style="color: #008000;">&#40;</span>connection_context<span style="color: #008000;">.</span><span style="color: #0000FF;">connection_id</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">;</span>
    &nbsp;
      <span style="color: #008080; font-style: italic;">// Not every connection must have an associated session</span>
      <span style="color: #0600FF; font-weight: bold;">if</span> <span style="color: #008000;">&#40;</span>it <span style="color: #008000;">==</span> connection_to_sessions_map_<span style="color: #008000;">.</span><span style="color: #0000FF;">end</span><span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#41;</span> <span style="color: #0600FF; font-weight: bold;">return</span><span style="color: #008000;">;</span>
    &nbsp;
      LOG<span style="color: #008000;">&#40;</span>INFO<span style="color: #008000;">&#41;</span> <span style="color: #008000;">&lt;&lt;</span> <span style="color: #666666;">&quot;Connection from client &quot;</span> <span style="color: #008000;">&lt;&lt;</span> connection_context<span style="color: #008000;">.</span><span style="color: #0000FF;">network_address</span>
                <span style="color: #008000;">&lt;&lt;</span> <span style="color: #666666;">&quot; closed, closing &quot;</span> <span style="color: #008000;">&lt;&lt;</span> it<span style="color: #008000;">-&gt;</span>second<span style="color: #008000;">.</span><span style="color: #0000FF;">size</span><span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span> <span style="color: #008000;">&lt;&lt;</span> <span style="color: #666666;">&quot; associated session(s)&quot;</span><span style="color: #008000;">;</span>
    &nbsp;
      BOOST_FOREACH<span style="color: #008000;">&#40;</span><span style="color: #0600FF; font-weight: bold;">const</span> TUniqueId<span style="color: #008000;">&amp;</span> session_id, it<span style="color: #008000;">-&gt;</span>second<span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
        Status status <span style="color: #008000;">=</span> CloseSessionInternal<span style="color: #008000;">&#40;</span>session_id, <span style="color: #0600FF; font-weight: bold;">true</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">;</span>
        <span style="color: #0600FF; font-weight: bold;">if</span> <span style="color: #008000;">&#40;</span><span style="color: #008000;">!</span>status<span style="color: #008000;">.</span><span style="color: #0000FF;">ok</span><span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">&#41;</span> <span style="color: #008000;">&#123;</span>
          LOG<span style="color: #008000;">&#40;</span>WARNING<span style="color: #008000;">&#41;</span> <span style="color: #008000;">&lt;&lt;</span> <span style="color: #666666;">&quot;Error closing session &quot;</span> <span style="color: #008000;">&lt;&lt;</span> session_id <span style="color: #008000;">&lt;&lt;</span> <span style="color: #666666;">&quot;: &quot;</span>
                       <span style="color: #008000;">&lt;&lt;</span> status<span style="color: #008000;">.</span><span style="color: #0000FF;">GetDetail</span><span style="color: #008000;">&#40;</span><span style="color: #008000;">&#41;</span><span style="color: #008000;">;</span>
        <span style="color: #008000;">&#125;</span>
      <span style="color: #008000;">&#125;</span>
      connection_to_sessions_map_<span style="color: #008000;">.</span><span style="color: #0000FF;">erase</span><span style="color: #008000;">&#40;</span>it<span style="color: #008000;">&#41;</span><span style="color: #008000;">;</span>
    <span style="color: #008000;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">void ImpalaServer::ConnectionEnd(
        const ThriftServer::ConnectionContext&amp; connection_context) {
      return;
      unique_lock&lt;mutex&gt; l(connection_to_sessions_map_lock_);
      ConnectionToSessionMap::iterator it =
          connection_to_sessions_map_.find(connection_context.connection_id);
    
      // Not every connection must have an associated session
      if (it == connection_to_sessions_map_.end()) return;
    
      LOG(INFO) &lt;&lt; &quot;Connection from client &quot; &lt;&lt; connection_context.network_address
                &lt;&lt; &quot; closed, closing &quot; &lt;&lt; it-&gt;second.size() &lt;&lt; &quot; associated session(s)&quot;;
    
      BOOST_FOREACH(const TUniqueId&amp; session_id, it-&gt;second) {
        Status status = CloseSessionInternal(session_id, true);
        if (!status.ok()) {
          LOG(WARNING) &lt;&lt; &quot;Error closing session &quot; &lt;&lt; session_id &lt;&lt; &quot;: &quot;
                       &lt;&lt; status.GetDetail();
        }
      }
      connection_to_sessions_map_.erase(it);
    }</p></div>
    ";}
categories:
  - hadoop
tags:
  - impala

---
代码在这里
https://github.com/cloudera/Impala/blob/cdh5-2.2.0_5.4.0/be/src/service/impala-server.cc
&nbsp;
如果不想断开清除session,直接return
<pre lang="csharp" escaped="true">void ImpalaServer::ConnectionEnd(
    const ThriftServer::ConnectionContext& connection_context) {
  return;
  unique_lock&lt;mutex&gt; l(connection_to_sessions_map_lock_);
  ConnectionToSessionMap::iterator it =
      connection_to_sessions_map_.find(connection_context.connection_id);

  // Not every connection must have an associated session
  if (it == connection_to_sessions_map_.end()) return;

  LOG(INFO) &lt;&lt; "Connection from client " &lt;&lt; connection_context.network_address
            &lt;&lt; " closed, closing " &lt;&lt; it-&gt;second.size() &lt;&lt; " associated session(s)";

  BOOST_FOREACH(const TUniqueId& session_id, it-&gt;second) {
    Status status = CloseSessionInternal(session_id, true);
    if (!status.ok()) {
      LOG(WARNING) &lt;&lt; "Error closing session " &lt;&lt; session_id &lt;&lt; ": "
                   &lt;&lt; status.GetDetail();
    }
  }
  connection_to_sessions_map_.erase(it);
}</pre>
&nbsp;