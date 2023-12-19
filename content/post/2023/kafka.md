---
title: "Kafka 面试题" # Title of the blog post.
date: 2023-12-06T18:05:43+08:00 # Date of post creation.
description: "Article description." # Description used for search engine.
featured: true # Sets if post is a featured post, making it appear on the sidebar. A featured post won't be listed on the sidebar if it's the current page
draft: false # Sets whether to render this page. Draft of true will not be rendered.
toc: false # Controls if a table of contents should be generated for first-level links automatically.
# menu: main
usePageBundles: false # Set to true to group assets like images in the same folder as this post.

codeMaxLines: 10 # Override global value for how many lines within a code block before auto-collapsing.
codeLineNumbers: false # Override global value for showing of line numbers within code block.
figurePositionShow: true # Override global value for showing the figure label.
showRelatedInArticle: false # Override global value for showing related posts in this series at the end of the content.
categories:
  - Technology
tags:
  - queue
  - Kafka
---

## 概念

- *Broker* : 一个 Kafka 节点就是一个 Broker
- *Consumer Group*：每个Consumer都属于一个Consumer Group，每条消息只能被Consumer Group中的一个Consumer消费，但可以被多个Consumer Group消费。
- *Controller：* Kafka 集群中的其中一个服务器，用来进行Leader election以及各种 Failover 操作。

## 使用场景

- **日志收集** 
- **消息队列**（系统解耦，通过消息交互，异步处理）

## Kafka 性能高原因

- 磁盘顺序读写，使用PageCache 缓存
- 零拷贝技术（发送使用sendfile，index使用mmap，log不用）
- Kafka支持批量读写和批量压缩，减少了网络传输的延迟和带宽开销。

## Kafka 文件高效存储设计原理

- Kafka把Topic中一个Partition大文件分成多个小文件段
- 索引文件稀疏存储，减少索引占用空间
- 索引元数据全部映射到 memory，可以避免 Segment 文件的磁盘I/O操作

## Kafka 的优缺点

优点

- 高性能、高吞吐量、低延迟：Kafka 生产和消费消息的速度都达到每秒10万级
- 高可用：所有消息持久化存储到磁盘，并支持数据备份防止数据丢失
- 高并发：支持数千个客户端同时读写
- 容错性：允许集群中节点失败（若副本数量为n，则允许 n-1 个节点失败）
- 高扩展性：Kafka 集群支持热伸缩，无须停机

## Kafka 写入过程

- 封装成一个 ProducerRecord 对象，然后序列化
- 对消息进行分区处理
- 放入生产者的缓存区，多条消息会被封装成一个批次（Batch），默认一个批次的大小是 16KB
- Sender 线程启动以后会从缓存里面去获取可以发送的批次，分批发送

## Kafka 读取过程

- 使用pull模式

## 负载均衡与故障转移

**负载均衡**

通过选举选出leader，读写分散到不同的partition。

**故障转移**

每台 Kafka 服务器启动后会以会话的形式把自己注册到 Zookeeper 服务器上，如果故障会断连，触发迁移。

？？？迁移逻辑

## Kafka 创建Topic后如何将分区放置到不同的 Broker 中

Kafka创建Topic将分区放置到不同的Broker时遵循以下规则：

1. 副本因子不能大于Broker的个数。
2. 第一个分区（编号为0）的第一个副本放置位置是随机从Broker List中选择的。
3. 其他分区的第一个副本放置位置相对于第0个分区依次往后移。也就是如果有3个Broker，3个分区，假设第一个分区放在第二个Broker上，那么第二个分区将会放在第三个Broker上；第三个分区将会放在第一个Broker上，更多Broker与更多分区依此类推。剩余的副本相对于第一个副本放置位置其实是由`nextReplicaShift`决定的，而这个数也是随机产生的。





## 参考

https://javabetter.cn/interview/kafka-40.html
