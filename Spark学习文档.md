# Spark



### 概念

Spark是分布式计算引擎（框架）、是一个主从式集群架构；集群主要分为两部分：Driver：驱动程序划分计算任务、分发调度、集群各节点的Executor负责并行执行分片运算并缓存中间数据；

以RDD弹性式夫数据集为底层核心、借助惰性求值、血缘容错、内存缓存机制大幅降低磁盘IO，相比传统的MR计算效率提升，支持离线批处理和实时微批处理的流式计算、是大数据离线分析的主流核心计算框架

### Spark和MR的区别

开发语言上：Spark是基于MR开发的，spark底层使用scala开发的，MR是用Java开发的；但是Java在数据处理中并不方便，在数据处理中我们更关心数据如何处理，但是面向对象语言在大数据处理中不适用，但是函数式语言更为方便 把功能封装起来更为方便；

处理方式：MR运行慢，因为Hadoop出现的早，只考虑到了单一计算的操作，如果后续还要继续计算，只能再次把输出端作为输入端再次启动MR计算进行迭代式计算；Spark优化了计算过程，将中间结果放到内存里，可以写一系列算子串联起来运用内存计算；

### Spark部署方式

部署Spark实际就是指Spark的程序逻辑在谁提供的资源中运行：Standalone和Yarn，在生产环境中，主要采用Spark On Yarn的方式

Spark-Yarn的两种运行方式：yarn-client和yarn-cluster两种模式，主要区别在于Driver程序的运行节点；yarn-client：Driver程序运行在客户端，适用于交互测试希望立刻看到输出；yarn-cluster：Driver程序运行在由ResourceManger启动的AppMaster，适用于生产环境。

### RDD

分布式数据计算模型：一定是一个对象；一定封装了大量的方法和属性；一定需要适合进行分布式处理（减小数据规模，并行计算）

![image-20260620001417262](https://raw.githubusercontent.com/RoseYuxin/material/main/img/20260620001812959.png)

RDD的处理模式和JAVA IO流完全一样，都采用装饰者模式来实现功能;Spark在读取数据时分区设定存在三种方式:1.优先使用方法参数；2.使用配置参数parallelize(2)：spark.default.parallelism;3.采用环境默认值 setMaster("local[2]")
