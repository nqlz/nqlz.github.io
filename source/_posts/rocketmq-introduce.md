---
title: 初识RocketMQ
date: 2019-09-27 00:02:43
tags: 
  - RocketMQ
toc: true
categories: 
  - RocketMQ
---
## RocketMQ的整体介绍
RocketMQ是一款分布式、队列模型的消息中间件，4.3.x版本后支持分布式事务。
### 优势：
- 天然支持集群模型、负载均衡、水平扩展能力。
- 上亿级别的消息堆积能力，天猫，双十一啥的。
- 采用零拷贝的原理，顺序写盘，随机读。
- 丰富的API使用。支持同步消息、异步消息、顺序消息、延迟消息、事务消息等等。
- 底层通信框架Netty nio
- 强调集群无单点，可扩展，任意一点高可用，水平可扩展。
- 消息失败重试机制，消息可查询。例如rabbitmq中只能用重入队列，死信队列，消息重发，或者监听再处理来实现。它的重试机制是有时间间隔的，可以定义重试次数。
<!-- more-->

## RocketMQ概念模型
Producer:消息生产者。
consumer：消息消费者。
push consumer:需要向consumer对象注册一个监听器，
pull consumer:主动向Broker请求拉取信息，
producer group:生产者集合，用于发送一类消息
consumer group:消费者集合，用于消费一类消息
Brocker：MQ消息服务器，中转角色，用于消息存储转发。