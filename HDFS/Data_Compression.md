# Data Compression

> **Abstract**\
> HDFS上的数据可以采用一些压缩算法进行压缩。常用的压缩算法包括Snappy, LZO, 
> Gzip, bzip2等。

[1] 中对HDFS上的各种压缩算法做了介绍。

数据压缩不仅可以节约存储还可以提高数据处理的性能. 因为I/O和网络是数据处理的主要开销。
数据压缩不仅包括压缩源数据，还包括压缩中间数据。

Hadoop所支持的数据压缩格式并不都是splittable的。

* Snappy

Snappy是Google开发的具有高压缩速度和较好的压缩率的压缩算法 (compression codec)。 它在速度和压缩率之间作了较好的权衡。 
由于Snappy不是splittable的，它需要被用在一个特定的文件格式中，例如Parquet和Orc。

* LZO

LZO和Snappy类似，也是比较注重压缩速度的。不同的是，LZO 压缩后的文件是splittable的, 不过这需要一个额外的indexing步骤。
因此相对于snappy。LZO更适合用作一个独立的压缩格式来对HDFS上的文本格式的文件进行压缩。
需要注意的是LZO的license不允许它和HDFS一起发行，因此需要单独安装.

* Gzip

Gzip提供了比较高的压缩性能，平均达到snappy的2.5倍。但是它的写入性能不如Snappy (平均只能达到Snappy的一半)。
在读性能方便，Gzip和Snappy基本差不多。Gzip同样不是splittable的，因此也需要嵌入在一个文件格式中使用。
有时候，由于Gzip的压缩效果太好，导致压缩出的数据很小、数据块数很少，所以在执行数据处理任务时的并行度可能会偏低，
从而导致数据处理的速度反而降低。这个问题可以通过使用较小的数据块来避免。

* bzip2

bzip2提供了非常好的压缩性能，但是其读取的性能远不如Snappy。bzip2是splittable的。
bzip2压缩后的空间占用通常比Gzip还小一点，但这导致了数据读写性能的严重下降，通常只能达到Gzip的1/10。
因此除非存储空间非常的有限，bzip2并不是一个理想的选择。

Hadoop数据压缩方面的建议:
可以对MapReduce的中间结果采用压缩，这样通常可以大幅降低中间结果的大小，从而提高数据处理的性能。
数据的顺序和分布对压缩效果有很大的影响。

> **References**\
> [1] https://www.safaribooksonline.com/library/view/hadoop-application-architectures/9781491910313/ch01.html


> **Linked Topics**
