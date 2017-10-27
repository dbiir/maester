# RISC Architecture

> **Abstract**\
> RISC Architecture是一种数据库架构的设计思想，和现有的商业数据库不断堆叠的错综复杂的复杂架构针锋相对。
> RISC架构参考了处理器设计中的RISC体系结构，这种架构可能更便于实现数据库管理系统的Self-tuning。


[1]是一篇古老但是很有意思的论文。一作Surajit Chaudhuri比较早研究self-tuning DBMS的人，有很多相关的工作。
这篇论文指出了当时商业DBMS的架构设计越来越复杂导致难以tuning，同时提出了将计算机体系结构中的RISC思想应用到数据库的架构设计当中。

论文中首先指出了数据库系统中存在的几个问题：
1. 数据库系统在市场竞争的驱动下，过分追求新的feature而导致数据库系统复杂度超出了人们的管理能力；
2. SQL语言过于复杂，除了常用的SPJ和Aggregation之外，SQL92标准中包含了大量复杂的、难以理解的、很少被用到的语法，
这也导致SQL越写越复杂、越来越难以理解和调试；
3. 商业数据库由于急于抢占市场，来不及对原有的架构进行很好的调整就强行堆叠新功能，
长期以来导致系统过于庞大和复杂。例如查询优化器之类的组件已经复杂到几乎无人可以理解其全部细节的程度，这就导致了数据库系统的性能不可预知；
4. 正因为以上的原因，导致数据库很难tune；
5. 越来越多的应用倾向于自己管理部分数据，而将数据库作为底层的存储使用，构建一个复杂的universal DBMS是不符合实际的；
6. 运行DBMS的计算设备越来越多样和小型化，甚至很多移动设备上都有数据库了，一个复杂庞大、难以裁剪的DBMS显然是不适应这种需求的；
7. 越来越复杂的数据库系统阻碍了system-oriented database research.

然后论文中列出了DBMS发展中的几个陷阱：
1. universality trap, 过于追求功能完善；
2. cost trap, 忽略系统运维、操作和调优的代价；
3. transparency trap, 过于追求对用户透明而忽视系统的效率；
4. resource sharing trap, 资源共享导致系统的tuning变得更加困难。

论文围绕这些问题论述了RISC架构的意义，即将数据库管理系统的各个模块解耦，保证每个模块都有较少的功能和比较简单的API，
让人们既可以理解每个模块，又可以理解模块之间的交互。
这样的架构使得self-tuning更加容易实施，也使得数据库系统更加便于维护和扩展，
体现了 'think globally, fix locally' 的策略。



> **References**\
> [1] Rethinking Database System Architecture: Towards a Self-Tuning RISC-Style Database System, VLDB 00\

> **Linked Topics**
