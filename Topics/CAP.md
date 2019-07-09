# CAP经典理论
CAP 定理是分布式系统设计中最基础，也是最为关键的理论。它指出，分布式数据存储不可能同时满足以下三个条件：

* **一致性（Consistency）** ：每次读取要么获得最近写入的数据，要么获得一个错误。
* **可用性（Availability）** ：每次请求都能获得一个（非错误）响应，但不保证返回的是最新写入的数据。
* **分区容忍（Partition tolerance）** ：尽管任意数量的消息被节点间的网络丢失（或延迟），系统仍继续运行。

# CAP理论的扩展
## ACID

## BASE
BASE是Basically Availability（基本可用）、Soft State（软状态）和Eventually Consistency（最终一致性）三个短语的缩写。BASE理论的核心思想就是 **即使无法做到强一致性（CAP的一致性就是强一致性性），但应用可以采用适合的方式达到最终一致性。**
