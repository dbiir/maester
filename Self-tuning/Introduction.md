# Introduction

[1] 是一篇类似综述的论文，不过更侧重与总结作者自己在Self-tuning DBMS方面十年间的工作。
论文中讲述了90年代末到2007年之间，Decision Support的逐渐广泛的应用对数据库self-tuning的影响非常大。
事务型数据库其实相对来说更便于tuning，因为query比较简单。而分析型数据库的查询非常复杂，查询优化技术也非常复杂，
在索引选择、物化视图、数据划分等偏向存储方面的tuning非常关键。可见面向分析的负载对self-tuning的需求更加强烈。

> **References**\
> [1] Self-tuning database systems: a decade of progress， VLDB 07

> **Linked Topics**