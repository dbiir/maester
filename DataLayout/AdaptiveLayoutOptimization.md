# Adaptive Layout Optimization

> **Abstract**\
> Adaptive Layout Optimization（自适应布局优化，这里简称ALO）是指根据查询负载的变化，
> 数据库管理系统主动地调整数据存储的布局。在现有的工作当中，ALO主要是在行存和列存之间进行自适应地变化。
> 而要自适应地去做优化，最重要的是要检测到数据、查询负载、甚至是软硬件资源的变化。

>
>
AutoStore[1]中提出了Online Partitioning问题，其实就是ALO。这篇论文首先干了件比较无聊的事情，
就是把传统数据库中的水平划分(Horizontal Partitioning)和垂直划分(Vertical Partitioning)问题换个方式定义了一下，
表面上统一成了一个问题，叫做1DDP(One-dimension Online Partitioning Problem)问题：
但是其实还是分成水平和垂直两种情况来处理。然后提出了AutoStore这么一个支持Online Partitioning的存储格式。论文中主要的工作其实有两点：
1\) 提出了Workload Monitoring，根据Workload的变化Online地来做Data Partitioning (不确定有没有更早这方面的论文)，
它做Workload Monitoring的方法是设置一个定长的Query Window，每来一个Query滑动一下，滑动某个设定的次数之后就触发一次Partitioning；
2\) 给出了一个叫做O2P的Greedy数据划分算法，其实就是Hill-Climbing算法[5]


H2O[2]是比较早地提出Adaptive Store的论文（虽然Data Morphing更早提出Adaptive Store，但是并没有考虑Workload的变化，只是针对某个特定Workload做优化，严格来讲不算是Adaptive）。
这篇论文当中第3章介绍了通过做[Column Grouping(3)](%base_url%/DataLayout/ColumnGroup)在[Row Store(2)](%base_url%/DataLayout/RowStore)、
[Column Store(1)](%base_url%/DataLayout/ColumnStore)之间进行权衡，也就是通常所说的行列混合。
此外，论文中的方法会在查询执行时根据Layout选择一个最佳的执行计划。
论文第3.2节中也给出了一个Workload Monitoring的方案：
收集查询的Access Pattern，统计Column在查询中被共同访问的频率。SELECT子句和WHERE子句中出现的Column会用两个矩阵分别进行访问的统计。
被共同访问且访问频率相近的Column会被Co-locate到一起。论文中使用了定长的Window Size来控制所监测的查询个数，从而控制矩阵的大小。


CMU [Peloton](http://pelotondb.io/)团队也做了ALO方面的工作[3]，
他们在论文第3章里面提出了Physical Tile的概念，其实也是Column Group。论文旨在自适应地调整一个Tile中包含的Column个数。
论文第5章中也给出了一种Workload Monitoring的方法：
分别收集和跟踪查询中SELECT和WHERE子句中出现的Column，将WHERE子句中出现的Column Co-locate到一个Tile中。
它认为这样可以提高谓词过滤的性能。论文中没有对SELECT和GROUP BY中的列做Co-location。
由于查询会不断积累，该论文中的方案会随机从收集到的查询负载当中进行随机采样，仅对样本做以上的统计分析。
这篇论文其实并没有太大的创新，整体思路和Workload Monitoring方法和[2]很类似，
就连里面所用的计算Layout的算法都和Trojan Layout[6]中的很类似，这种方法没有任何的对效果的保证，就是很简单的贪心算法，
在Workload很复杂的情况下很可能是不work的（所以实验当中只用了5个不同类型的Query）。
论文主要贡献就是用了个Tile的概念包装了一下Data Layout，然后基于Tile提出了要把Layout和Query Execution解耦，这个思想还是比较有意思的。
此外论文中做了一个50列和一个500列的Benchmark，这个也比较有意思。


除了Workload Monitoring，[[4]](http://db.cs.cmu.edu/papers/2017/p42-pavlo-cidr17.pdf) 中用了机器学习（RNN）对未来的查询负载进行预测。
这篇论文中没有去讨论Layout的优化问题，但是在Related Works中比较详细地讨论了Workload Modeling问题。详细内容在
[Self-Tuning DBMS(4)](%base_url%/SelftuningDBMS/Introduction)中讨论。

> **References**\
> [1] Relax and Let the Database Do the Partitioning Online, BIRTE 11\
> [2] H2O: a hands-free adaptive store, SIGMOD 14\
> [3] Bridging the Archipelago between Row-Stores and Column-Stores for Hybrid Workloads, SIGMOD 16\
> [4] Self-Driving Database Management Systems, CIDR 17\
> [5] Data Morphing: An Adaptive, Cache-Conscious Storage Technique, VLDB 03\
> [6] Trojan Data Layouts: Right Shoes for a Running Elephant, SOCC 11

> **Linked Topics**\
> (1) DataLayout/ColumnStore\
> (2) DataLayout/RowStore\
> (3) DataLayout/ColumnGroup\
> (4) SelftuningDBMS/Introduction
