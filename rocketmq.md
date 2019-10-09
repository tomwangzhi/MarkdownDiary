### rocketmq概述

> 整理自：https://blog.csdn.net/qq_28851503/article/details/100182071

1. rocketmq简介
2. rocketmq发送消息的三种方式

#### 1. rocketmq简介

```text
消息队列rocketmq是Apache旗下的开源项目（原是Alibaba开源的项目）
，当springboot盛行后，Apache团队开源了rocketmq-spring来
帮助我们在springboot中快速集成rocketmq，
只需引入rocketmq-spring-boot-starter即可。

```

#### rocketmq发送消息的三种方式
1.同步发送 sync 

这种方式只有在消息完全发送完成之后才返回结果，
此方式存在需要同步等待发送结果的时间代价
在主动声明本次消息发送失败之前，内部实现将重试一定次数，
默认为2次
> rocketMQTemplate.syncSend("topic-name", "send sync message !");

2. 异步发送 async

发送消息采用异步发送模式，消息发送后立刻返回，当消息完全完成发送后，
会调用回调函数sendCallback来告知发送者本次发送是成功或者失败。
异步模式也在内部实现了重试机制，默认次数为2次
> rocketMQTemplate.asyncSend("topic-name", "send sync message !",, new SendCallback() {});

3. 直接发送 one-way

采用one-way发送模式发送消息的时候，发送端发送完消息后会立即返回，
不会等待来自broker的ack来告知本次消息发送是否完全完成发送。
> rocketMQTemplate.sendOneWay("","")

> 在实际使用场景中，利用何种发送方式，可以总结如下：
  当发送的消息不重要时，采用one-way方式，以提高吞吐量；
  当发送的消息很重要是，且对响应时间不敏感的时候采用sync方式;
  当发送的消息很重要，且对响应时间非常敏感的时候采用async方式；