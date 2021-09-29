## Kafka
### 机架感知 （Rack Awareness）
Kafka在0.10时引入了机架感知，如果在集群很大的情况下，所有的replica都在同一个机架上，那么一旦此机架出问题，那么所有的replica都将失效（当然这种情况非常少）。现在kafka可以让replica分布到不同的机架上，提高了整个集群的稳定性和可用性。所以如果指定了机架信息，那么Kafka在分配replica的时候，就会尽可能的为partition的多个副本分配不同的机架的broker。

参考资料：https://www.jianshu.com/p/da8cd8e48722

