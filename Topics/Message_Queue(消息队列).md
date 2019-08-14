# 消息队列
**一个大型的分布式系统，通常都会异步化，走消息总线。** 消息队列作为最主要的基础组件，在整个体系架构中，有着及其重要的作用。

## 业界主流消息队列

消息队列 | 主页 | 是否开源 | Github地址
---|---|---|---
Apache Kafka | http://kafka.apache.org/ | 开源 | https://github.com/apache/kafka
Apache RocketMQ |http://rocketmq.apache.org/ | 开源 | https://github.com/apache/rocketmq
RabbitMQ | https://www.rabbitmq.com/ | 开源 | https://github.com/rabbitmq
Apache ActiveMQ| http://activemq.apache.org/ | 开源 | https://github.com/apache/activemq
Apache Pulsar | http://pulsar.apache.org/ | 开源 | https://github.com/apache/pulsar

Kafka是目前最常用的消息队列，尤其是在大数据方面，有着极高的吞吐量。而RocketMQ和RabbitMQ，都是电信级别的消息队列，在业务上用的比较多。2019年了，不要再盯着JMS不放了（说的就是臃肿的ActiveMQ）。

Pulsar是为了解决一些Kafka上的问题而诞生的消息系统，比较年轻，工具链有限。有些激进的团队经过试用，反响不错。

MQTT具体来说是一种协议，主要用在物联网方面，能够双向通信，属于消息队列范畴。
