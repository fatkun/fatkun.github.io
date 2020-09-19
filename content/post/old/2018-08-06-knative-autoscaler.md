---
title: knative分析 – autoscaler
author: fatkun
type: post
date: 2018-08-06T12:00:42+00:00
url: /2018/08/knative-autoscaler.html
wp-syntax-cache-content:
  - |
    a:3:{i:1;s:3431:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="other" style="font-family:monospace;">   +---------------------+
       | ROUTE               |
       |                     |
       |   +-------------+   |
       |   | Istio Route |---------------+
       |   +-------------+   |           |
       |         |           |           |
       +---------|-----------+           |
                 |                       |
                 |                       |
                 | inactive              | active
                 |  route                | route
                 |                       |
                 |                       |
                 |                +------|------------------------------------+
                 V         watch  |      V                                    |
           +-----------+   first  |   +- ----+  create   +------------+       |
           | Activator |-------------&gt;| Pods |&lt;----------| Deployment |       |
           +-----------+          |   +------+           +------------+       |
                 |                |       |                     ^             |
                 |   activate     |       |                     | resize      |
                 +---------------&gt;|       |                     |             |
                                  |       |    metrics    +---------------+   |
                                  |       +--------------&gt;| Single-tenant |   |
                                  |                       |  Autoscaler   |   |
                                  |                       +---------------+   |
                                  | REVISION                                  |
                                  +-------------------------------------------+</pre></td></tr></table><p class="theCode" style="display:none;">   +---------------------+
       | ROUTE               |
       |                     |
       |   +-------------+   |
       |   | Istio Route |---------------+
       |   +-------------+   |           |
       |         |           |           |
       +---------|-----------+           |
                 |                       |
                 |                       |
                 | inactive              | active
                 |  route                | route
                 |                       |
                 |                       |
                 |                +------|------------------------------------+
                 V         watch  |      V                                    |
           +-----------+   first  |   +- ----+  create   +------------+       |
           | Activator |-------------&gt;| Pods |&lt;----------| Deployment |       |
           +-----------+          |   +------+           +------------+       |
                 |                |       |                     ^             |
                 |   activate     |       |                     | resize      |
                 +---------------&gt;|       |                     |             |
                                  |       |    metrics    +---------------+   |
                                  |       +--------------&gt;| Single-tenant |   |
                                  |                       |  Autoscaler   |   |
                                  |                       +---------------+   |
                                  | REVISION                                  |
                                  +-------------------------------------------+</p></div>
    ";i:2;s:813:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="other" style="font-family:monospace;">const (
       // 每个pod实例同时只处理一个请求
       RevisionRequestConcurrencyModelSingle RevisionRequestConcurrencyModelType = &quot;Single&quot;
       // 每个pod实例同时处理多个请求
       RevisionRequestConcurrencyModelMulti RevisionRequestConcurrencyModelType = &quot;Multi&quot;
    )</pre></td></tr></table><p class="theCode" style="display:none;">const (
       // 每个pod实例同时只处理一个请求
       RevisionRequestConcurrencyModelSingle RevisionRequestConcurrencyModelType = &quot;Single&quot;
       // 每个pod实例同时处理多个请求
       RevisionRequestConcurrencyModelMulti RevisionRequestConcurrencyModelType = &quot;Multi&quot;
    )</p></div>
    ";i:3;s:3773:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="other" style="font-family:monospace;">apiVersion: v1
    kind: ConfigMap
    metadata:
      name: config-autoscaler
      namespace: knative-serving
    data:
      # Static parameters:
    &nbsp;
      # 期望每个pod并发请求数
      multi-concurrency-target: &quot;1.0&quot;
      # 如果是单个并发，值要接近1.0
      single-concurrency-target: &quot;0.9&quot;
    &nbsp;
      # stable窗口时间，计算平均并发会用到。如果进入panic模式后，经过stable窗口时间也会恢复stable
      stable-window: &quot;60s&quot;
    &nbsp;
      # 如果平均并发在panic窗口时间内达到2倍目标并发，autoscaler进入panic模式。
      # 在panic模式下，自动伸缩按在panic窗口时间的平均并发来操作。
      panic-window: &quot;6s&quot;
    &nbsp;
      # 最大增长比例，每次调整会根据并发计算增长比例，最大增长不超过这个值
      max-scale-up-rate: &quot;10&quot;
    &nbsp;
      # 计算并发值的参数，每一段时间得到最大并发，作为一个bucket，最后汇报的时候，
      # 平均并发 = 各个bucket最大并发之和 / 总bucket数，汇报间隔是1秒（hard coded）
      concurrency-quantum-of-time: &quot;100ms&quot;
    &nbsp;
      # 是否开启缩容到0
      enable-scale-to-zero: &quot;true&quot;
    &nbsp;
      # 实验性：开启垂直扩容
      # Requires a VPA installation (e.g. ./third_party/vpa/install-vpa.sh)
      enable-vertical-pod-autoscaling: &quot;false&quot;
    &nbsp;
      # 如果开启了enable-vertical-pod-autoscaling，这个值就会替代multi-concurrency-target，
      # 如果成熟了后期会变成默认值
      vpa-multi-concurrency-target: &quot;10.0&quot;
    &nbsp;
      # 多长时间调整一次
      tick-interval: &quot;2s&quot;
    &nbsp;
      # Dynamic parameters (take effect when config map is updated):
    &nbsp;
      # 空闲多长时间缩容到0
      scale-to-zero-threshold: &quot;5m&quot;</pre></td></tr></table><p class="theCode" style="display:none;">apiVersion: v1
    kind: ConfigMap
    metadata:
      name: config-autoscaler
      namespace: knative-serving
    data:
      # Static parameters:
    
      # 期望每个pod并发请求数
      multi-concurrency-target: &quot;1.0&quot;
      # 如果是单个并发，值要接近1.0
      single-concurrency-target: &quot;0.9&quot;
    
      # stable窗口时间，计算平均并发会用到。如果进入panic模式后，经过stable窗口时间也会恢复stable
      stable-window: &quot;60s&quot;
    
      # 如果平均并发在panic窗口时间内达到2倍目标并发，autoscaler进入panic模式。
      # 在panic模式下，自动伸缩按在panic窗口时间的平均并发来操作。
      panic-window: &quot;6s&quot;
    
      # 最大增长比例，每次调整会根据并发计算增长比例，最大增长不超过这个值
      max-scale-up-rate: &quot;10&quot;
    
      # 计算并发值的参数，每一段时间得到最大并发，作为一个bucket，最后汇报的时候，
      # 平均并发 = 各个bucket最大并发之和 / 总bucket数，汇报间隔是1秒（hard coded）
      concurrency-quantum-of-time: &quot;100ms&quot;
    
      # 是否开启缩容到0
      enable-scale-to-zero: &quot;true&quot;
    
      # 实验性：开启垂直扩容
      # Requires a VPA installation (e.g. ./third_party/vpa/install-vpa.sh)
      enable-vertical-pod-autoscaling: &quot;false&quot;
     
      # 如果开启了enable-vertical-pod-autoscaling，这个值就会替代multi-concurrency-target，
      # 如果成熟了后期会变成默认值
      vpa-multi-concurrency-target: &quot;10.0&quot;
    
      # 多长时间调整一次
      tick-interval: &quot;2s&quot;
      
      # Dynamic parameters (take effect when config map is updated):
    
      # 空闲多长时间缩容到0
      scale-to-zero-threshold: &quot;5m&quot;</p></div>
    ";}
categories:
  - docker
tags:
  - k8s
  - knative

---
<div data-type="p">  文档说目前的实现只是为了快速实现，后期还会修改。</div>
<div data-type="p"></div>
<h2 id="pistun" data-type="h">  knative是如何做伸缩容的？</h2>
<p data-type="p">  处理伸缩容问题，首先要解决的问题是根据什么指标判断伸缩容？cpu、内存、请求数？这里knative使用的是请求数。</p>
<p data-type="p">  其次是伸缩多少的问题。</p>
<p data-type="p">  knative的伸缩是依赖修改deployment的replicate数实现的。</p>
<div data-type="p"></div>
## 如何采集请求数？

<p data-type="p">  启动revision的pod时，也会启动一个autoscaler（一个knative revision只启动一个autoscaler），autoscaler自己本身也会scale到0，用于接收请求数统计和处理伸缩容。</p>
<p data-type="p">  业务pod中，会注入queue-proxy sidecard，用于接收请求，在这里会统计并发数，每秒向autoscaler汇报，接收到的请求会转发给业务container。</p>
<p data-type="p">  注：单租户模式下一个revision启动一个autoscaler，多租户共用一个autoscaler</p>
<div data-type="p"></div>
<h2 id="5nvoev" data-type="h">  计算需要pod的个数？</h2>
<p data-type="p">  autoscaler接收到并发统计的时候，会根据算法计算需要的pod个数。</p>
<p data-type="p">  算法中有两种模式，分别是panic和stable模式，一个是短时间，一个是长时间，为了解决短时间内请求突增的场景，需要快速扩容。</p>
<p data-type="p">  <a class="bi-link" href="https://github.com/knative/docs/blob/master/serving/samples/autoscale-go/README.md#algorithm" target="_blank" rel="noopener">文档中描述</a><span data-type="ranges">的算法是，默认的target concurency是1，如果一个revision 35QPS，每个请求花费0.25秒，Knative Serving 觉得需要 9 个 pod。 </span></p>
    ceil(35 * .25) = ceil(8.75) = 9
    
<div data-type="p"></div>
<h4 id="xsewfu" data-type="h">  Stable Mode（稳定模式）</h4>
<p data-type="p">  <span data-type="ranges">在稳定模式下，Autoscaler 根据每个pod期望的并发来调整Deployment的副本个数。根据每个pod在60秒窗口内的平均并发来计算，而不是根据现有副本个数计算，因为pod的数量增加和pod变为可服务和提供指标数据有一定时间间隔。</span></p>
<div data-type="p"></div>
<h4 id="gysqiy" data-type="h">  Panic Mode （恐慌模式）</h4>
<p data-type="p">  <span data-type="ranges">Panic时间窗口默认是6秒，如果在6秒内达到2倍期望的并发，则转换到恐慌模式下。在恐慌模式下，Autoscaler根据这6秒的时间窗口计算，这样更能及时的响应突发的流量请求。每2秒调整Deployment的副本数达到想要的pod个数（或者最大10倍当前pod的数量），为了避免pod数量频繁变动，在恐慌模式下只能增加，不会减少。60秒后会恢复回稳定模式。</span></p>
<div data-type="p"></div>
<h1 id="6dz5gx" data-type="h">  <span data-type="ranges">autoscaler 单租户图</span></h1>
<pre lang="other" escaped="true">+---------------------+
   | ROUTE               |
   |                     |
   |   +-------------+   |
   |   | Istio Route |---------------+
   |   +-------------+   |           |
   |         |           |           |
   +---------|-----------+           |
             |                       |
             |                       |
             | inactive              | active
             |  route                | route
             |                       |
             |                       |
             |                +------|------------------------------------+
             V         watch  |      V                                    |
       +-----------+   first  |   +- ----+  create   +------------+       |
       | Activator |-------------&gt;| Pods |&lt;----------| Deployment |       |
       +-----------+          |   +------+           +------------+       |
             |                |       |                     ^             |
             |   activate     |       |                     | resize      |
             +---------------&gt;|       |                     |             |
                              |       |    metrics    +---------------+   |
                              |       +--------------&gt;| Single-tenant |   |
                              |                       |  Autoscaler   |   |
                              |                       +---------------+   |
                              | REVISION                                  |
                              +-------------------------------------------+</pre>
<h1 id="dq5srw" data-type="h">  模式</h1>
<pre lang="other" escaped="true">const (
   // 每个pod实例同时只处理一个请求
   RevisionRequestConcurrencyModelSingle RevisionRequestConcurrencyModelType = "Single"
   // 每个pod实例同时处理多个请求
   RevisionRequestConcurrencyModelMulti RevisionRequestConcurrencyModelType = "Multi"
)</pre>
<h1 id="grc3yo" data-type="h">  配置</h1>
<div data-type="p">  <pre lang="other" escaped="true">apiVersion: v1
kind: ConfigMap
metadata:
  name: config-autoscaler
  namespace: knative-serving
data:
  # Static parameters:

  # 期望每个pod并发请求数
  multi-concurrency-target: "1.0"
  # 如果是单个并发，值要接近1.0
  single-concurrency-target: "0.9"

  # stable窗口时间，计算平均并发会用到。如果进入panic模式后，经过stable窗口时间也会恢复stable
  stable-window: "60s"

  # 如果平均并发在panic窗口时间内达到2倍目标并发，autoscaler进入panic模式。
  # 在panic模式下，自动伸缩按在panic窗口时间的平均并发来操作。
  panic-window: "6s"

  # 最大增长比例，每次调整会根据并发计算增长比例，最大增长不超过这个值
  max-scale-up-rate: "10"

  # 计算并发值的参数，每一段时间得到最大并发，作为一个bucket，最后汇报的时候，
  # 平均并发 = 各个bucket最大并发之和 / 总bucket数，汇报间隔是1秒（hard coded）
  concurrency-quantum-of-time: "100ms"

  # 是否开启缩容到0
  enable-scale-to-zero: "true"

  # 实验性：开启垂直扩容
  # Requires a VPA installation (e.g. ./third_party/vpa/install-vpa.sh)
  enable-vertical-pod-autoscaling: "false"
 
  # 如果开启了enable-vertical-pod-autoscaling，这个值就会替代multi-concurrency-target，
  # 如果成熟了后期会变成默认值
  vpa-multi-concurrency-target: "10.0"

  # 多长时间调整一次
  tick-interval: "2s"
  
  # Dynamic parameters (take effect when config map is updated):

  # 空闲多长时间缩容到0
  scale-to-zero-threshold: "5m"</pre></div>
<h1 id="nbe3dr" data-type="h">  参考</h1>
<div data-type="p">  <a class="bi-link" href="https://github.com/knative/serving/blob/master/docs/scaling/DEVELOPMENT.md" target="_blank" rel="noopener">https://github.com/knative/serving/blob/master/docs/scaling/DEVELOPMENT.md</a> Autoscaling</div>