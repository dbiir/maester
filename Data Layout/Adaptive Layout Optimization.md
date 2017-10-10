# Adaptive Layout Optimization

> **Abstract**\
> Adaptive Layout Optimization（自适应布局优化，这里简称ALO）是指根据查询负载的变化，
> 数据库管理系统主动地调整数据存储的布局。在现有的工作当中，ALO主要是在行存和列存之间进行自适应地变化。
> 而要自适应地去做优化，最重要的是要检测到数据、查询负载、甚至是软硬件资源的变化。

现有工作中ALO主要是在行存、列存、行列混合存储之间作自适应调整。AutoStore[[1]](https://link.springer.com/chapter/10.1007/978-3-642-33500-6_5) 
根据查询负载对数据进行自动的行列划分。H2O[[2]](https://dl.acm.org/citation.cfm?id=2588555.2610502) 是比较早的ALO方面的工作。
这篇论文当中第3章介绍了如何通过[Column Group](%base_url%/Data%20Layout/Column%20Group)在[Row Store](%base_url%/Data%20Layout/Row%20Store)、
[Column Store](%base_url%/Data%20Layout/Column%20Store)之间进行权衡，
并且在查询执行时根据Layout选择一个最佳的执行计划。
CMU [Peloton](http://pelotondb.io/)团队也做了ALO方面的工作[[3]](https://dl.acm.org/citation.cfm?id=2915231)，
他们在论文第3章里面提出了Physical Tile的概念，其实也是Column Group，自适应地去调整一个Tile中包含的Column个数。

在检测变化方面，目前工作中主要是检测查询负载的变化，并没有去关注数据和系统中软硬件资源的变化。
H2O[[2]](https://dl.acm.org/citation.cfm?id=2588555.2610502) 第3.2节中给出了一个Workload Monitoring的方案：
统计Column在查询中被共同访问的频率。它会收集查询的Access Pattern。SELECT子句和WHERE子句中出现的Column会用两个矩阵分别进行访问的统计。
被共同访问且访问频率相近的Column会被Co-locate到一起。论文中使用了定长的Window Size来控制所监测的查询个数，从而控制矩阵的大小。
[[3]](https://dl.acm.org/citation.cfm?id=2915231) 第5章中"On-line Query Monitoring"给出了一种方法：
分别收集和跟踪查询中SELECT和WHERE子句中出现的Column，将WHERE子句中出现的Column Co-locate到一个Tile中。
它认为这样可以提高谓词过滤的性能。论文中没有对SELECT和GROUP BY中的列做Co-location。
由于查询会不断积累，该论文中的方案会随机从收集到的查询负载当中进行随机采样，仅对样本做以上的统计分析。

除了对查询负载的监测，[[4]](http://db.cs.cmu.edu/papers/2017/p42-pavlo-cidr17.pdf) 中用了机器学习（RNN）对未来的查询负载进行预测。
这篇论文中没有去讨论Layout的优化问题，但是在Related Works中比较详细地讨论了Workload Modeling问题。详细内容在
[Self-Tuning DBMS](%base_url%/Self-tuning%20DBMS/Introduction) Topic中讨论。

> **Reading List**\
> [1] Relax and Let the Database Do the Partitioning Online, BIRTE 11\
> [2] H2O: a hands-free adaptive store, SIGMOD 14\
> [3] Bridging the Archipelago between Row-Stores and Column-Stores for Hybrid Workloads, SIGMOD 16\
> [4] Self-Driving Database Management Systems, CIDR 17

> **Linked Topics**\
> Data Layout/Column Store\
> Data Layout/Row Store\
> Data Layout/Column Group\
> Self-Tuning DBMS/Introduction
