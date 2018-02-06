# HDFS Caching

> **Abstract**\
> HDFS支持对数据进行Cache。在2.3.0之前，主要依靠操作系统的Page Cache，
> 2.3.0之后增加了HDFS centralized cache management（集中式缓存管理）.

[1,2,3] 中介绍了Linux系统page cache的原理。与page cache相关的是Linux内核的read ahead（预读）机制。
Read ahead可以看做一种提前的、主动的cache. [3] 中对head ahead也做了详细的介绍。
Linux系统的预读是以磁盘扇区为单位的，通常默认扇区大小为512字节，默认read ahead为256个扇区。

HDFS本身也有对数据块的预读，以字节为单位。
[4] 中的dfs.datanode.readahead.bytes配置了HDFS read ahead的大小。此外，HDFS中还可以配置是否drop page cache.

[5] 中讨论了page cache在HDFS中的问题，以及HDFS centralized cache中的一些技术问题，例如Zero Copy Read等。
[6] 是HDFS centralized cache management的官方文档，介绍了如何在Apache Hadoop中使用这一Cache特性。
[7] 中讨论了更多的原理和使用细节。目前HDFS的集中式缓存还只支持文件和目录级别的缓存。

> **References**\
> [1] [Linux 内核的文件 Cache 管理机制介绍](https://www.ibm.com/developerworks/cn/linux/l-cache/index.html)\
> [2] [Linux文件读写机制及优化方式](http://littlewhite.us/archives/381)\
> [3] [Linux内核文件Cache机制](http://www.ilinuxkernel.com/files/Linux.Kernel.Cache.pdf)\
> [4] [hdfs-default.xml](https://hadoop.apache.org/docs/r2.7.3/hadoop-project-dist/hadoop-hdfs/hdfs-default.xml)\
> [5] [New in CDH 5.1: HDFS Read Caching](http://blog.cloudera.com/blog/2014/08/new-in-cdh-5-1-hdfs-read-caching/)\
> [6] [Centralized Cache Management in HDFS](https://hadoop.apache.org/docs/r2.7.3/hadoop-project-dist/hadoop-hdfs/CentralizedCacheManagement.html)\
> [7] [HDFS集中式的缓存管理原理与代码剖析](http://www.infoq.com/cn/articles/hdfs-centralized-cache)

> **Linked Topics**
