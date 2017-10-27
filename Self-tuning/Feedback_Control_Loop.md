# Feedback Control Loop

> **Abstract**\
> Feedback Control Loop应该是来自自动控制当中的概念，但是如果将DBMS看做是一个自动控制的对象，
> Feedback Control 同样是适用的。

[1] 中提出了一个在DBMS self-tuning中采用feedback control。论文中将一个feedback control loop分为三个部分：
Observation, Prediction和Reaction.

其中Observation主要是要找到正确的performance metrics并对其进行监测。performance metric除了例如throughput、
query response time这类显而易见的macroscopic metrics之外，往往更重要的是要找到一些有用的microscopic metrics，
例如每个data item上等待的事务个数（即等待队列长度，可以用排队论来分析）。

Prediction就是要根据microscopic metric可以很好地定义一些模型，将要tuning的参数和tuning的目标建立起直接的映社关系。
并用一些数学模型对最优tuning方案进行预判和决策。

Reaction就是执行Prediction给出的tuning方案。但是这里面有一些复杂的工程问题，online地去调整一些参数对于数据库系统来说，
有时是很有挑战的。

论文还举了一些例子来说明feedback control loop在实际的DBMS tuning中如何工作。论文也列举了一些self-tuning面临的挑战，
并肯定了RICS架构 (1) 对于self-tuning DBMS的重要性。



> **References**\
> [1] Self-tuning database technology and information services: from wishful thinking to viable engineering， VLDB 02

> **Linked Topics**\
> (1) Self-tuning/RISC_Architecture