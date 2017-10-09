# Adaptive Layout Optimization

Adaptive Layout Optimization（自适应布局优化，这里简称ALO）是指根据查询负载的变化，
数据库管理系统主动地调整数据存储的布局。关于Adaptive（自适应），最直观的例子就是变色龙，
它可以根据环境的变化而主动地改变自己的颜色。
在现有的工作当中，ALO主要是在行存和列存之间进行自适应地变化。

在行列之间作自适应调整的工作有以下三个。[H2O[1]](https://dl.acm.org/citation.cfm?id=2588555.2610502) 是比较早的ALO方面的工作。
这篇论文当中第3章介绍了如何通过Column Group在Row Store、Column Store之间进行权衡，
并且在查询执行时根据Layout选择一个最佳的执行计划。
[AutoStore[2]](https://link.springer.com/chapter/10.1007/978-3-642-33500-6_5) follow up
了H2O，根据查询负载对数据进行自动的行列划分。CMU [Peloton](http://pelotondb.io/)团队也做了ALO方面的工作[[3]](https://dl.acm.org/citation.cfm?id=2915231)，
他们在论文第3章里面提出了Physical Tile的概念，其实也是Column Group，自适应地去调整一个Tile中包含的Column个数。
> References:\
> [1] H2O: a hands-free adaptive store, SIGMOD 14\
> [2] Relax and Let the Database Do the Partitioning Online, BIRTE 11\
> [3] Bridging the Archipelago between Row-Stores and Column-Stores for Hybrid Workloads, SIGMOD 16 

