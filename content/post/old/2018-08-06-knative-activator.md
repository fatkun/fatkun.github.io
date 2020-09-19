---
title: knative分析 – activator
author: fatkun
type: post
date: 2018-08-06T12:04:51+00:00
url: /2018/08/knative-activator.html
categories:
  - docker
tags:
  - k8s
  - knative

---
<h1 id="qxxgwm" data-type="h">  当scale到0时，是怎样唤醒业务容器的？</h1>
<p data-type="p">  activator就是负责做这个事情的组件。activator做两件事情，一个是负责把pod启动起来，另外一个是把启动中的请求转发给pod。</p>
<p data-type="p">  <p data-type="p">    请求是怎么转发到activator的？  </p>
  <p data-type="p">    当业务pod scale到0的时候，会更新istio VirtualServer，把流量按权重分配给activator。在pod启动ready之后，流量权重又直接指向业务pod，所有revision都ready的情况下，activator不会分配到流量。  </p>
  <p data-type="p">    <p data-type="p">      唤醒pod是通过更新 revision.Spec.ServingState = v1alpha1.RevisionServingStateActive 状态实现的，controller会根据状态，创建出业务pod和autoscaler。    </p>
    <p data-type="p">      这里要解决的一个问题是在pod没启动之前，可能会有很多个请求，这里做了限制每个revision只会触发一次。    </p>
    <p data-type="p">      还有个问题是在pod没ready前，把请求阻塞。    </p>
    <p data-type="p">      activator本身是个HTTP服务，在POD启动的期间，当pod ready之后，会把请求转发到到pod里（通过FQDN域名）    </p>
    <div data-type="p">    </div>
    <div data-type="p">    </div>
    <div data-type="p">    </div>
    <h1 id="1b60dl" data-type="h">      流量转发    </h1>
    <div data-type="p">    </div>
    <div data-type="p">      以下内容主要来自：<a class="bi-link" href="https://github.com/knative/serving/blob/master/pkg/activator/README.md" target="_blank" rel="noopener">https://github.com/knative/serving/blob/master/pkg/activator/README.md</a>    </div>
    <div data-type="p">    </div>
    <div data-type="p">      这个图感觉没更新，目前没有看到有用ingress来路由，而是由istio ingress gateway来路由。    </div>
    <div data-type="p">    </div>
    <div data-type="p">      <div data-type="image" data-display="block" data-align="left" data-src="https://cdn.nlark.com/lark/0/2018/png/2023/1533027397839-996997db-e966-4428-a41a-e9dbe232f825.png" data-width="782">        <img src="https://cdn.nlark.com/lark/0/2018/png/2023/1533027397839-996997db-e966-4428-a41a-e9dbe232f825.png" width="782" />      </div>    </div>
    <div data-type="p">    </div>
    <h2 id="q03mkb" data-type="h">      Istio Route Rules Configurations    </h2>
    <div data-type="p">      <span data-type="ranges">Knative Serving 使用istio route rules来控制流量（根据Route对象指定的比例分配），如果某个revision因为不活跃变为Reserve状态，会把部分流量转向activator。</span>    </div>
    <div data-type="p">      下面分三种情况    </div>
    <h3 id="ifipty" data-type="h">      All revisions are active    </h3>
    <div data-type="p">      <span data-type="ranges">如果所有revision都是活跃的，activator 不会收到任何流量。</span>    </div>
    <div data-type="p">    </div>
    <div data-type="p">      <div data-type="image" data-display="block" data-align="left" data-src="https://cdn.nlark.com/lark/0/2018/png/2023/1533030224312-c79a3bec-15a4-4d04-bceb-29fa13019e95.png" data-width="528">        <img src="https://cdn.nlark.com/lark/0/2018/png/2023/1533030224312-c79a3bec-15a4-4d04-bceb-29fa13019e95.png" width="528" />      </div>    </div>
    <h3 id="18kegg" data-type="h">      One revision is in Reserve state    </h3>
    <div data-type="p">      如果一个revision是Reserve状态，则会把原本给revision b的流量转发给activator，activator收到请求后，会启动revision b，revision b ready后会把流量导入revision b。后续的流量直接到revision b。    </div>
    <div data-type="p">    </div>
    <div data-type="p">      <div data-type="image" data-display="block" data-align="left" data-src="https://cdn.nlark.com/lark/0/2018/png/2023/1533030284503-bf5220e4-1ce4-47ab-8c81-5bac26f9f3d8.png" data-width="697">        <img src="https://cdn.nlark.com/lark/0/2018/png/2023/1533030284503-bf5220e4-1ce4-47ab-8c81-5bac26f9f3d8.png" width="697" />      </div>    </div>
    <div data-type="p">    </div>
    <h3 id="lqnnql" data-type="h">      Multiple revisions are in Reserve state    </h3>
    <div data-type="p">      如果有两个或两个以上revision是Reserve状态，所有到reserve状态的流量转向activator    </div>