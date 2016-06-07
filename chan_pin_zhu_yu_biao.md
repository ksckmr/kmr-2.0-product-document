# 产品术语表


| 英文术语 | 简写/缩写 | 中文术语 | 术语描述 |
| -- | -- | -- | -- |
| Kingsoft MapReduce | KMR |  | 金山云平台上的Hadoop托管集群，可通过Web对外提供服务 |
| KMR cluster | Cluster | KMR 集群 | 由若干金山云主机实例组成的Hadoop集群 |
| KMR Master Node | Master | 主节点 | 主要用于集群管理，并将计算程序和原始数据集分配到核心实例。此外，它还会跟踪每个计算作业的执行状态，监控实例的运行状况。KMR主节点与Hadoop系统的主节点相对应。一个KMR集群只有一个主节点。 |
| KMR Core Node | Core | 核心节点 | 主要用于执行各项集群计算作业，也做为hadoop分布式文件系统的数据节点存储数据。KMR核心节点与Hadoop系统的slave节点相对应。一个KMR集群可以有2至多个核心节点 |
| KMR Job | Job | 作业 | 一个作业是提交到集群中的一个工作单元。 一个作业可能包含一个或多个Hadoop任务，或者包含安装或配置一个应用程序的指令。 您可以对一个集群提交多达256个作业。 |
| SSH KEY |  | SSH密钥 | 指用户在控制台上上传的SSH 公钥 |
| Kingsoft standard storage service | KS3 | 云存储 | 金山云标准存储服务 |
| Hadoop file system | HDFS |  | Hadoop 分布式文件系统 (HDFS) 是一种分布式的、可扩展的文件系统，供 Hadoop 使用。 |
| MapReduce | MR | | MapReduce 是一种用于分布式计算的编程模型,用于大规模数据集的并行运算。| 
| Hadoop |  |  | Apache Hadoop 是一种开源 Java 软件框架，支持跨越一组服务器处理大量数据。它可以在一台服务器或成千上万台服务器上运行。Hadoop 使用名为 MapReduce 的编程模型在多个服务器之间分配处理工作。此外，它还实施了一个名为 HDFS 的分布式文件系统，在多个服务器之间存储数据。 |
