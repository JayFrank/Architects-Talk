# 理论历史由来
**CAP定理（CAP theorem）** 又被称作 *布鲁尔定理(Brewer's theorem)* ，是回加州大学柏克莱分校的计算机科学家埃里克·布鲁尔（Eric Brewer）在2000年的ACM PODC上提出的一个猜想。2002 年，麻省理工学院的赛斯·吉尔伯特（Seth Gilbert）和南希·林奇（Nancy Lynch）发表了布鲁尔猜想的证明，使之成为分布式计算领域公认的一个定理。

# CAP经典理论
CAP定理是分布式系统设计中最基础，也是最为关键的理论。它指出，分布式数据存储不可能同时满足以下三个条件：

* **一致性（Consistency）** ：每次读取要么获得最近写入的数据，要么获得一个错误。
* **可用性（Availability）** ：每次请求都能获得一个（非错误）响应，但不保证返回的是最新写入的数据。
* **分区容错性（Partition tolerance）** ：尽管任意数量的消息被节点间的网络丢失（或延迟），系统仍继续运行。

CAP定理表明，在存在网络分区的情况下，一致性和可用性必须二选一。当网络发生分区（不同节点之间的网络发生故障或者延迟较大）时，要么失去一致性（允许不同分区的数据写入），要么失去可用性（识别到网络分区时停止服务）。而在没有发生网络故障时，即分布式系统正常运行时，一致性和可用性是可以同时被满足的。

*注意：* CAP 定理中的一致性与 ACID 数据库事务中的一致性截然不同。ACID 的 C 指的是事务不能破坏任何数据库规则，如键的唯一性。与之相比，CAP 的 C 仅指单一副本这个意义上的一致性，因此只是 ACID 一致性约束的一个严格的子集。

CAP 理论看起来难理解，其实只要抓住一个核心点就能推导出来，不用死记硬背。在出现网络分区的时候，

* 如果系统不允许写入，那么意味着降低了系统的可用性，但不同分区的数据能够保持一致，即选择了 **一致性**。
* 如果系统允许写入，那么意味着不同分区之间的数据产生不一致，系统可用性得到保障，即选择 **可用性**。

# CAP的新理解
CAP 经常被误解，很大程度上是因为在讨论 CAP 的时候可用性和一致性的作用范围往往都是含糊不清的。如果不先定义好可用性、一致性、分区容忍在具体场景下的概念，CAP 实际上反而会束缚系统设计的思路。

首先，由于分区很少发生，那么在系统不存在分区的情况下没什么理由牺牲 C 或 A。

其次，C 与 A 之间的取舍可以在同一系统内以非常细小的粒度反复发生，而每一次的决策可能因为具体的操作，乃至因为牵涉到特定的数据或用户而有所不同。

最后，这三种性质都可以在程度上都可以进行度量，并不是非黑即白的有或无。可用性显然是在 0% 到 100% 之间连续变化的，一致性分很多级别，连分区也可以细分为不同含义，如系统内的不同部分对于是否存在分区可以有不一样的认知。

**理论抽象于现实，服务于现实，但绝不等于现实。** 对 CAP 理论“三选二”的误解就源于我们经常把理论等同于现实。

CAP 的诞生主要是为了拓宽设计思路，不要局限在强一致性的约束中。简单的把“三选二”进行套用反而限制了设计思路。在现实世界中，不同业务场景对可用性和一致性的要求不一样，并且一致性和可用性的范围和区间是动态变化的，并不是非此即彼。因此，准确理解 CAP 理论，从管理分区的角度出发，结合具体的业务场景，才能做出更好的系统设计。

# CAP相关的理论
## ACID理论
ACID 是数据库管理系统为了保证事务的正确性而提出来的一个理论，ACID 包含四个约束：
1. **Atomicity（原子性）** :一个事务中的所有操作，要么全部完成，要么全部不完成，不会在中间某个环节结束。事务在执行过程中发生错误，会被回滚到事务开始前的状态，就像这个事务从来没有执行过一样。
2. **Consistency（一致性）** :在事务开始之前和事务结束以后，数据库的完整性没有被破坏。
3. **Isolation（隔离性）** :数据库允许多个并发事务同时对数据进行读写和修改的能力。隔离性可以防止多个事务并发执行时由于交叉执行而导致数据的不一致。事务隔离分为不同级别，包括读未提交（Read uncommitted）、读提交（read committed）、可重复读（repeatable read）和串行化（Serializable）。
4. **Durability（持久性）** :事务处理结束后，对数据的修改就是永久的，即便系统故障也不会丢失。

## BASE理论
BASE是Basically Availability（基本可用）、Soft State（软状态）和Eventually Consistency（最终一致性）三个短语的缩写。BASE理论的核心思想就是 **即使无法做到强一致性（CAP的一致性就是强一致性性），但应用可以采用适合的方式达到最终一致性。**

# 参考文献
* [An Illustrated Proof of the CAP Theorem](https://mwhittaker.github.io/blog/an_illustrated_proof_of_the_cap_theorem/)
* [E. Brewer, "CAP twelve years later: How the "rules" have changed," in Computer, vol. 45, no. 2, pp. 23-29, Feb. 2012.](https://ieeexplore.ieee.org/document/6133253)
* [Cluster-Based Scalable Network Services](http://citeseerx.ist.psu.edu/viewdoc/download?spm=a2c4e.11153940.0.0.51a38c31rjMf0R&doi=10.1.1.1.2034&rep=rep1&type=pdf)
* [Harvest, Yield and Scalable Tolerant Systems](http://citeseerx.ist.psu.edu/viewdoc/download?spm=a2c4e.11153940.0.0.51a38c31rjMf0R&doi=10.1.1.24.3690&rep=rep1&type=pdf)
* [肖汉松, "分布式系统：CAP 理论的前世今生", 云栖社区](https://yq.aliyun.com/articles/700488)
* [阮一峰, "CAP 定理的含义", 阮一峰的网络日志](http://www.ruanyifeng.com/blog/2018/07/cap.html)
* ["ACID、BASE和CAP原理", CSDN](https://blog.csdn.net/sinat_27186785/article/details/52032510)
