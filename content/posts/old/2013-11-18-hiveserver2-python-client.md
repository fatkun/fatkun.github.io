---
title: hiveserver2 python client
author: fatkun
type: post
date: 2013-11-17T16:45:11+00:00
url: /2013/11/hiveserver2-python-client.html
duoshuo_thread_id:
  - 6300410060191302401
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:1202:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">java.<span style="color: #006633;">lang</span>.<span style="color: #003399;">RuntimeException</span><span style="color: #339933;">:</span> org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">thrift</span>.<span style="color: #006633;">transport</span>.<span style="color: #006633;">TTransportException</span>
    	at org.<span style="color: #006633;">apache</span>.<span style="color: #006633;">thrift</span>.<span style="color: #006633;">transport</span>.<span style="color: #006633;">TSaslServerTransport</span>$Factory.<span style="color: #006633;">getTransport</span><span style="color: #009900;">&#40;</span>TSaslServerTransport.<span style="color: #006633;">java</span><span style="color: #339933;">:</span><span style="color: #cc66cc;">219</span><span style="color: #009900;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">java.lang.RuntimeException: org.apache.thrift.transport.TTransportException
    	at org.apache.thrift.transport.TSaslServerTransport$Factory.getTransport(TSaslServerTransport.java:219)</p></div>
    ";i:2;s:1222:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;property<span style="color: #000000; font-weight: bold;">&gt;</span></span><span style="color: #000000; font-weight: bold;">&lt;name<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>hive.server2.authentication<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/name<span style="color: #000000; font-weight: bold;">&gt;</span></span><span style="color: #000000; font-weight: bold;">&lt;value<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>NOSASL<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/value<span style="color: #000000; font-weight: bold;">&gt;</span></span><span style="color: #000000; font-weight: bold;">&lt;/property<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">&lt;property&gt;&lt;name&gt;hive.server2.authentication&lt;/name&gt;&lt;value&gt;NOSASL&lt;/value&gt;&lt;/property&gt;</p></div>
    ";i:3;s:22853:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="python" style="font-family:monospace;"><span style="color: #808080; font-style: italic;">#!/usr/bin/env python</span>
    <span style="color: #808080; font-style: italic;"># -*- coding: utf-8 -*-</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">import</span> <span style="color: #dc143c;">sys</span>
    <span style="color: #ff7700;font-weight:bold;">import</span> <span style="color: #dc143c;">os</span>
    &nbsp;
    &nbsp;
    cur_dir <span style="color: #66cc66;">=</span> <span style="color: #dc143c;">os</span>.<span style="color: black;">path</span>.<span style="color: black;">dirname</span><span style="color: black;">&#40;</span><span style="color: #dc143c;">os</span>.<span style="color: black;">path</span>.<span style="color: black;">abspath</span><span style="color: black;">&#40;</span>__file__<span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    <span style="color: #dc143c;">sys</span>.<span style="color: black;">path</span>.<span style="color: black;">append</span><span style="color: black;">&#40;</span><span style="color: #dc143c;">os</span>.<span style="color: black;">path</span>.<span style="color: black;">join</span><span style="color: black;">&#40;</span>cur_dir<span style="color: #66cc66;">,</span> <span style="color: #483d8b;">&quot;gen-py&quot;</span><span style="color: black;">&#41;</span><span style="color: black;">&#41;</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">from</span> TCLIService <span style="color: #ff7700;font-weight:bold;">import</span> TCLIService
    <span style="color: #ff7700;font-weight:bold;">from</span> TCLIService.<span style="color: black;">ttypes</span> <span style="color: #ff7700;font-weight:bold;">import</span> TOpenSessionReq<span style="color: #66cc66;">,</span> TGetTablesReq<span style="color: #66cc66;">,</span> TFetchResultsReq<span style="color: #66cc66;">,</span>\
      TStatusCode<span style="color: #66cc66;">,</span> TGetResultSetMetadataReq<span style="color: #66cc66;">,</span> TGetColumnsReq<span style="color: #66cc66;">,</span> TType<span style="color: #66cc66;">,</span>\
      TExecuteStatementReq<span style="color: #66cc66;">,</span> TGetOperationStatusReq<span style="color: #66cc66;">,</span> TFetchOrientation<span style="color: #66cc66;">,</span>\
      TCloseSessionReq<span style="color: #66cc66;">,</span> TGetSchemasReq<span style="color: #66cc66;">,</span> TGetLogReq<span style="color: #66cc66;">,</span> TCancelOperationReq
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">from</span> thrift <span style="color: #ff7700;font-weight:bold;">import</span> Thrift
    <span style="color: #ff7700;font-weight:bold;">from</span> thrift.<span style="color: black;">transport</span> <span style="color: #ff7700;font-weight:bold;">import</span> TSocket
    <span style="color: #ff7700;font-weight:bold;">from</span> thrift.<span style="color: black;">transport</span> <span style="color: #ff7700;font-weight:bold;">import</span> TTransport
    <span style="color: #ff7700;font-weight:bold;">from</span> thrift.<span style="color: black;">protocol</span> <span style="color: #ff7700;font-weight:bold;">import</span> TBinaryProtocol
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">class</span> HiveServerTColumnValue:
      <span style="color: #ff7700;font-weight:bold;">def</span> <span style="color: #0000cd;">__init__</span><span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: #66cc66;">,</span> tcolumn_value<span style="color: black;">&#41;</span>:
        <span style="color: #008000;">self</span>.<span style="color: black;">column_value</span> <span style="color: #66cc66;">=</span> tcolumn_value
    &nbsp;
      <span style="color: #66cc66;">@</span><span style="color: #008000;">property</span>
      <span style="color: #ff7700;font-weight:bold;">def</span> val<span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: black;">&#41;</span>:
        <span style="color: #808080; font-style: italic;"># TODO get index from schema</span>
        <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #008000;">self</span>.<span style="color: black;">column_value</span>.<span style="color: black;">boolVal</span> <span style="color: #ff7700;font-weight:bold;">is</span> <span style="color: #ff7700;font-weight:bold;">not</span> <span style="color: #008000;">None</span>:
          <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: #008000;">self</span>.<span style="color: black;">column_value</span>.<span style="color: black;">boolVal</span>.<span style="color: black;">value</span>
        <span style="color: #ff7700;font-weight:bold;">elif</span> <span style="color: #008000;">self</span>.<span style="color: black;">column_value</span>.<span style="color: black;">byteVal</span> <span style="color: #ff7700;font-weight:bold;">is</span> <span style="color: #ff7700;font-weight:bold;">not</span> <span style="color: #008000;">None</span>:
          <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: #008000;">self</span>.<span style="color: black;">column_value</span>.<span style="color: black;">byteVal</span>.<span style="color: black;">value</span>
        <span style="color: #ff7700;font-weight:bold;">elif</span> <span style="color: #008000;">self</span>.<span style="color: black;">column_value</span>.<span style="color: black;">i16Val</span> <span style="color: #ff7700;font-weight:bold;">is</span> <span style="color: #ff7700;font-weight:bold;">not</span> <span style="color: #008000;">None</span>:
          <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: #008000;">self</span>.<span style="color: black;">column_value</span>.<span style="color: black;">i16Val</span>.<span style="color: black;">value</span>
        <span style="color: #ff7700;font-weight:bold;">elif</span> <span style="color: #008000;">self</span>.<span style="color: black;">column_value</span>.<span style="color: black;">i32Val</span> <span style="color: #ff7700;font-weight:bold;">is</span> <span style="color: #ff7700;font-weight:bold;">not</span> <span style="color: #008000;">None</span>:
          <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: #008000;">self</span>.<span style="color: black;">column_value</span>.<span style="color: black;">i32Val</span>.<span style="color: black;">value</span>
        <span style="color: #ff7700;font-weight:bold;">elif</span> <span style="color: #008000;">self</span>.<span style="color: black;">column_value</span>.<span style="color: black;">i64Val</span> <span style="color: #ff7700;font-weight:bold;">is</span> <span style="color: #ff7700;font-weight:bold;">not</span> <span style="color: #008000;">None</span>:
          <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: #008000;">self</span>.<span style="color: black;">column_value</span>.<span style="color: black;">i64Val</span>.<span style="color: black;">value</span>
        <span style="color: #ff7700;font-weight:bold;">elif</span> <span style="color: #008000;">self</span>.<span style="color: black;">column_value</span>.<span style="color: black;">doubleVal</span> <span style="color: #ff7700;font-weight:bold;">is</span> <span style="color: #ff7700;font-weight:bold;">not</span> <span style="color: #008000;">None</span>:
          <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: #008000;">self</span>.<span style="color: black;">column_value</span>.<span style="color: black;">doubleVal</span>.<span style="color: black;">value</span>
        <span style="color: #ff7700;font-weight:bold;">elif</span> <span style="color: #008000;">self</span>.<span style="color: black;">column_value</span>.<span style="color: black;">stringVal</span> <span style="color: #ff7700;font-weight:bold;">is</span> <span style="color: #ff7700;font-weight:bold;">not</span> <span style="color: #008000;">None</span>:
          <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: #008000;">self</span>.<span style="color: black;">column_value</span>.<span style="color: black;">stringVal</span>.<span style="color: black;">value</span>
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">class</span> HiveServerClient<span style="color: black;">&#40;</span><span style="color: #008000;">object</span><span style="color: black;">&#41;</span>:
        <span style="color: #dc143c;">user</span> <span style="color: #66cc66;">=</span> <span style="color: #483d8b;">'fatkun'</span>
        session_handle <span style="color: #66cc66;">=</span> <span style="color: #008000;">None</span>
    &nbsp;
        <span style="color: #ff7700;font-weight:bold;">def</span> connect<span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: black;">&#41;</span>:
            transport <span style="color: #66cc66;">=</span> TSocket.<span style="color: black;">TSocket</span><span style="color: black;">&#40;</span><span style="color: #483d8b;">'localhost'</span><span style="color: #66cc66;">,</span> <span style="color: #ff4500;">10000</span><span style="color: black;">&#41;</span>
            transport <span style="color: #66cc66;">=</span> TTransport.<span style="color: black;">TBufferedTransport</span><span style="color: black;">&#40;</span>transport<span style="color: black;">&#41;</span>
            protocol <span style="color: #66cc66;">=</span> TBinaryProtocol.<span style="color: black;">TBinaryProtocol</span><span style="color: black;">&#40;</span>transport<span style="color: black;">&#41;</span>
            client <span style="color: #66cc66;">=</span> TCLIService.<span style="color: black;">Client</span><span style="color: black;">&#40;</span>protocol<span style="color: black;">&#41;</span>
            transport.<span style="color: #008000;">open</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
            <span style="color: #008000;">self</span>._client <span style="color: #66cc66;">=</span> client
    &nbsp;
        <span style="color: #ff7700;font-weight:bold;">def</span> open_session<span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: #66cc66;">,</span> username<span style="color: black;">&#41;</span>:
            req <span style="color: #66cc66;">=</span> TOpenSessionReq<span style="color: black;">&#40;</span>username<span style="color: #66cc66;">=</span>username<span style="color: #66cc66;">,</span> configuration<span style="color: #66cc66;">=</span><span style="color: black;">&#123;</span><span style="color: black;">&#125;</span><span style="color: black;">&#41;</span>
            res <span style="color: #66cc66;">=</span> <span style="color: #008000;">self</span>._client.<span style="color: black;">OpenSession</span><span style="color: black;">&#40;</span>req<span style="color: black;">&#41;</span>
            session_handle <span style="color: #66cc66;">=</span> res.<span style="color: black;">sessionHandle</span>
            <span style="color: #ff7700;font-weight:bold;">print</span> res
            <span style="color: #ff7700;font-weight:bold;">return</span> session_handle
    &nbsp;
        <span style="color: #ff7700;font-weight:bold;">def</span> call<span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: #66cc66;">,</span> fn<span style="color: #66cc66;">,</span> req<span style="color: #66cc66;">,</span> status<span style="color: #66cc66;">=</span>TStatusCode.<span style="color: black;">SUCCESS_STATUS</span><span style="color: black;">&#41;</span>:
            <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #008000;">self</span>.<span style="color: black;">session_handle</span> <span style="color: #ff7700;font-weight:bold;">is</span> <span style="color: #008000;">None</span>:
                <span style="color: #008000;">self</span>.<span style="color: black;">session_handle</span> <span style="color: #66cc66;">=</span> <span style="color: #008000;">self</span>.<span style="color: black;">open_session</span><span style="color: black;">&#40;</span><span style="color: #008000;">self</span>.<span style="color: #dc143c;">user</span><span style="color: black;">&#41;</span>
    &nbsp;
            <span style="color: #ff7700;font-weight:bold;">if</span> <span style="color: #008000;">hasattr</span><span style="color: black;">&#40;</span>req<span style="color: #66cc66;">,</span> <span style="color: #483d8b;">'sessionHandle'</span><span style="color: black;">&#41;</span> <span style="color: #ff7700;font-weight:bold;">and</span> req.<span style="color: black;">sessionHandle</span> <span style="color: #ff7700;font-weight:bold;">is</span> <span style="color: #008000;">None</span>:
                req.<span style="color: black;">sessionHandle</span> <span style="color: #66cc66;">=</span> <span style="color: #008000;">self</span>.<span style="color: black;">session_handle</span>
    &nbsp;
            res <span style="color: #66cc66;">=</span> fn<span style="color: black;">&#40;</span>req<span style="color: black;">&#41;</span>
            <span style="color: #ff7700;font-weight:bold;">return</span> res
    &nbsp;
        <span style="color: #ff7700;font-weight:bold;">def</span> execute_statement<span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: #66cc66;">,</span> statement<span style="color: #66cc66;">,</span> max_rows<span style="color: #66cc66;">=</span><span style="color: #ff4500;">100</span><span style="color: black;">&#41;</span>:
            req <span style="color: #66cc66;">=</span> TExecuteStatementReq<span style="color: black;">&#40;</span>statement<span style="color: #66cc66;">=</span>statement<span style="color: #66cc66;">,</span> confOverlay<span style="color: #66cc66;">=</span><span style="color: black;">&#123;</span><span style="color: black;">&#125;</span><span style="color: black;">&#41;</span>
            res <span style="color: #66cc66;">=</span> <span style="color: #008000;">self</span>.<span style="color: black;">call</span><span style="color: black;">&#40;</span><span style="color: #008000;">self</span>._client.<span style="color: black;">ExecuteStatement</span><span style="color: #66cc66;">,</span> req<span style="color: black;">&#41;</span>
    &nbsp;
            <span style="color: #ff7700;font-weight:bold;">return</span> <span style="color: #008000;">self</span>.<span style="color: black;">fetch_result</span><span style="color: black;">&#40;</span>res.<span style="color: black;">operationHandle</span><span style="color: #66cc66;">,</span> max_rows<span style="color: #66cc66;">=</span>max_rows<span style="color: black;">&#41;</span>
    &nbsp;
    &nbsp;
        <span style="color: #ff7700;font-weight:bold;">def</span> fetch_result<span style="color: black;">&#40;</span><span style="color: #008000;">self</span><span style="color: #66cc66;">,</span> operation_handle<span style="color: #66cc66;">,</span> orientation<span style="color: #66cc66;">=</span>TFetchOrientation.<span style="color: black;">FETCH_NEXT</span><span style="color: #66cc66;">,</span> max_rows<span style="color: #66cc66;">=</span><span style="color: #ff4500;">100</span><span style="color: black;">&#41;</span>:
            fetch_req <span style="color: #66cc66;">=</span> TFetchResultsReq<span style="color: black;">&#40;</span>operationHandle<span style="color: #66cc66;">=</span>operation_handle<span style="color: #66cc66;">,</span> orientation<span style="color: #66cc66;">=</span>orientation<span style="color: #66cc66;">,</span> maxRows<span style="color: #66cc66;">=</span>max_rows<span style="color: black;">&#41;</span>
            res <span style="color: #66cc66;">=</span> <span style="color: #008000;">self</span>.<span style="color: black;">call</span><span style="color: black;">&#40;</span><span style="color: #008000;">self</span>._client.<span style="color: black;">FetchResults</span><span style="color: #66cc66;">,</span> fetch_req<span style="color: black;">&#41;</span>
    &nbsp;
            <span style="color: #ff7700;font-weight:bold;">if</span> operation_handle.<span style="color: black;">hasResultSet</span>:
              meta_req <span style="color: #66cc66;">=</span> TGetResultSetMetadataReq<span style="color: black;">&#40;</span>operationHandle<span style="color: #66cc66;">=</span>operation_handle<span style="color: black;">&#41;</span>
              schema <span style="color: #66cc66;">=</span> <span style="color: #008000;">self</span>.<span style="color: black;">call</span><span style="color: black;">&#40;</span><span style="color: #008000;">self</span>._client.<span style="color: black;">GetResultSetMetadata</span><span style="color: #66cc66;">,</span> meta_req<span style="color: black;">&#41;</span>
            <span style="color: #ff7700;font-weight:bold;">else</span>:
              schema <span style="color: #66cc66;">=</span> <span style="color: #008000;">None</span>
    &nbsp;
            <span style="color: #ff7700;font-weight:bold;">return</span> res<span style="color: #66cc66;">,</span> schema
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">def</span> main<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>:
    &nbsp;
        client <span style="color: #66cc66;">=</span> HiveServerClient<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
        client.<span style="color: black;">connect</span><span style="color: black;">&#40;</span><span style="color: black;">&#41;</span>
        client.<span style="color: black;">execute_statement</span><span style="color: black;">&#40;</span>statement<span style="color: #66cc66;">=</span><span style="color: #483d8b;">'SET hive.server2.blocking.query=true'</span><span style="color: black;">&#41;</span>
    &nbsp;
        statement <span style="color: #66cc66;">=</span> <span style="color: #483d8b;">'select name from test'</span>
        res<span style="color: #66cc66;">,</span> schema <span style="color: #66cc66;">=</span> client.<span style="color: black;">execute_statement</span><span style="color: black;">&#40;</span>statement<span style="color: black;">&#41;</span>
        <span style="color: #ff7700;font-weight:bold;">for</span> row <span style="color: #ff7700;font-weight:bold;">in</span> res.<span style="color: black;">results</span>.<span style="color: black;">rows</span>:
            <span style="color: #ff7700;font-weight:bold;">for</span> column <span style="color: #ff7700;font-weight:bold;">in</span> row.<span style="color: black;">colVals</span>:
                <span style="color: #ff7700;font-weight:bold;">print</span> HiveServerTColumnValue<span style="color: black;">&#40;</span>column<span style="color: black;">&#41;</span>.<span style="color: black;">val</span>
    &nbsp;
    &nbsp;
    <span style="color: #ff7700;font-weight:bold;">if</span> __name__ <span style="color: #66cc66;">==</span> <span style="color: #483d8b;">'__main__'</span>:
    	main<span style="color: black;">&#40;</span><span style="color: black;">&#41;</span></pre></td></tr></table><p class="theCode" style="display:none;">#!/usr/bin/env python
    # -*- coding: utf-8 -*-
    
    import sys
    import os
    
    
    cur_dir = os.path.dirname(os.path.abspath(__file__))
    sys.path.append(os.path.join(cur_dir, &quot;gen-py&quot;))
    
    from TCLIService import TCLIService
    from TCLIService.ttypes import TOpenSessionReq, TGetTablesReq, TFetchResultsReq,\
      TStatusCode, TGetResultSetMetadataReq, TGetColumnsReq, TType,\
      TExecuteStatementReq, TGetOperationStatusReq, TFetchOrientation,\
      TCloseSessionReq, TGetSchemasReq, TGetLogReq, TCancelOperationReq
    
    from thrift import Thrift
    from thrift.transport import TSocket
    from thrift.transport import TTransport
    from thrift.protocol import TBinaryProtocol
    
    class HiveServerTColumnValue:
      def __init__(self, tcolumn_value):
        self.column_value = tcolumn_value
    
      @property
      def val(self):
        # TODO get index from schema
        if self.column_value.boolVal is not None:
          return self.column_value.boolVal.value
        elif self.column_value.byteVal is not None:
          return self.column_value.byteVal.value
        elif self.column_value.i16Val is not None:
          return self.column_value.i16Val.value
        elif self.column_value.i32Val is not None:
          return self.column_value.i32Val.value
        elif self.column_value.i64Val is not None:
          return self.column_value.i64Val.value
        elif self.column_value.doubleVal is not None:
          return self.column_value.doubleVal.value
        elif self.column_value.stringVal is not None:
          return self.column_value.stringVal.value
    
    class HiveServerClient(object):
        user = 'fatkun'
        session_handle = None
        
        def connect(self):
            transport = TSocket.TSocket('localhost', 10000)
            transport = TTransport.TBufferedTransport(transport)
            protocol = TBinaryProtocol.TBinaryProtocol(transport)
            client = TCLIService.Client(protocol)
            transport.open()
            self._client = client
    
        def open_session(self, username):
            req = TOpenSessionReq(username=username, configuration={})
            res = self._client.OpenSession(req)
            session_handle = res.sessionHandle
            print res
            return session_handle
        
        def call(self, fn, req, status=TStatusCode.SUCCESS_STATUS):
            if self.session_handle is None:
                self.session_handle = self.open_session(self.user)
                
            if hasattr(req, 'sessionHandle') and req.sessionHandle is None:
                req.sessionHandle = self.session_handle
            
            res = fn(req)
            return res
        
        def execute_statement(self, statement, max_rows=100):
            req = TExecuteStatementReq(statement=statement, confOverlay={})
            res = self.call(self._client.ExecuteStatement, req)
    
            return self.fetch_result(res.operationHandle, max_rows=max_rows)
    
    
        def fetch_result(self, operation_handle, orientation=TFetchOrientation.FETCH_NEXT, max_rows=100):
            fetch_req = TFetchResultsReq(operationHandle=operation_handle, orientation=orientation, maxRows=max_rows)
            res = self.call(self._client.FetchResults, fetch_req)
    
            if operation_handle.hasResultSet:
              meta_req = TGetResultSetMetadataReq(operationHandle=operation_handle)
              schema = self.call(self._client.GetResultSetMetadata, meta_req)
            else:
              schema = None
    
            return res, schema
    
    def main():
        
        client = HiveServerClient()
        client.connect()
        client.execute_statement(statement='SET hive.server2.blocking.query=true')
        
        statement = 'select name from test'
        res, schema = client.execute_statement(statement)
        for row in res.results.rows:
            for column in row.colVals:
                print HiveServerTColumnValue(column).val
    
    
    if __name__ == '__main__':
    	main()</p></div>
    ";}
categories:
  - hive
tags:
  - hive
  - hiveserver2
  - python

---
一个hiveserver2 python客户端的例子，大部分代码来自于hue。
忽略了一些必要的判断，只是做一个简单的例子。  
需要安装thrift以及把hive-0.10.0-cdh4.3.0/src/service/src/gen/thrift/gen-py目录拷贝到项目目录中。  
thrift文件在hive-0.10.0-cdh4.3.0/src/service/if/TCLIService.thrift
默认需要通过sasl客户端，前端的表现是连接了没反应，后端hiveserver2有错误日志
<pre escaped="true" lang="java">java.lang.RuntimeException: org.apache.thrift.transport.TTransportException
	at org.apache.thrift.transport.TSaslServerTransport$Factory.getTransport(TSaslServerTransport.java:219)</pre>
如果不用sasl客户端，可以设置参数（[参考stackoverflow][1]）
<pre escaped="true" lang="xml">&lt;property&gt;&lt;name&gt;hive.server2.authentication&lt;/name&gt;&lt;value&gt;NOSASL&lt;/value&gt;&lt;/property&gt;</pre>
<pre escaped="true" lang="python">#!/usr/bin/env python
# -*- coding: utf-8 -*-

import sys
import os


cur_dir = os.path.dirname(os.path.abspath(__file__))
sys.path.append(os.path.join(cur_dir, "gen-py"))

from TCLIService import TCLIService
from TCLIService.ttypes import TOpenSessionReq, TGetTablesReq, TFetchResultsReq,\
  TStatusCode, TGetResultSetMetadataReq, TGetColumnsReq, TType,\
  TExecuteStatementReq, TGetOperationStatusReq, TFetchOrientation,\
  TCloseSessionReq, TGetSchemasReq, TGetLogReq, TCancelOperationReq

from thrift import Thrift
from thrift.transport import TSocket
from thrift.transport import TTransport
from thrift.protocol import TBinaryProtocol

class HiveServerTColumnValue:
  def __init__(self, tcolumn_value):
    self.column_value = tcolumn_value

  @property
  def val(self):
    # TODO get index from schema
    if self.column_value.boolVal is not None:
      return self.column_value.boolVal.value
    elif self.column_value.byteVal is not None:
      return self.column_value.byteVal.value
    elif self.column_value.i16Val is not None:
      return self.column_value.i16Val.value
    elif self.column_value.i32Val is not None:
      return self.column_value.i32Val.value
    elif self.column_value.i64Val is not None:
      return self.column_value.i64Val.value
    elif self.column_value.doubleVal is not None:
      return self.column_value.doubleVal.value
    elif self.column_value.stringVal is not None:
      return self.column_value.stringVal.value

class HiveServerClient(object):
    user = 'fatkun'
    session_handle = None
    
    def connect(self):
        transport = TSocket.TSocket('localhost', 10000)
        transport = TTransport.TBufferedTransport(transport)
        protocol = TBinaryProtocol.TBinaryProtocol(transport)
        client = TCLIService.Client(protocol)
        transport.open()
        self._client = client

    def open_session(self, username):
        req = TOpenSessionReq(username=username, configuration={})
        res = self._client.OpenSession(req)
        session_handle = res.sessionHandle
        print res
        return session_handle
    
    def call(self, fn, req, status=TStatusCode.SUCCESS_STATUS):
        if self.session_handle is None:
            self.session_handle = self.open_session(self.user)
            
        if hasattr(req, 'sessionHandle') and req.sessionHandle is None:
            req.sessionHandle = self.session_handle
        
        res = fn(req)
        return res
    
    def execute_statement(self, statement, max_rows=100):
        req = TExecuteStatementReq(statement=statement, confOverlay={})
        res = self.call(self._client.ExecuteStatement, req)

        return self.fetch_result(res.operationHandle, max_rows=max_rows)


    def fetch_result(self, operation_handle, orientation=TFetchOrientation.FETCH_NEXT, max_rows=100):
        fetch_req = TFetchResultsReq(operationHandle=operation_handle, orientation=orientation, maxRows=max_rows)
        res = self.call(self._client.FetchResults, fetch_req)

        if operation_handle.hasResultSet:
          meta_req = TGetResultSetMetadataReq(operationHandle=operation_handle)
          schema = self.call(self._client.GetResultSetMetadata, meta_req)
        else:
          schema = None

        return res, schema

def main():
    
    client = HiveServerClient()
    client.connect()
    client.execute_statement(statement='SET hive.server2.blocking.query=true')
    
    statement = 'select name from test'
    res, schema = client.execute_statement(statement)
    for row in res.results.rows:
        for column in row.colVals:
            print HiveServerTColumnValue(column).val


if __name__ == '__main__':
	main()
</pre>

 [1]: http://stackoverflow.com/questions/15372388/hiveserver2-java-api/16008071#16008071