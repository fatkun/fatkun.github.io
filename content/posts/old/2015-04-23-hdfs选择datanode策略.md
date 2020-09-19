---
title: hdfs选择datanode策略
author: fatkun
type: post
date: 2015-04-23T07:04:22+00:00
url: /2015/04/hdfs选择datanode策略.html
duoshuo_thread_id:
  - 6300410881951924994
wp-syntax-cache-content:
  - |
    a:7:{i:1;s:3037:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="other" style="font-family:monospace;">Error: org.apache.hadoop.ipc.RemoteException(java.io.IOException): File /user/xxx/part-r-00002 could only be replicated to 0 nodes instead of minReplication (=1).  There are 11 datanode(s) running and no node(s) are excluded in this operation.
    	at org.apache.hadoop.hdfs.server.blockmanagement.BlockManager.chooseTarget(BlockManager.java:1327)
    	at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.getAdditionalBlock(FSNamesystem.java:2278)
    	at org.apache.hadoop.hdfs.server.namenode.NameNodeRpcServer.addBlock(NameNodeRpcServer.java:480)
    	at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolServerSideTranslatorPB.addBlock(ClientNamenodeProtocolServerSideTranslatorPB.java:297)
    	at org.apache.hadoop.hdfs.protocol.proto.ClientNamenodeProtocolProtos$ClientNamenodeProtocol$2.callBlockingMethod(ClientNamenodeProtocolProtos.java:44080)
    	at org.apache.hadoop.ipc.ProtobufRpcEngine$Server$ProtoBufRpcInvoker.call(ProtobufRpcEngine.java:453)
    	at org.apache.hadoop.ipc.RPC$Server.call(RPC.java:1002)
    	at org.apache.hadoop.ipc.Server$Handler$1.run(Server.java:1695)
    	at org.apache.hadoop.ipc.Server$Handler$1.run(Server.java:1691)
    	at java.security.AccessController.doPrivileged(Native Method)
    	at javax.security.auth.Subject.doAs(Subject.java:396)
    	at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1408)
    	at org.apache.hadoop.ipc.Server$Handler.run(Server.java:1689)</pre></td></tr></table><p class="theCode" style="display:none;">Error: org.apache.hadoop.ipc.RemoteException(java.io.IOException): File /user/xxx/part-r-00002 could only be replicated to 0 nodes instead of minReplication (=1).  There are 11 datanode(s) running and no node(s) are excluded in this operation.
    	at org.apache.hadoop.hdfs.server.blockmanagement.BlockManager.chooseTarget(BlockManager.java:1327)
    	at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.getAdditionalBlock(FSNamesystem.java:2278)
    	at org.apache.hadoop.hdfs.server.namenode.NameNodeRpcServer.addBlock(NameNodeRpcServer.java:480)
    	at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolServerSideTranslatorPB.addBlock(ClientNamenodeProtocolServerSideTranslatorPB.java:297)
    	at org.apache.hadoop.hdfs.protocol.proto.ClientNamenodeProtocolProtos$ClientNamenodeProtocol$2.callBlockingMethod(ClientNamenodeProtocolProtos.java:44080)
    	at org.apache.hadoop.ipc.ProtobufRpcEngine$Server$ProtoBufRpcInvoker.call(ProtobufRpcEngine.java:453)
    	at org.apache.hadoop.ipc.RPC$Server.call(RPC.java:1002)
    	at org.apache.hadoop.ipc.Server$Handler$1.run(Server.java:1695)
    	at org.apache.hadoop.ipc.Server$Handler$1.run(Server.java:1691)
    	at java.security.AccessController.doPrivileged(Native Method)
    	at javax.security.auth.Subject.doAs(Subject.java:396)
    	at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1408)
    	at org.apache.hadoop.ipc.Server$Handler.run(Server.java:1689)</p></div>
    ";i:2;s:14301:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">  <span style="color: #666666; font-style: italic;">/* choose &lt;i&gt;numOfReplicas&lt;/i&gt; from all data nodes */</span>
      <span style="color: #000000; font-weight: bold;">private</span> DatanodeDescriptor chooseTarget<span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> numOfReplicas,
                                              DatanodeDescriptor writer,
                                              HashMap<span style="color: #339933;">&lt;</span>Node, Node<span style="color: #339933;">&gt;</span> excludedNodes,
                                              <span style="color: #000066; font-weight: bold;">long</span> blocksize,
                                              <span style="color: #000066; font-weight: bold;">int</span> maxNodesPerRack,
                                              List<span style="color: #339933;">&lt;</span>DatanodeDescriptor<span style="color: #339933;">&gt;</span> results<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>numOfReplicas <span style="color: #339933;">==</span> <span style="color: #cc66cc;">0</span> <span style="color: #339933;">&amp;</span>brvbar<span style="color: #339933;">;&amp;</span>brvbar<span style="color: #339933;">;</span> clusterMap.<span style="color: #006633;">getNumOfLeaves</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">==</span><span style="color: #cc66cc;">0</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #000000; font-weight: bold;">return</span> writer<span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
        <span style="color: #000066; font-weight: bold;">int</span> totalReplicasExpected <span style="color: #339933;">=</span> numOfReplicas<span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">// 总共需要的副本数</span>
    &nbsp;
    <span style="color: #666666; font-style: italic;">// results是当前已分配的节点</span>
        <span style="color: #000066; font-weight: bold;">int</span> numOfResults <span style="color: #339933;">=</span> results.<span style="color: #006633;">size</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #000066; font-weight: bold;">boolean</span> newBlock <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span>numOfResults<span style="color: #339933;">==</span><span style="color: #cc66cc;">0</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>writer <span style="color: #339933;">==</span> <span style="color: #000066; font-weight: bold;">null</span> <span style="color: #339933;">&amp;&amp;</span> <span style="color: #339933;">!</span>newBlock<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          writer <span style="color: #339933;">=</span> results.<span style="color: #006633;">get</span><span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">0</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #666666; font-style: italic;">// 如果还没分配过，先选择本地节点</span>
          <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>numOfResults <span style="color: #339933;">==</span> <span style="color: #cc66cc;">0</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            writer <span style="color: #339933;">=</span> chooseLocalNode<span style="color: #009900;">&#40;</span>writer, excludedNodes, 
                                     blocksize, maxNodesPerRack, results<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span><span style="color: #339933;">--</span>numOfReplicas <span style="color: #339933;">==</span> <span style="color: #cc66cc;">0</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
              <span style="color: #000000; font-weight: bold;">return</span> writer<span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
          <span style="color: #009900;">&#125;</span>
    <span style="color: #666666; font-style: italic;">// 如果之前已分配一个或零个，在其他机架的一台机器选择</span>
          <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>numOfResults <span style="color: #339933;">&lt;=</span> <span style="color: #cc66cc;">1</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            chooseRemoteRack<span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">1</span>, results.<span style="color: #006633;">get</span><span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">0</span><span style="color: #009900;">&#41;</span>, excludedNodes, 
                             blocksize, maxNodesPerRack, results<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span><span style="color: #339933;">--</span>numOfReplicas <span style="color: #339933;">==</span> <span style="color: #cc66cc;">0</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
              <span style="color: #000000; font-weight: bold;">return</span> writer<span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
          <span style="color: #009900;">&#125;</span>
    <span style="color: #666666; font-style: italic;">// 如果前面还没分配完，已有小于或等于两个副本</span>
          <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>numOfResults <span style="color: #339933;">&lt;=</span> <span style="color: #cc66cc;">2</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #666666; font-style: italic;">// 如果前两个在同一个机架上，选择一个其他机架的</span>
            <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>clusterMap.<span style="color: #006633;">isOnSameRack</span><span style="color: #009900;">&#40;</span>results.<span style="color: #006633;">get</span><span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">0</span><span style="color: #009900;">&#41;</span>, results.<span style="color: #006633;">get</span><span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">1</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
              chooseRemoteRack<span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">1</span>, results.<span style="color: #006633;">get</span><span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">0</span><span style="color: #009900;">&#41;</span>, excludedNodes,
                               blocksize, maxNodesPerRack, results<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">else</span> <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>newBlock<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#123;</span> 
              chooseLocalRack<span style="color: #009900;">&#40;</span>results.<span style="color: #006633;">get</span><span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">1</span><span style="color: #009900;">&#41;</span>, excludedNodes, blocksize, 
                              maxNodesPerRack, results<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">else</span> <span style="color: #009900;">&#123;</span>
              chooseLocalRack<span style="color: #009900;">&#40;</span>writer, excludedNodes, blocksize,
                              maxNodesPerRack, results<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
            <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span><span style="color: #339933;">--</span>numOfReplicas <span style="color: #339933;">==</span> <span style="color: #cc66cc;">0</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
              <span style="color: #000000; font-weight: bold;">return</span> writer<span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
          <span style="color: #009900;">&#125;</span>
    <span style="color: #666666; font-style: italic;">// 如果还需要副本，就随机选择</span>
          chooseRandom<span style="color: #009900;">&#40;</span>numOfReplicas, NodeBase.<span style="color: #006633;">ROOT</span>, excludedNodes, 
                       blocksize, maxNodesPerRack, results<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span>NotEnoughReplicasException e<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          LOG.<span style="color: #006633;">warn</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Not able to place enough replicas, still in need of &quot;</span>
                   <span style="color: #339933;">+</span> numOfReplicas <span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot; to reach &quot;</span> <span style="color: #339933;">+</span> totalReplicasExpected <span style="color: #339933;">+</span> <span style="color: #0000ff;">&quot;<span style="color: #000099; font-weight: bold;">\n</span>&quot;</span>
                   <span style="color: #339933;">+</span> e.<span style="color: #006633;">getMessage</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
        <span style="color: #000000; font-weight: bold;">return</span> writer<span style="color: #339933;">;</span>
      <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">  /* choose &lt;i&gt;numOfReplicas&lt;/i&gt; from all data nodes */
      private DatanodeDescriptor chooseTarget(int numOfReplicas,
                                              DatanodeDescriptor writer,
                                              HashMap&lt;Node, Node&gt; excludedNodes,
                                              long blocksize,
                                              int maxNodesPerRack,
                                              List&lt;DatanodeDescriptor&gt; results) {
          
        if (numOfReplicas == 0 &amp;brvbar;&amp;brvbar; clusterMap.getNumOfLeaves()==0) {
          return writer;
        }
        int totalReplicasExpected = numOfReplicas; // 总共需要的副本数
          
    // results是当前已分配的节点
        int numOfResults = results.size();
        boolean newBlock = (numOfResults==0);
        if (writer == null &amp;&amp; !newBlock) {
          writer = results.get(0);
        }
          
        try {
    // 如果还没分配过，先选择本地节点
          if (numOfResults == 0) {
            writer = chooseLocalNode(writer, excludedNodes, 
                                     blocksize, maxNodesPerRack, results);
            if (--numOfReplicas == 0) {
              return writer;
            }
          }
    // 如果之前已分配一个或零个，在其他机架的一台机器选择
          if (numOfResults &lt;= 1) {
            chooseRemoteRack(1, results.get(0), excludedNodes, 
                             blocksize, maxNodesPerRack, results);
            if (--numOfReplicas == 0) {
              return writer;
            }
          }
    // 如果前面还没分配完，已有小于或等于两个副本
          if (numOfResults &lt;= 2) {
            // 如果前两个在同一个机架上，选择一个其他机架的
            if (clusterMap.isOnSameRack(results.get(0), results.get(1))) {
              chooseRemoteRack(1, results.get(0), excludedNodes,
                               blocksize, maxNodesPerRack, results);
            } else if (newBlock){ 
              chooseLocalRack(results.get(1), excludedNodes, blocksize, 
                              maxNodesPerRack, results);
            } else {
              chooseLocalRack(writer, excludedNodes, blocksize,
                              maxNodesPerRack, results);
            }
            if (--numOfReplicas == 0) {
              return writer;
            }
          }
    // 如果还需要副本，就随机选择
          chooseRandom(numOfReplicas, NodeBase.ROOT, excludedNodes, 
                       blocksize, maxNodesPerRack, results);
        } catch (NotEnoughReplicasException e) {
          LOG.warn(&quot;Not able to place enough replicas, still in need of &quot;
                   + numOfReplicas + &quot; to reach &quot; + totalReplicasExpected + &quot;\n&quot;
                   + e.getMessage());
        }
        return writer;
      }</p></div>
    ";i:3;s:6630:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #666666; font-style: italic;">/* choose &lt;i&gt;localMachine&lt;/i&gt; as the target.
       * if &lt;i&gt;localMachine&lt;/i&gt; is not available, 
       * choose a node on the same rack
       * @return the chosen node
       */</span>
      <span style="color: #000000; font-weight: bold;">private</span> DatanodeDescriptor chooseLocalNode<span style="color: #009900;">&#40;</span>
                                                 DatanodeDescriptor localMachine,
                                                 HashMap<span style="color: #339933;">&lt;</span>Node, Node<span style="color: #339933;">&gt;</span> excludedNodes,
                                                 <span style="color: #000066; font-weight: bold;">long</span> blocksize,
                                                 <span style="color: #000066; font-weight: bold;">int</span> maxNodesPerRack,
                                                 List<span style="color: #339933;">&lt;</span>DatanodeDescriptor<span style="color: #339933;">&gt;</span> results<span style="color: #009900;">&#41;</span>
        <span style="color: #000000; font-weight: bold;">throws</span> NotEnoughReplicasException <span style="color: #009900;">&#123;</span>
        <span style="color: #666666; font-style: italic;">// if no local machine, randomly choose one node 如果没有本地机器，随机选择一个</span>
        <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>localMachine <span style="color: #339933;">==</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span>
          <span style="color: #000000; font-weight: bold;">return</span> chooseRandom<span style="color: #009900;">&#40;</span>NodeBase.<span style="color: #006633;">ROOT</span>, excludedNodes, 
                              blocksize, maxNodesPerRack, results<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>preferLocalNode<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span> <span style="color: #666666; font-style: italic;">// 这个值写死为true</span>
          <span style="color: #666666; font-style: italic;">// otherwise try local machine first</span>
          Node oldNode <span style="color: #339933;">=</span> excludedNodes.<span style="color: #006633;">put</span><span style="color: #009900;">&#40;</span>localMachine, localMachine<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">// 把当前节点先加入排除列表</span>
          <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>oldNode <span style="color: #339933;">==</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span> <span style="color: #666666; font-style: italic;">// was not in the excluded list 如果返回null表示之前没有在排除列表里</span>
            <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>isGoodTarget<span style="color: #009900;">&#40;</span>localMachine, blocksize,
                             maxNodesPerRack, <span style="color: #000066; font-weight: bold;">false</span>, results<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span><span style="color: #666666; font-style: italic;">//判断是否好的目标，后面再看这个方法</span>
              results.<span style="color: #006633;">add</span><span style="color: #009900;">&#40;</span>localMachine<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
              <span style="color: #000000; font-weight: bold;">return</span> localMachine<span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
          <span style="color: #009900;">&#125;</span> 
        <span style="color: #009900;">&#125;</span>      
        <span style="color: #666666; font-style: italic;">// try a node on local rack</span>
        <span style="color: #000000; font-weight: bold;">return</span> chooseLocalRack<span style="color: #009900;">&#40;</span>localMachine, excludedNodes, 
                               blocksize, maxNodesPerRack, results<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #666666; font-style: italic;">// 如果本机不适合，选择同机架的其他机器</span>
      <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">/* choose &lt;i&gt;localMachine&lt;/i&gt; as the target.
       * if &lt;i&gt;localMachine&lt;/i&gt; is not available, 
       * choose a node on the same rack
       * @return the chosen node
       */
      private DatanodeDescriptor chooseLocalNode(
                                                 DatanodeDescriptor localMachine,
                                                 HashMap&lt;Node, Node&gt; excludedNodes,
                                                 long blocksize,
                                                 int maxNodesPerRack,
                                                 List&lt;DatanodeDescriptor&gt; results)
        throws NotEnoughReplicasException {
        // if no local machine, randomly choose one node 如果没有本地机器，随机选择一个
        if (localMachine == null)
          return chooseRandom(NodeBase.ROOT, excludedNodes, 
                              blocksize, maxNodesPerRack, results);
        if (preferLocalNode) { // 这个值写死为true
          // otherwise try local machine first
          Node oldNode = excludedNodes.put(localMachine, localMachine); // 把当前节点先加入排除列表
          if (oldNode == null) { // was not in the excluded list 如果返回null表示之前没有在排除列表里
            if (isGoodTarget(localMachine, blocksize,
                             maxNodesPerRack, false, results)) {//判断是否好的目标，后面再看这个方法
              results.add(localMachine);
              return localMachine;
            }
          } 
        }      
        // try a node on local rack
        return chooseLocalRack(localMachine, excludedNodes, 
                               blocksize, maxNodesPerRack, results);// 如果本机不适合，选择同机架的其他机器
      }</p></div>
    ";i:4;s:9950:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">  <span style="color: #666666; font-style: italic;">/* choose one node from the rack that &lt;i&gt;localMachine&lt;/i&gt; is on.
       * if no such node is available, choose one node from the rack where
       * a second replica is on.
       * if still no such node is available, choose a random node 
       * in the cluster.
       * @return the chosen node
       */</span>
      <span style="color: #000000; font-weight: bold;">private</span> DatanodeDescriptor chooseLocalRack<span style="color: #009900;">&#40;</span>
                                                 DatanodeDescriptor localMachine,
                                                 HashMap<span style="color: #339933;">&lt;</span>Node, Node<span style="color: #339933;">&gt;</span> excludedNodes,
                                                 <span style="color: #000066; font-weight: bold;">long</span> blocksize,
                                                 <span style="color: #000066; font-weight: bold;">int</span> maxNodesPerRack,
                                                 List<span style="color: #339933;">&lt;</span>DatanodeDescriptor<span style="color: #339933;">&gt;</span> results<span style="color: #009900;">&#41;</span>
        <span style="color: #000000; font-weight: bold;">throws</span> NotEnoughReplicasException <span style="color: #009900;">&#123;</span>
        <span style="color: #666666; font-style: italic;">// no local machine, so choose a random machine</span>
        <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>localMachine <span style="color: #339933;">==</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #000000; font-weight: bold;">return</span> chooseRandom<span style="color: #009900;">&#40;</span>NodeBase.<span style="color: #006633;">ROOT</span>, excludedNodes, 
                              blocksize, maxNodesPerRack, results<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        <span style="color: #666666; font-style: italic;">// choose one from the local rack 选择同一个机架的</span>
        <span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #000000; font-weight: bold;">return</span> chooseRandom<span style="color: #009900;">&#40;</span>
                              localMachine.<span style="color: #006633;">getNetworkLocation</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>,
                              excludedNodes, blocksize, maxNodesPerRack, results<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span>NotEnoughReplicasException e1<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #666666; font-style: italic;">// find the second replica 从已有副本里面找同一个机架的</span>
          DatanodeDescriptor newLocal<span style="color: #339933;">=</span><span style="color: #000066; font-weight: bold;">null</span><span style="color: #339933;">;</span>
          <span style="color: #000000; font-weight: bold;">for</span><span style="color: #009900;">&#40;</span>Iterator<span style="color: #339933;">&lt;</span>DatanodeDescriptor<span style="color: #339933;">&gt;</span> iter<span style="color: #339933;">=</span>results.<span style="color: #006633;">iterator</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
              iter.<span style="color: #006633;">hasNext</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            DatanodeDescriptor nextNode <span style="color: #339933;">=</span> iter.<span style="color: #006633;">next</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>nextNode <span style="color: #339933;">!=</span> localMachine<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
              newLocal <span style="color: #339933;">=</span> nextNode<span style="color: #339933;">;</span>
              <span style="color: #000000; font-weight: bold;">break</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
          <span style="color: #009900;">&#125;</span>
          <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>newLocal <span style="color: #339933;">!=</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#123;</span>
              <span style="color: #000000; font-weight: bold;">return</span> chooseRandom<span style="color: #009900;">&#40;</span>
                                  newLocal.<span style="color: #006633;">getNetworkLocation</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>,
                                  excludedNodes, blocksize, maxNodesPerRack, results<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span><span style="color: #009900;">&#40;</span>NotEnoughReplicasException e2<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
              <span style="color: #666666; font-style: italic;">//otherwise randomly choose one from the network 如果还是找不到，随机选择</span>
              <span style="color: #000000; font-weight: bold;">return</span> chooseRandom<span style="color: #009900;">&#40;</span>NodeBase.<span style="color: #006633;">ROOT</span>, excludedNodes,
                                  blocksize, maxNodesPerRack, results<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
          <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">else</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #666666; font-style: italic;">//otherwise randomly choose one from the network</span>
            <span style="color: #000000; font-weight: bold;">return</span> chooseRandom<span style="color: #009900;">&#40;</span>NodeBase.<span style="color: #006633;">ROOT</span>, excludedNodes,
                                blocksize, maxNodesPerRack, results<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #009900;">&#125;</span>
        <span style="color: #009900;">&#125;</span>
      <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">  /* choose one node from the rack that &lt;i&gt;localMachine&lt;/i&gt; is on.
       * if no such node is available, choose one node from the rack where
       * a second replica is on.
       * if still no such node is available, choose a random node 
       * in the cluster.
       * @return the chosen node
       */
      private DatanodeDescriptor chooseLocalRack(
                                                 DatanodeDescriptor localMachine,
                                                 HashMap&lt;Node, Node&gt; excludedNodes,
                                                 long blocksize,
                                                 int maxNodesPerRack,
                                                 List&lt;DatanodeDescriptor&gt; results)
        throws NotEnoughReplicasException {
        // no local machine, so choose a random machine
        if (localMachine == null) {
          return chooseRandom(NodeBase.ROOT, excludedNodes, 
                              blocksize, maxNodesPerRack, results);
        }
          
        // choose one from the local rack 选择同一个机架的
        try {
          return chooseRandom(
                              localMachine.getNetworkLocation(),
                              excludedNodes, blocksize, maxNodesPerRack, results);
        } catch (NotEnoughReplicasException e1) {
          // find the second replica 从已有副本里面找同一个机架的
          DatanodeDescriptor newLocal=null;
          for(Iterator&lt;DatanodeDescriptor&gt; iter=results.iterator();
              iter.hasNext();) {
            DatanodeDescriptor nextNode = iter.next();
            if (nextNode != localMachine) {
              newLocal = nextNode;
              break;
            }
          }
          if (newLocal != null) {
            try {
              return chooseRandom(
                                  newLocal.getNetworkLocation(),
                                  excludedNodes, blocksize, maxNodesPerRack, results);
            } catch(NotEnoughReplicasException e2) {
              //otherwise randomly choose one from the network 如果还是找不到，随机选择
              return chooseRandom(NodeBase.ROOT, excludedNodes,
                                  blocksize, maxNodesPerRack, results);
            }
          } else {
            //otherwise randomly choose one from the network
            return chooseRandom(NodeBase.ROOT, excludedNodes,
                                blocksize, maxNodesPerRack, results);
          }
        }
      }</p></div>
    ";i:5;s:4961:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">  <span style="color: #666666; font-style: italic;">/* choose &lt;i&gt;numOfReplicas&lt;/i&gt; nodes from the racks 
       * that &lt;i&gt;localMachine&lt;/i&gt; is NOT on.
       * if not enough nodes are available, choose the remaining ones 
       * from the local rack
       */</span>
    &nbsp;
      <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000066; font-weight: bold;">void</span> chooseRemoteRack<span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> numOfReplicas,
                                    DatanodeDescriptor localMachine,
                                    HashMap<span style="color: #339933;">&lt;</span>Node, Node<span style="color: #339933;">&gt;</span> excludedNodes,
                                    <span style="color: #000066; font-weight: bold;">long</span> blocksize,
                                    <span style="color: #000066; font-weight: bold;">int</span> maxReplicasPerRack,
                                    List<span style="color: #339933;">&lt;</span>DatanodeDescriptor<span style="color: #339933;">&gt;</span> results<span style="color: #009900;">&#41;</span>
        <span style="color: #000000; font-weight: bold;">throws</span> NotEnoughReplicasException <span style="color: #009900;">&#123;</span>
        <span style="color: #000066; font-weight: bold;">int</span> oldNumOfReplicas <span style="color: #339933;">=</span> results.<span style="color: #006633;">size</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #666666; font-style: italic;">// randomly choose one node from remote racks 选择其他机架的节点，注意这里的&quot;~&quot;是表示排除本机架，如果找不到就只有在本机架找</span>
        <span style="color: #000000; font-weight: bold;">try</span> <span style="color: #009900;">&#123;</span>
          chooseRandom<span style="color: #009900;">&#40;</span>numOfReplicas, <span style="color: #0000ff;">&quot;~&quot;</span><span style="color: #339933;">+</span>localMachine.<span style="color: #006633;">getNetworkLocation</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>,
                       excludedNodes, blocksize, maxReplicasPerRack, results<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">catch</span> <span style="color: #009900;">&#40;</span>NotEnoughReplicasException e<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          chooseRandom<span style="color: #009900;">&#40;</span>numOfReplicas<span style="color: #339933;">-</span><span style="color: #009900;">&#40;</span>results.<span style="color: #006633;">size</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">-</span>oldNumOfReplicas<span style="color: #009900;">&#41;</span>,
                       localMachine.<span style="color: #006633;">getNetworkLocation</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, excludedNodes, blocksize, 
                       maxReplicasPerRack, results<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
      <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">  /* choose &lt;i&gt;numOfReplicas&lt;/i&gt; nodes from the racks 
       * that &lt;i&gt;localMachine&lt;/i&gt; is NOT on.
       * if not enough nodes are available, choose the remaining ones 
       * from the local rack
       */
        
      private void chooseRemoteRack(int numOfReplicas,
                                    DatanodeDescriptor localMachine,
                                    HashMap&lt;Node, Node&gt; excludedNodes,
                                    long blocksize,
                                    int maxReplicasPerRack,
                                    List&lt;DatanodeDescriptor&gt; results)
        throws NotEnoughReplicasException {
        int oldNumOfReplicas = results.size();
        // randomly choose one node from remote racks 选择其他机架的节点，注意这里的&quot;~&quot;是表示排除本机架，如果找不到就只有在本机架找
        try {
          chooseRandom(numOfReplicas, &quot;~&quot;+localMachine.getNetworkLocation(),
                       excludedNodes, blocksize, maxReplicasPerRack, results);
        } catch (NotEnoughReplicasException e) {
          chooseRandom(numOfReplicas-(results.size()-oldNumOfReplicas),
                       localMachine.getNetworkLocation(), excludedNodes, blocksize, 
                       maxReplicasPerRack, results);
        }
      }</p></div>
    ";i:6;s:10265:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">  <span style="color: #666666; font-style: italic;">/* Randomly choose &lt;i&gt;numOfReplicas&lt;/i&gt; targets from &lt;i&gt;nodes&lt;/i&gt;.
       */</span>
      <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000066; font-weight: bold;">void</span> chooseRandom<span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> numOfReplicas,
                                <span style="color: #003399;">String</span> nodes,
                                HashMap<span style="color: #339933;">&lt;</span>Node, Node<span style="color: #339933;">&gt;</span> excludedNodes,
                                <span style="color: #000066; font-weight: bold;">long</span> blocksize,
                                <span style="color: #000066; font-weight: bold;">int</span> maxNodesPerRack,
                                List<span style="color: #339933;">&lt;</span>DatanodeDescriptor<span style="color: #339933;">&gt;</span> results<span style="color: #009900;">&#41;</span>
        <span style="color: #000000; font-weight: bold;">throws</span> NotEnoughReplicasException <span style="color: #009900;">&#123;</span>
    &nbsp;
        <span style="color: #000066; font-weight: bold;">int</span> numOfAvailableNodes <span style="color: #339933;">=</span>
          clusterMap.<span style="color: #006633;">countNumOfAvailableNodes</span><span style="color: #009900;">&#40;</span>nodes, excludedNodes.<span style="color: #006633;">keySet</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">// 当前可用节点数</span>
        StringBuilder builder <span style="color: #339933;">=</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #339933;">;</span>
        <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>LOG.<span style="color: #006633;">isDebugEnabled</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          builder <span style="color: #339933;">=</span> threadLocalBuilder.<span style="color: #006633;">get</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          builder.<span style="color: #006633;">setLength</span><span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">0</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          builder.<span style="color: #006633;">append</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;[&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
        <span style="color: #000066; font-weight: bold;">boolean</span> badTarget <span style="color: #339933;">=</span> <span style="color: #000066; font-weight: bold;">false</span><span style="color: #339933;">;</span>
        <span style="color: #000000; font-weight: bold;">while</span><span style="color: #009900;">&#40;</span>numOfReplicas <span style="color: #339933;">&gt;</span> <span style="color: #cc66cc;">0</span> <span style="color: #339933;">&amp;&amp;</span> numOfAvailableNodes <span style="color: #339933;">&gt;</span> <span style="color: #cc66cc;">0</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span> <span style="color: #666666; font-style: italic;">// 循环直到所有可用副本数为0</span>
          DatanodeDescriptor chosenNode <span style="color: #339933;">=</span> 
            <span style="color: #009900;">&#40;</span>DatanodeDescriptor<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#40;</span>clusterMap.<span style="color: #006633;">chooseRandom</span><span style="color: #009900;">&#40;</span>nodes<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          Node oldNode <span style="color: #339933;">=</span> excludedNodes.<span style="color: #006633;">put</span><span style="color: #009900;">&#40;</span>chosenNode, chosenNode<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>oldNode <span style="color: #339933;">==</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            numOfAvailableNodes<span style="color: #339933;">--;</span>
    &nbsp;
            <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>isGoodTarget<span style="color: #009900;">&#40;</span>chosenNode, blocksize, maxNodesPerRack, results<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
              numOfReplicas<span style="color: #339933;">--;</span>
              results.<span style="color: #006633;">add</span><span style="color: #009900;">&#40;</span>chosenNode<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">else</span> <span style="color: #009900;">&#123;</span>
              badTarget <span style="color: #339933;">=</span> <span style="color: #000066; font-weight: bold;">true</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
          <span style="color: #009900;">&#125;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>numOfReplicas<span style="color: #339933;">&gt;</span><span style="color: #cc66cc;">0</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #003399;">String</span> detail <span style="color: #339933;">=</span> enableDebugLogging<span style="color: #339933;">;</span>
          <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>LOG.<span style="color: #006633;">isDebugEnabled</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>badTarget <span style="color: #339933;">&amp;&amp;</span> builder <span style="color: #339933;">!=</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
              detail <span style="color: #339933;">=</span> builder.<span style="color: #006633;">append</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;]&quot;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">toString</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
              builder.<span style="color: #006633;">setLength</span><span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">0</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">else</span> detail <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;&quot;</span><span style="color: #339933;">;</span>
          <span style="color: #009900;">&#125;</span>
          <span style="color: #000000; font-weight: bold;">throw</span> <span style="color: #000000; font-weight: bold;">new</span> NotEnoughReplicasException<span style="color: #009900;">&#40;</span>detail<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
      <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">  /* Randomly choose &lt;i&gt;numOfReplicas&lt;/i&gt; targets from &lt;i&gt;nodes&lt;/i&gt;.
       */
      private void chooseRandom(int numOfReplicas,
                                String nodes,
                                HashMap&lt;Node, Node&gt; excludedNodes,
                                long blocksize,
                                int maxNodesPerRack,
                                List&lt;DatanodeDescriptor&gt; results)
        throws NotEnoughReplicasException {
          
        int numOfAvailableNodes =
          clusterMap.countNumOfAvailableNodes(nodes, excludedNodes.keySet()); // 当前可用节点数
        StringBuilder builder = null;
        if (LOG.isDebugEnabled()) {
          builder = threadLocalBuilder.get();
          builder.setLength(0);
          builder.append(&quot;[&quot;);
        }
        boolean badTarget = false;
        while(numOfReplicas &gt; 0 &amp;&amp; numOfAvailableNodes &gt; 0) { // 循环直到所有可用副本数为0
          DatanodeDescriptor chosenNode = 
            (DatanodeDescriptor)(clusterMap.chooseRandom(nodes));
          Node oldNode = excludedNodes.put(chosenNode, chosenNode);
          if (oldNode == null) {
            numOfAvailableNodes--;
    
            if (isGoodTarget(chosenNode, blocksize, maxNodesPerRack, results)) {
              numOfReplicas--;
              results.add(chosenNode);
            } else {
              badTarget = true;
            }
          }
        }
          
        if (numOfReplicas&gt;0) {
          String detail = enableDebugLogging;
          if (LOG.isDebugEnabled()) {
            if (badTarget &amp;&amp; builder != null) {
              detail = builder.append(&quot;]&quot;).toString();
              builder.setLength(0);
            } else detail = &quot;&quot;;
          }
          throw new NotEnoughReplicasException(detail);
        }
      }</p></div>
    ";i:7;s:21670:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">  <span style="color: #666666; font-style: italic;">/* judge if a node is a good target.
       * return true if &lt;i&gt;node&lt;/i&gt; has enough space, 
       * does not have too much load, and the rack does not have too many nodes
       */</span>
      <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000066; font-weight: bold;">boolean</span> isGoodTarget<span style="color: #009900;">&#40;</span>DatanodeDescriptor node,
                                   <span style="color: #000066; font-weight: bold;">long</span> blockSize, <span style="color: #000066; font-weight: bold;">int</span> maxTargetPerLoc,
                                   List<span style="color: #339933;">&lt;</span>DatanodeDescriptor<span style="color: #339933;">&gt;</span> results<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
        <span style="color: #000000; font-weight: bold;">return</span> isGoodTarget<span style="color: #009900;">&#40;</span>node, blockSize, maxTargetPerLoc,
                            <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">considerLoad</span>, results<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
      <span style="color: #009900;">&#125;</span>
    &nbsp;
      <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000066; font-weight: bold;">boolean</span> isGoodTarget<span style="color: #009900;">&#40;</span>DatanodeDescriptor node,
                                   <span style="color: #000066; font-weight: bold;">long</span> blockSize, <span style="color: #000066; font-weight: bold;">int</span> maxTargetPerLoc,
                                   <span style="color: #000066; font-weight: bold;">boolean</span> considerLoad,
                                   List<span style="color: #339933;">&lt;</span>DatanodeDescriptor<span style="color: #339933;">&gt;</span> results<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
        <span style="color: #666666; font-style: italic;">// check if the node is (being) decommissed 判断是否退役了</span>
        <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>node.<span style="color: #006633;">isDecommissionInProgress</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">&amp;</span>brvbar<span style="color: #339933;">;&amp;</span>brvbar<span style="color: #339933;">;</span> node.<span style="color: #006633;">isDecommissioned</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #000000; font-weight: bold;">if</span><span style="color: #009900;">&#40;</span>LOG.<span style="color: #006633;">isDebugEnabled</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            threadLocalBuilder.<span style="color: #006633;">get</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">append</span><span style="color: #009900;">&#40;</span>node.<span style="color: #006633;">toString</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">append</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;: &quot;</span><span style="color: #009900;">&#41;</span>
              .<span style="color: #006633;">append</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Node &quot;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">append</span><span style="color: #009900;">&#40;</span>NodeBase.<span style="color: #006633;">getPath</span><span style="color: #009900;">&#40;</span>node<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span>
              .<span style="color: #006633;">append</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot; is not chosen because the node is (being) decommissioned &quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #009900;">&#125;</span>
          <span style="color: #000000; font-weight: bold;">return</span> <span style="color: #000066; font-weight: bold;">false</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        <span style="color: #000066; font-weight: bold;">long</span> remaining <span style="color: #339933;">=</span> node.<span style="color: #006633;">getRemaining</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">-</span> 
                         <span style="color: #009900;">&#40;</span>node.<span style="color: #006633;">getBlocksScheduled</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">*</span> blockSize<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> 
        <span style="color: #666666; font-style: italic;">// check the remaining capacity of the target machine 判断剩余的磁盘空间， 块大小 * 5 &gt; 剩余大小 表示不可用</span>
        <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>blockSize<span style="color: #339933;">*</span> HdfsConstants.<span style="color: #006633;">MIN_BLOCKS_FOR_WRITE</span><span style="color: #339933;">&gt;</span>remaining<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #000000; font-weight: bold;">if</span><span style="color: #009900;">&#40;</span>LOG.<span style="color: #006633;">isDebugEnabled</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            threadLocalBuilder.<span style="color: #006633;">get</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">append</span><span style="color: #009900;">&#40;</span>node.<span style="color: #006633;">toString</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">append</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;: &quot;</span><span style="color: #009900;">&#41;</span>
              .<span style="color: #006633;">append</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Node &quot;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">append</span><span style="color: #009900;">&#40;</span>NodeBase.<span style="color: #006633;">getPath</span><span style="color: #009900;">&#40;</span>node<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span>
              .<span style="color: #006633;">append</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot; is not chosen because the node does not have enough space &quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #009900;">&#125;</span>
          <span style="color: #000000; font-weight: bold;">return</span> <span style="color: #000066; font-weight: bold;">false</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        <span style="color: #666666; font-style: italic;">// check the communication traffic of the target machine 判断各个datanode的负载情况，这里的负载不是系统负载，而是根据xceiver线程数，这个线程好像是负责读写的。</span>
        <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>considerLoad<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span> <span style="color: #666666; font-style: italic;">// 默认这个为true，配置项 dfs.namenode.replication.considerLoad</span>
          <span style="color: #000066; font-weight: bold;">double</span> avgLoad <span style="color: #339933;">=</span> <span style="color: #cc66cc;">0</span><span style="color: #339933;">;</span>
          <span style="color: #000066; font-weight: bold;">int</span> size <span style="color: #339933;">=</span> clusterMap.<span style="color: #006633;">getNumOfLeaves</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">// 所有datanode数</span>
          <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>size <span style="color: #339933;">!=</span> <span style="color: #cc66cc;">0</span> <span style="color: #339933;">&amp;&amp;</span> stats <span style="color: #339933;">!=</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            avgLoad <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">double</span><span style="color: #009900;">&#41;</span>stats.<span style="color: #006633;">getTotalLoad</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">/</span>size<span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">// 获取总的xceiver线程数除以所有datanode数，算出平均负载</span>
          <span style="color: #009900;">&#125;</span>
          <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>node.<span style="color: #006633;">getXceiverCount</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">&gt;</span> <span style="color: #009900;">&#40;</span><span style="color: #cc66cc;">2.0</span> <span style="color: #339933;">*</span> avgLoad<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span> <span style="color: #666666; font-style: italic;">// 如果当前线程数 大于 平均值的两倍，则不可使用</span>
            <span style="color: #000000; font-weight: bold;">if</span><span style="color: #009900;">&#40;</span>LOG.<span style="color: #006633;">isDebugEnabled</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
              threadLocalBuilder.<span style="color: #006633;">get</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">append</span><span style="color: #009900;">&#40;</span>node.<span style="color: #006633;">toString</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">append</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;: &quot;</span><span style="color: #009900;">&#41;</span>
                .<span style="color: #006633;">append</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Node &quot;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">append</span><span style="color: #009900;">&#40;</span>NodeBase.<span style="color: #006633;">getPath</span><span style="color: #009900;">&#40;</span>node<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span>
                .<span style="color: #006633;">append</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot; is not chosen because the node is too busy &quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
            <span style="color: #000000; font-weight: bold;">return</span> <span style="color: #000066; font-weight: bold;">false</span><span style="color: #339933;">;</span>
          <span style="color: #009900;">&#125;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        <span style="color: #666666; font-style: italic;">// check if the target rack has chosen too many nodes 检查是否有太多节点在当前机架上</span>
        <span style="color: #003399;">String</span> rackname <span style="color: #339933;">=</span> node.<span style="color: #006633;">getNetworkLocation</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #000066; font-weight: bold;">int</span> counter<span style="color: #339933;">=</span><span style="color: #cc66cc;">1</span><span style="color: #339933;">;</span>
        <span style="color: #000000; font-weight: bold;">for</span><span style="color: #009900;">&#40;</span>Iterator<span style="color: #339933;">&lt;</span>DatanodeDescriptor<span style="color: #339933;">&gt;</span> iter <span style="color: #339933;">=</span> results.<span style="color: #006633;">iterator</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            iter.<span style="color: #006633;">hasNext</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          Node result <span style="color: #339933;">=</span> iter.<span style="color: #006633;">next</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>rackname.<span style="color: #006633;">equals</span><span style="color: #009900;">&#40;</span>result.<span style="color: #006633;">getNetworkLocation</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            counter<span style="color: #339933;">++;</span>
          <span style="color: #009900;">&#125;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
    <span style="color: #666666; font-style: italic;">//maxNodesPerRack的算法，没看懂，可能是每个机架的平均数+2，不知道为什么定一个这样的值 int maxNodesPerRack = (totalNumOfReplicas-1)/clusterMap.getNumOfRacks()+2;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>counter<span style="color: #339933;">&gt;</span>maxTargetPerLoc<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
          <span style="color: #000000; font-weight: bold;">if</span><span style="color: #009900;">&#40;</span>LOG.<span style="color: #006633;">isDebugEnabled</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            threadLocalBuilder.<span style="color: #006633;">get</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">append</span><span style="color: #009900;">&#40;</span>node.<span style="color: #006633;">toString</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">append</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;: &quot;</span><span style="color: #009900;">&#41;</span>
              .<span style="color: #006633;">append</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;Node &quot;</span><span style="color: #009900;">&#41;</span>.<span style="color: #006633;">append</span><span style="color: #009900;">&#40;</span>NodeBase.<span style="color: #006633;">getPath</span><span style="color: #009900;">&#40;</span>node<span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span>
              .<span style="color: #006633;">append</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot; is not chosen because the rack has too many chosen nodes &quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
          <span style="color: #009900;">&#125;</span>
          <span style="color: #000000; font-weight: bold;">return</span> <span style="color: #000066; font-weight: bold;">false</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
        <span style="color: #000000; font-weight: bold;">return</span> <span style="color: #000066; font-weight: bold;">true</span><span style="color: #339933;">;</span>
      <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">  /* judge if a node is a good target.
       * return true if &lt;i&gt;node&lt;/i&gt; has enough space, 
       * does not have too much load, and the rack does not have too many nodes
       */
      private boolean isGoodTarget(DatanodeDescriptor node,
                                   long blockSize, int maxTargetPerLoc,
                                   List&lt;DatanodeDescriptor&gt; results) {
        return isGoodTarget(node, blockSize, maxTargetPerLoc,
                            this.considerLoad, results);
      }
        
      private boolean isGoodTarget(DatanodeDescriptor node,
                                   long blockSize, int maxTargetPerLoc,
                                   boolean considerLoad,
                                   List&lt;DatanodeDescriptor&gt; results) {
        // check if the node is (being) decommissed 判断是否退役了
        if (node.isDecommissionInProgress() &amp;brvbar;&amp;brvbar; node.isDecommissioned()) {
          if(LOG.isDebugEnabled()) {
            threadLocalBuilder.get().append(node.toString()).append(&quot;: &quot;)
              .append(&quot;Node &quot;).append(NodeBase.getPath(node))
              .append(&quot; is not chosen because the node is (being) decommissioned &quot;);
          }
          return false;
        }
    
        long remaining = node.getRemaining() - 
                         (node.getBlocksScheduled() * blockSize); 
        // check the remaining capacity of the target machine 判断剩余的磁盘空间， 块大小 * 5 &gt; 剩余大小 表示不可用
        if (blockSize* HdfsConstants.MIN_BLOCKS_FOR_WRITE&gt;remaining) {
          if(LOG.isDebugEnabled()) {
            threadLocalBuilder.get().append(node.toString()).append(&quot;: &quot;)
              .append(&quot;Node &quot;).append(NodeBase.getPath(node))
              .append(&quot; is not chosen because the node does not have enough space &quot;);
          }
          return false;
        }
          
        // check the communication traffic of the target machine 判断各个datanode的负载情况，这里的负载不是系统负载，而是根据xceiver线程数，这个线程好像是负责读写的。
        if (considerLoad) { // 默认这个为true，配置项 dfs.namenode.replication.considerLoad
          double avgLoad = 0;
          int size = clusterMap.getNumOfLeaves(); // 所有datanode数
          if (size != 0 &amp;&amp; stats != null) {
            avgLoad = (double)stats.getTotalLoad()/size; // 获取总的xceiver线程数除以所有datanode数，算出平均负载
          }
          if (node.getXceiverCount() &gt; (2.0 * avgLoad)) { // 如果当前线程数 大于 平均值的两倍，则不可使用
            if(LOG.isDebugEnabled()) {
              threadLocalBuilder.get().append(node.toString()).append(&quot;: &quot;)
                .append(&quot;Node &quot;).append(NodeBase.getPath(node))
                .append(&quot; is not chosen because the node is too busy &quot;);
            }
            return false;
          }
        }
          
        // check if the target rack has chosen too many nodes 检查是否有太多节点在当前机架上
        String rackname = node.getNetworkLocation();
        int counter=1;
        for(Iterator&lt;DatanodeDescriptor&gt; iter = results.iterator();
            iter.hasNext();) {
          Node result = iter.next();
          if (rackname.equals(result.getNetworkLocation())) {
            counter++;
          }
        }
    
    //maxNodesPerRack的算法，没看懂，可能是每个机架的平均数+2，不知道为什么定一个这样的值 int maxNodesPerRack = (totalNumOfReplicas-1)/clusterMap.getNumOfRacks()+2;
    
        if (counter&gt;maxTargetPerLoc) {
          if(LOG.isDebugEnabled()) {
            threadLocalBuilder.get().append(node.toString()).append(&quot;: &quot;)
              .append(&quot;Node &quot;).append(NodeBase.getPath(node))
              .append(&quot; is not chosen because the rack has too many chosen nodes &quot;);
          }
          return false;
        }
        return true;
      }</p></div>
    ";}
categories:
  - hadoop
  - 未分类

---
前几天报错如下：
<pre lang="other" escaped="true">Error: org.apache.hadoop.ipc.RemoteException(java.io.IOException): File /user/xxx/part-r-00002 could only be replicated to 0 nodes instead of minReplication (=1).  There are 11 datanode(s) running and no node(s) are excluded in this operation.
	at org.apache.hadoop.hdfs.server.blockmanagement.BlockManager.chooseTarget(BlockManager.java:1327)
	at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.getAdditionalBlock(FSNamesystem.java:2278)
	at org.apache.hadoop.hdfs.server.namenode.NameNodeRpcServer.addBlock(NameNodeRpcServer.java:480)
	at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolServerSideTranslatorPB.addBlock(ClientNamenodeProtocolServerSideTranslatorPB.java:297)
	at org.apache.hadoop.hdfs.protocol.proto.ClientNamenodeProtocolProtos$ClientNamenodeProtocol$2.callBlockingMethod(ClientNamenodeProtocolProtos.java:44080)
	at org.apache.hadoop.ipc.ProtobufRpcEngine$Server$ProtoBufRpcInvoker.call(ProtobufRpcEngine.java:453)
	at org.apache.hadoop.ipc.RPC$Server.call(RPC.java:1002)
	at org.apache.hadoop.ipc.Server$Handler$1.run(Server.java:1695)
	at org.apache.hadoop.ipc.Server$Handler$1.run(Server.java:1691)
	at java.security.AccessController.doPrivileged(Native Method)
	at javax.security.auth.Subject.doAs(Subject.java:396)
	at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1408)
	at org.apache.hadoop.ipc.Server$Handler.run(Server.java:1689)</pre>
阅读一下代码了解hdfs选择块的策略，可能理解有误，如果有错误请指出，代码来自cdh-4.2.1版本
在 FSNamesystem.getAdditionalBlock()里，有个blockManager.chooseTarget(src, replication, clientNode, excludedNodes, blockSize);  
这个方法用来决定在那个节点写数据
代码文件：hadoop-2.0.0-cdh4.2.1\src\hadoop-hdfs-project\hadoop-hdfs\src\main\java\org\apache\hadoop\hdfs\server\blockmanagement\BlockPlacementPolicyDefault.java
chooseTarget方法调用了几次转换，看最终调用的方法
<pre escaped="true" lang="java">/* choose &lt;i&gt;numOfReplicas&lt;/i&gt; from all data nodes */
  private DatanodeDescriptor chooseTarget(int numOfReplicas,
                                          DatanodeDescriptor writer,
                                          HashMap&lt;Node, Node&gt; excludedNodes,
                                          long blocksize,
                                          int maxNodesPerRack,
                                          List&lt;DatanodeDescriptor&gt; results) {
      
    if (numOfReplicas == 0 &brvbar;&brvbar; clusterMap.getNumOfLeaves()==0) {
      return writer;
    }
    int totalReplicasExpected = numOfReplicas; // 总共需要的副本数
      
// results是当前已分配的节点
    int numOfResults = results.size();
    boolean newBlock = (numOfResults==0);
    if (writer == null && !newBlock) {
      writer = results.get(0);
    }
      
    try {
// 如果还没分配过，先选择本地节点
      if (numOfResults == 0) {
        writer = chooseLocalNode(writer, excludedNodes, 
                                 blocksize, maxNodesPerRack, results);
        if (--numOfReplicas == 0) {
          return writer;
        }
      }
// 如果之前已分配一个或零个，在其他机架的一台机器选择
      if (numOfResults &lt;= 1) {
        chooseRemoteRack(1, results.get(0), excludedNodes, 
                         blocksize, maxNodesPerRack, results);
        if (--numOfReplicas == 0) {
          return writer;
        }
      }
// 如果前面还没分配完，已有小于或等于两个副本
      if (numOfResults &lt;= 2) {
        // 如果前两个在同一个机架上，选择一个其他机架的
        if (clusterMap.isOnSameRack(results.get(0), results.get(1))) {
          chooseRemoteRack(1, results.get(0), excludedNodes,
                           blocksize, maxNodesPerRack, results);
        } else if (newBlock){ 
          chooseLocalRack(results.get(1), excludedNodes, blocksize, 
                          maxNodesPerRack, results);
        } else {
          chooseLocalRack(writer, excludedNodes, blocksize,
                          maxNodesPerRack, results);
        }
        if (--numOfReplicas == 0) {
          return writer;
        }
      }
// 如果还需要副本，就随机选择
      chooseRandom(numOfReplicas, NodeBase.ROOT, excludedNodes, 
                   blocksize, maxNodesPerRack, results);
    } catch (NotEnoughReplicasException e) {
      LOG.warn("Not able to place enough replicas, still in need of "
               + numOfReplicas + " to reach " + totalReplicasExpected + "\n"
               + e.getMessage());
    }
    return writer;
  }</pre>
看一下 chooseLocalNode
<pre escaped="true" lang="java">/* choose &lt;i&gt;localMachine&lt;/i&gt; as the target.
   * if &lt;i&gt;localMachine&lt;/i&gt; is not available, 
   * choose a node on the same rack
   * @return the chosen node
   */
  private DatanodeDescriptor chooseLocalNode(
                                             DatanodeDescriptor localMachine,
                                             HashMap&lt;Node, Node&gt; excludedNodes,
                                             long blocksize,
                                             int maxNodesPerRack,
                                             List&lt;DatanodeDescriptor&gt; results)
    throws NotEnoughReplicasException {
    // if no local machine, randomly choose one node 如果没有本地机器，随机选择一个
    if (localMachine == null)
      return chooseRandom(NodeBase.ROOT, excludedNodes, 
                          blocksize, maxNodesPerRack, results);
    if (preferLocalNode) { // 这个值写死为true
      // otherwise try local machine first
      Node oldNode = excludedNodes.put(localMachine, localMachine); // 把当前节点先加入排除列表
      if (oldNode == null) { // was not in the excluded list 如果返回null表示之前没有在排除列表里
        if (isGoodTarget(localMachine, blocksize,
                         maxNodesPerRack, false, results)) {//判断是否好的目标，后面再看这个方法
          results.add(localMachine);
          return localMachine;
        }
      } 
    }      
    // try a node on local rack
    return chooseLocalRack(localMachine, excludedNodes, 
                           blocksize, maxNodesPerRack, results);// 如果本机不适合，选择同机架的其他机器
  }</pre>
继续看chooseLocalRack
<pre escaped="true" lang="java">/* choose one node from the rack that &lt;i&gt;localMachine&lt;/i&gt; is on.
   * if no such node is available, choose one node from the rack where
   * a second replica is on.
   * if still no such node is available, choose a random node 
   * in the cluster.
   * @return the chosen node
   */
  private DatanodeDescriptor chooseLocalRack(
                                             DatanodeDescriptor localMachine,
                                             HashMap&lt;Node, Node&gt; excludedNodes,
                                             long blocksize,
                                             int maxNodesPerRack,
                                             List&lt;DatanodeDescriptor&gt; results)
    throws NotEnoughReplicasException {
    // no local machine, so choose a random machine
    if (localMachine == null) {
      return chooseRandom(NodeBase.ROOT, excludedNodes, 
                          blocksize, maxNodesPerRack, results);
    }
      
    // choose one from the local rack 选择同一个机架的
    try {
      return chooseRandom(
                          localMachine.getNetworkLocation(),
                          excludedNodes, blocksize, maxNodesPerRack, results);
    } catch (NotEnoughReplicasException e1) {
      // find the second replica 从已有副本里面找同一个机架的
      DatanodeDescriptor newLocal=null;
      for(Iterator&lt;DatanodeDescriptor&gt; iter=results.iterator();
          iter.hasNext();) {
        DatanodeDescriptor nextNode = iter.next();
        if (nextNode != localMachine) {
          newLocal = nextNode;
          break;
        }
      }
      if (newLocal != null) {
        try {
          return chooseRandom(
                              newLocal.getNetworkLocation(),
                              excludedNodes, blocksize, maxNodesPerRack, results);
        } catch(NotEnoughReplicasException e2) {
          //otherwise randomly choose one from the network 如果还是找不到，随机选择
          return chooseRandom(NodeBase.ROOT, excludedNodes,
                              blocksize, maxNodesPerRack, results);
        }
      } else {
        //otherwise randomly choose one from the network
        return chooseRandom(NodeBase.ROOT, excludedNodes,
                            blocksize, maxNodesPerRack, results);
      }
    }
  }</pre>
继续chooseRemoteRack
<pre escaped="true" lang="java">/* choose &lt;i&gt;numOfReplicas&lt;/i&gt; nodes from the racks 
   * that &lt;i&gt;localMachine&lt;/i&gt; is NOT on.
   * if not enough nodes are available, choose the remaining ones 
   * from the local rack
   */
    
  private void chooseRemoteRack(int numOfReplicas,
                                DatanodeDescriptor localMachine,
                                HashMap&lt;Node, Node&gt; excludedNodes,
                                long blocksize,
                                int maxReplicasPerRack,
                                List&lt;DatanodeDescriptor&gt; results)
    throws NotEnoughReplicasException {
    int oldNumOfReplicas = results.size();
    // randomly choose one node from remote racks 选择其他机架的节点，注意这里的"~"是表示排除本机架，如果找不到就只有在本机架找
    try {
      chooseRandom(numOfReplicas, "~"+localMachine.getNetworkLocation(),
                   excludedNodes, blocksize, maxReplicasPerRack, results);
    } catch (NotEnoughReplicasException e) {
      chooseRandom(numOfReplicas-(results.size()-oldNumOfReplicas),
                   localMachine.getNetworkLocation(), excludedNodes, blocksize, 
                   maxReplicasPerRack, results);
    }
  }
</pre>
最后一个 chooseRandom
<pre escaped="true" lang="java">/* Randomly choose &lt;i&gt;numOfReplicas&lt;/i&gt; targets from &lt;i&gt;nodes&lt;/i&gt;.
   */
  private void chooseRandom(int numOfReplicas,
                            String nodes,
                            HashMap&lt;Node, Node&gt; excludedNodes,
                            long blocksize,
                            int maxNodesPerRack,
                            List&lt;DatanodeDescriptor&gt; results)
    throws NotEnoughReplicasException {
      
    int numOfAvailableNodes =
      clusterMap.countNumOfAvailableNodes(nodes, excludedNodes.keySet()); // 当前可用节点数
    StringBuilder builder = null;
    if (LOG.isDebugEnabled()) {
      builder = threadLocalBuilder.get();
      builder.setLength(0);
      builder.append("[");
    }
    boolean badTarget = false;
    while(numOfReplicas &gt; 0 && numOfAvailableNodes &gt; 0) { // 循环直到所有可用副本数为0
      DatanodeDescriptor chosenNode = 
        (DatanodeDescriptor)(clusterMap.chooseRandom(nodes));
      Node oldNode = excludedNodes.put(chosenNode, chosenNode);
      if (oldNode == null) {
        numOfAvailableNodes--;

        if (isGoodTarget(chosenNode, blocksize, maxNodesPerRack, results)) {
          numOfReplicas--;
          results.add(chosenNode);
        } else {
          badTarget = true;
        }
      }
    }
      
    if (numOfReplicas&gt;0) {
      String detail = enableDebugLogging;
      if (LOG.isDebugEnabled()) {
        if (badTarget && builder != null) {
          detail = builder.append("]").toString();
          builder.setLength(0);
        } else detail = "";
      }
      throw new NotEnoughReplicasException(detail);
    }
  }</pre>
最后来看如何判断节点是否可用，isGoodTarget
<pre escaped="true" lang="java">/* judge if a node is a good target.
   * return true if &lt;i&gt;node&lt;/i&gt; has enough space, 
   * does not have too much load, and the rack does not have too many nodes
   */
  private boolean isGoodTarget(DatanodeDescriptor node,
                               long blockSize, int maxTargetPerLoc,
                               List&lt;DatanodeDescriptor&gt; results) {
    return isGoodTarget(node, blockSize, maxTargetPerLoc,
                        this.considerLoad, results);
  }
    
  private boolean isGoodTarget(DatanodeDescriptor node,
                               long blockSize, int maxTargetPerLoc,
                               boolean considerLoad,
                               List&lt;DatanodeDescriptor&gt; results) {
    // check if the node is (being) decommissed 判断是否退役了
    if (node.isDecommissionInProgress() &brvbar;&brvbar; node.isDecommissioned()) {
      if(LOG.isDebugEnabled()) {
        threadLocalBuilder.get().append(node.toString()).append(": ")
          .append("Node ").append(NodeBase.getPath(node))
          .append(" is not chosen because the node is (being) decommissioned ");
      }
      return false;
    }

    long remaining = node.getRemaining() - 
                     (node.getBlocksScheduled() * blockSize); 
    // check the remaining capacity of the target machine 判断剩余的磁盘空间， 块大小 * 5 > 剩余大小 表示不可用
    if (blockSize* HdfsConstants.MIN_BLOCKS_FOR_WRITE&gt;remaining) {
      if(LOG.isDebugEnabled()) {
        threadLocalBuilder.get().append(node.toString()).append(": ")
          .append("Node ").append(NodeBase.getPath(node))
          .append(" is not chosen because the node does not have enough space ");
      }
      return false;
    }
      
    // check the communication traffic of the target machine 判断各个datanode的负载情况，这里的负载不是系统负载，而是根据xceiver线程数，这个线程好像是负责读写的。
    if (considerLoad) { // 默认这个为true，配置项 dfs.namenode.replication.considerLoad
      double avgLoad = 0;
      int size = clusterMap.getNumOfLeaves(); // 所有datanode数
      if (size != 0 && stats != null) {
        avgLoad = (double)stats.getTotalLoad()/size; // 获取总的xceiver线程数除以所有datanode数，算出平均负载
      }
      if (node.getXceiverCount() &gt; (2.0 * avgLoad)) { // 如果当前线程数 大于 平均值的两倍，则不可使用
        if(LOG.isDebugEnabled()) {
          threadLocalBuilder.get().append(node.toString()).append(": ")
            .append("Node ").append(NodeBase.getPath(node))
            .append(" is not chosen because the node is too busy ");
        }
        return false;
      }
    }
      
    // check if the target rack has chosen too many nodes 检查是否有太多节点在当前机架上
    String rackname = node.getNetworkLocation();
    int counter=1;
    for(Iterator&lt;DatanodeDescriptor&gt; iter = results.iterator();
        iter.hasNext();) {
      Node result = iter.next();
      if (rackname.equals(result.getNetworkLocation())) {
        counter++;
      }
    }

//maxNodesPerRack的算法，没看懂，可能是每个机架的平均数+2，不知道为什么定一个这样的值 int maxNodesPerRack = (totalNumOfReplicas-1)/clusterMap.getNumOfRacks()+2;

    if (counter&gt;maxTargetPerLoc) {
      if(LOG.isDebugEnabled()) {
        threadLocalBuilder.get().append(node.toString()).append(": ")
          .append("Node ").append(NodeBase.getPath(node))
          .append(" is not chosen because the rack has too many chosen nodes ");
      }
      return false;
    }
    return true;
  }</pre>
我们当前集群状态，总共11台datanode，没有退役机器。其中7台机器磁盘已满或者基本满，剩下4台机器可写。没有划分机架，所以整个集群认为只有一个机架。所以应该不会触发“同一个机架不能有太多个节点的问题”（具体原因看上面代码，这里表述可能不是很准确）
**怀疑检查负载的逻辑，7台满的机器datanode负载可能很低，但因为磁盘满不可以使用，导致剩下的4台机器线程数超过平均值的两倍。**  
当前只能加入日志，等下次出错后检查。