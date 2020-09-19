---
title: knative分析 – controller
author: fatkun
type: post
date: 2018-08-06T12:06:37+00:00
url: /2018/08/knative-controller.html
categories:
  - docker
tags:
  - k8s
  - knative

---
由于service名称重复，这里会用knative service 和 k8s service区分两者。
# 总体流程 {#总体流程}

用户创建knative service后，会创建出route和configuration。  
然后根据configuration创建revision，根据revision创建deployment启动业务pod。  
根据route创建k8s service和istio VirtualService，负责流量如何转发。
<div data-type="image" data-src="https://github.com/knative/serving/raw/master/docs/spec/images/object_model.png">  <img src="https://github.com/knative/serving/raw/master/docs/spec/images/object_model.png" /></div>
# controller代码分析 {#controller代码分析}

## knative service controller {#knative-service-controller}

监听（knative service，configuration，route）
  * 如果没有Configuration，则会创建一个。如果已存在，会比较然后判断是否需要更新。
  * 如果没有Route，则会创建一个，如果已存在，比较判断是否需要更新。
## Configuration controller {#configuration-controller}

监听（configuration, revision）
  * 检查是否创建了Revision(Revision名字由 config.Name 和 config.Spec.Generation构成)，如果没有创建则创建一个。 
      * 如果有config.Spec.Build，会同时创建Build和Revision
      * 如果存在，则更新状态
## Revision controller {#revision-controller}

监听(revision，build，endpoint, deployment, configMap)
  * 如果需要build，检查build的状态
  * 如果没有build或者build完成后 
      * reconcileDeployment, 判断rev.Spec.ServingState状态 
          * v1alpha1.RevisionServingStateActive, v1alpha1.RevisionServingStateReserve 活跃或保留状态 
              * 如果不存在，创建deployment（如果是Reserve状态，把副本设为0）
              * 如果存在，检查更新deployment
          * v1alpha1.RevisionServingStateRetired 退休状态 
              * 如果存在，删除deployment
      * reconcileService， 创建或更新k8s service(名称例子：autoscale-go-00000-service)
      * reconcileFluentdConfigMap，配置fluentd的configmap
      * reconcileAutoscalerDeployment，创建或更新Autoscaler 的deployment
      * reconcileAutoscalerService，创建Autoscaler的k8s service
      * reconcileVPA，创建或删除VPA
## Route controller {#route-controller}

监听（route，Configuration）
  * reconcilePlaceholderService, 创建同名的k8s service或更新k8s service的ClusterIP
  * configureTraffic，尝试根据RouteSpec分配流量，如果找不到目标（例如没有ready状态的Revision，或者状态是Revision）,则不会分配流量。如果流量分配配置好了，会把RouteStatus更新为AllTrafficAssigned = True, 否则设为 False，并在原因里面写明缺少的目标。 
      * 如果TrafficTarget.RevisionName不为空，判断target是否ready了 
          * 如果target ready了，创建或更新Istio VirtualService 
              * 判断target是否active，如果POD还没启动，会添加部分流量到activator里
      * 如果TrafficTarget.ConfigurationName不为空，则会从conf里面拿到LatestReadyRevisionName，然后按RevisionName不为空的流程配置
&nbsp;
<pre># istio VirtualService 例子
spec:
  gateways:
  - knative-shared-gateway.knative-serving.svc.cluster.local
  - mesh
  hosts:
  - '*.helloworld-python.default.example.com'
  - helloworld-python.default.example.com
  - helloworld-python.default.svc.cluster.local
  http:
  - appendHeaders:
      Knative-Serving-Namespace: default
      Knative-Serving-Revision: helloworld-python-00000
      x-envoy-upstream-rq-timeout-ms: "0"
    match:
    - authority:
        exact: helloworld-python.default.example.com
    - authority:
        exact: helloworld-python.default.svc.cluster.local
    route:
    - destination:
        host: activator-service.knative-serving.svc.cluster.local
        port:
          number: 80
      weight: 100
    timeout: 60s</pre>