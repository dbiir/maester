# Index Selection

> **Abstract**\
> Index Selection是Self-tuning DBMS领域最早被研究的内容，因为索引对一个数据库的性能来说是至关重要的。
> 早在90年代就有相关的研究工作。

[1] 中提出了一个帮助DBA选择索引的方法，并在SQL Server 7.0上实现了一个索引选择的工具。
论文中提出的方法将Workload作为输入，给出可行的索引方案的建议。具体的方法没有细看。
论文当中很有意思的一个思想是将优化工具（例如本文中的索引选择工具）与查询优化器配合起来，
体现了 Optimizer-in-the-loop 的思想。

[2] 和 [1] 是相同的作者，做的工作也是一样的。论文主要提出了 'what-if' 的索引选择方式，
没有细看，感觉大概的意思就是对workload的变化和数据规模的变化做出一些假设和预判，
然后分析这些 what-if index 是否可行。实际上是把预测的思想引入的DBMS的tuning中，
不再假设workload和数据都是静态的。

[3] 是更新一点的Index Selection方面的论文，还没有读。

> **References**\
> [1] An Efficient Cost-Driven Index Selection Tool for Microsoft SQL Server, VLDB 97\
> [2] AutoAdmin “what-if” index analysis utility, SIGMOD 98\
> [3] An Online Approach to Physical Design Tuning, ICDE 07

> **Linked Topics**
