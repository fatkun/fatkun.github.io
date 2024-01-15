---
title: "Nacos配置服务源码分析"
date: 2024-01-15T20:05:39+08:00
tags: []
categories: []
author: "fatkun"
draft: false
---

# 概要

分析的版本为nacos 2.3.0，nacos 2.x版本使用grpc通信，先看主要的proto文件

# GRPC通信

## 获取配置

先从代码入口入手，nacos源码中有一个Example（com.alibaba.nacos.example.ConfigExample）

```java
String serverAddr = "localhost";
String dataId = "test";
String group = "DEFAULT_GROUP";
Properties properties = new Properties();
properties.put("serverAddr", serverAddr);
// 创建一个NacosConfigService
ConfigService configService = NacosFactory.createConfigService(properties);
// 获取配置
String content = configService.getConfig(dataId, group, 5000);
System.out.println("[config content] " + content);
// 注册回调
configService.addListener(dataId, group, new Listener() {
    @Override
    public void receiveConfigInfo(String configInfo) {
        System.out.println("receive:" + configInfo);
    }

    @Override
    public Executor getExecutor() {
        return null;
    }
});
```



进入getConfig方法，看看是如何获取配置的

```java
private String getConfigInner(String tenant, String dataId, String group, long timeoutMs) throws NacosException {
	// ...
	// 从本地获取配置，这个是用于灾备场景的
	String content = LocalConfigInfoProcessor.getFailover(worker.getAgentName(), dataId, group, tenant);
	// ...
  // 从服务端获取配置
  ConfigResponse response = worker.getServerConfig(dataId, group, tenant, timeoutMs, false);
  cr.setContent(response.getContent());
  
}
```



调用的是ClientWorker.getServerConfig() -> ConfigRpcTransportClient.queryConfig()

```java
public ConfigResponse queryConfig(String dataId, String group, String tenant, long readTimeouts, boolean notify) throws NacosException {
  					// 创建一个ConfigQueryRequest的请求
            ConfigQueryRequest request = ConfigQueryRequest.build(dataId, group, tenant);
            request.putHeader(NOTIFY_HEADER, String.valueOf(notify));
            RpcClient rpcClient = getOneRunningClient();
            ...
            // 向服务端请求
            ConfigQueryResponse response = (ConfigQueryResponse) requestProxy(rpcClient, request, readTimeouts);
            
            ConfigResponse configResponse = new ConfigResponse();
            if (response.isSuccess()) {
                // 写成文件
                LocalConfigInfoProcessor.saveSnapshot(this.getName(), dataId, group, tenant, response.getContent());
                
                configResponse.setContent(response.getContent());
                ...
        }
```



跟踪代码，ConfigRpcTransportClient.requestProxy() -> rpcClientInner.request() -> GrpcConnection#request()

```java
    public Response request(Request request, long timeouts) throws NacosException {
      // 序列化请求
        Payload grpcRequest = GrpcUtils.convert(request);
      // 调用PB方法
        ListenableFuture<Payload> requestFuture = grpcFutureServiceStub.request(grpcRequest);
        Payload grpcResponse;
        try {
            if (timeouts <= 0) {
                grpcResponse = requestFuture.get();
            } else {
                grpcResponse = requestFuture.get(timeouts, TimeUnit.MILLISECONDS);
            }
        } catch (Exception e) {
            throw new NacosException(NacosException.SERVER_ERROR, e);
        }
        
      // 反序列化结果
        return (Response) GrpcUtils.parse(grpcResponse);
    }
```



这里涉及到grpc的调用，从proto文件（src/main/proto/nacos_grpc_service.proto）看，主要有两个接口

```protobuf
message Payload {
  Metadata metadata = 2;
  google.protobuf.Any body = 3; // 主要的Request对象序列化成这个
}

service Request {
  // 注册、获取配置
  rpc request (Payload) returns (Payload) {
  }
}

service BiRequestStream {
  // stream接口，双向通信，用于接收服务端推送的更新
  rpc requestBiStream (stream Payload) returns (stream Payload) {
  }
}
```



客户端的请求是ConfigQueryRequest，对应服务端的代码在com.alibaba.nacos.config.server.remote.ConfigQueryRequestHandler

// 待填充

// 服务端这里主要是从磁盘里(直接文件获取或者通过rocksDB)获取内容



## 监听配置

监听采用的回调的思想，当服务端通知的时候，调用回调方法。

```java
public void addListener(String dataId, String group, Listener listener) throws NacosException {
    worker.addTenantListeners(dataId, group, Collections.singletonList(listener));
}

public void addTenantListeners(String dataId, String group, List<? extends Listener> listeners) throws NacosException {
    group = blank2defaultGroup(group);
    String tenant = agent.getTenant();
    // 增加一个CacheData，会存放在ClientWorker.cacheMap里面
    CacheData cache = addCacheDataIfAbsent(dataId, group, tenant);
    synchronized (cache) {
        for (Listener listener : listeners) {
            // 加入到CopyOnWriteArrayList<ManagerListenerWrap> listeners里面
            cache.addListener(listener);
        }
        cache.setDiscard(false);
        cache.setConsistentWithServer(false);
        // 通知
        agent.notifyListenConfig();
    }
}

private final BlockingQueue<Object> listenExecutebell = new ArrayBlockingQueue<>(1);
public void notifyListenConfig() {
    // 放入一个BlockingQueue里面，有一个线程消费这个queue，执行executeConfigListen方法
    listenExecutebell.offer(bellItem);
}

public void startInternal() {
    executor.schedule(() -> {
        while (!executor.isShutdown() && !executor.isTerminated()) {
            try {
                listenExecutebell.poll(5L, TimeUnit.SECONDS);
                // 省略一部分代码...
                executeConfigListen();
            } catch (Throwable e) {
                // 省略一部分代码...
                notifyListenConfig();
            }
        }
    }, 0L, TimeUnit.MILLISECONDS);

}

public void executeConfigListen() {
  // 省略一部分代码...
  for (CacheData cache : cacheMap.get().values()) {
    // consistentWithServer 在新加入进来时是false，在收到服务端一致时才是true
    if (cache.isConsistentWithServer()) {
        cache.checkListenerMd5();
        if (!needAllSync) {
            continue;
        }
    }
    // 省略一部分代码...
    // 检查数据有没有变化
    boolean hasChangedKeys = checkListenCache(listenCachesMap);
    
  }
  // 省略一部分代码...
}
```

和服务端对比MD5，检查配置是否有变更

```java
private boolean checkListenCache(Map<String, List<CacheData>> listenCachesMap) {
	//...
  for (Map.Entry<String, List<CacheData>> entry : listenCachesMap.entrySet()) {
    // 按照taskId多线程执行
    ...
    // 发起RPC请求，批量检查配置是否有变更
    ConfigBatchListenRequest configChangeListenRequest = buildConfigRequest(listenCaches);
    RpcClient rpcClient = ensureRpcClient(taskId);
    ConfigChangeBatchListenResponse listenResponse = (ConfigChangeBatchListenResponse) requestProxy(rpcClient, configChangeListenRequest);
    
    List<ConfigChangeBatchListenResponse.ConfigContext> changedConfigs = listenResponse.getChangedConfigs();
    //handle changed keys,notify listener
    if (!CollectionUtils.isEmpty(changedConfigs)) {
        hasChangedKeys.set(true);
        for (ConfigChangeBatchListenResponse.ConfigContext changeConfig : changedConfigs) {
            String changeKey = GroupKey.getKeyTenant(changeConfig.getDataId(),
                    changeConfig.getGroup(), changeConfig.getTenant());
            changeKeys.add(changeKey);
            boolean isInitializing = cacheMap.get().get(changeKey).isInitializing();
            // 获取数据，并且执行用户回调
            refreshContentAndCheck(changeKey, !isInitializing);
        }
    }
  }
  //...
}
```

从服务端获取配置，回调用户方法

```java
private void refreshContentAndCheck(CacheData cacheData, boolean notify) {
    try {
				// 从服务端获取配置
        ConfigResponse response = getServerConfig(cacheData.dataId, cacheData.group, cacheData.tenant, 3000L, notify);
        cacheData.setEncryptedDataKey(response.getEncryptedDataKey());
        cacheData.setContent(response.getContent());
        if (null != response.getConfigType()) {
            cacheData.setType(response.getConfigType());
        }
        // ...
        // 和listener最后执行的md5比较，如果不一样就调用用户注册的回调方法
        cacheData.checkListenerMd5();
    } catch (Exception e) {
        // ...
    }
}
```



## 配置变更推送

再回来看看服务端怎么处理ConfigBatchListenRequest请求，服务端代码在ConfigChangeBatchListenRequestHandler

```java
public ConfigChangeBatchListenResponse handle(ConfigBatchListenRequest configChangeListenRequest, RequestMeta meta)
            throws NacosException {
    for (ConfigBatchListenRequest.ConfigListenContext listenContext : configChangeListenRequest.getConfigListenContexts()) {
      
      if (configChangeListenRequest.isListen()) {
          // 加入监听列表
          configChangeListenContext.addListen(groupKey, md5, connectionId);
          boolean isUptoDate = ConfigCacheService.isUptodate(groupKey, md5, meta.getClientIp(), tag);
          if (!isUptoDate) {
            configChangeBatchListenResponse.addChangeConfig(listenContext.getDataId(), listenContext.getGroup(), listenContext.getTenant());
          }
      } else {
          // 从监听列表移除
          configChangeListenContext.removeListen(groupKey, connectionId);
      }             
    }

}
```



加入监控列表

```java
// com.alibaba.nacos.config.server.remote.ConfigChangeListenContext#addListen
// 维护一个 {connectionId:{groupKey:md5}} 的关系
private ConcurrentHashMap<String, HashMap<String, String>> connectionIdContext = new ConcurrentHashMap<>();

// 维护 groupKey-> connection 关系
private ConcurrentHashMap<String, HashSet<String>> groupKeyContext = new ConcurrentHashMap<>();

public synchronized void addListen(String groupKey, String md5, String connectionId) {
  //...
}
```

RpcConfigChangeNotifier 是负责推送配置的类，在接收到LocalDataChangeEvent变更之后，触发推送

```java
public void configDataChanged(String groupKey, String dataId, String group, String tenant, boolean isBeta,
            List<String> betaIps, String tag) {
        // 获取所有和这个groupKey相关的连接
        Set<String> listeners = configChangeListenContext.getListeners(groupKey);
        if (CollectionUtils.isEmpty(listeners)) {
            return;
        }
        int notifyClientCount = 0;
        for (final String client : listeners) {
            Connection connection = connectionManager.getConnection(client);
            if (connection == null) {
                continue;
            }
            
            ConnectionMeta metaInfo = connection.getMetaInfo();
            String clientIp = metaInfo.getClientIp();
            String clientTag = metaInfo.getTag();
            
            //tag check
            if (StringUtils.isNotBlank(tag) && !tag.equals(clientTag)) {
                continue;
            }
            
            ConfigChangeNotifyRequest notifyRequest = ConfigChangeNotifyRequest.build(dataId, group, tenant);
            // 构造RPC推送
            RpcPushTask rpcPushRetryTask = new RpcPushTask(notifyRequest,
                    ConfigCommonConfig.getInstance().getMaxPushRetryTimes(), client, clientIp, metaInfo.getAppName());
            push(rpcPushRetryTask, connectionManager);
            notifyClientCount++;
        }
        Loggers.REMOTE_PUSH.info("push [{}] clients, groupKey=[{}]", notifyClientCount, groupKey);
    }
```

这里的grpc推送，从RpcPushTask跟进去，调用rpcPushService.pushWithCallback，GrpcConnection#sendRequestNoAck方法里面通过streamObserver来发送。

这个streamObserver是在com.alibaba.nacos.core.remote.grpc.GrpcBiStreamRequestAcceptor#requestBiStream调用时，前面看到的grpc方法，客户端在建立双向流后，使用streamObserver给客户端推送请求。





# 参考文章

[Nacos源码分析](https://juejin.cn/column/7207620183308255292)

