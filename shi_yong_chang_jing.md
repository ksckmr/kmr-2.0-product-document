## 使用场景


### 　　离线数据处理

  
　　离线数据处理是最常见的Hadoop应用场景，您可将原始数据上传到KS3或者集群HDFS文件系统中，通过控制台或者API来执行批量的离线处理作业。
  
  ![离线数据处理](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/KMR2.0/1.4Batch.jpg)
  

### 　　数据查询和报表

  
　　KMR提供了Hive和SparkSQL等类SQL查询方案，用户可使用简单直观的查询方法对海量的数据进行分析或者使用主流的BI工具生成报表。
  
  ![既席数据分析](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/KMR2.0/1.4SQL.jpg)
  
  

### 　　流式数据处理

  
　　流式数据处理逐渐成为大数据的热点，例如网站流量统计或游戏在线玩家数据，需要在不同粒度上对不同数据进行统计，既有实时性的需求，又需要涉及到聚合、去重、连接等较为复杂的统计需求，KMR提供了分布式消息队列Kafka,流式数据处理框架Storm以及Spark Streaming，帮助您轻松应对实时的数据处理需求。
  
![流式数据处理](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/KMR2.0/1.4Stream.jpg)

### 　　NoSQL数据库
　　互联网应用的典型特征是数据量大，高并发，业务增长快，KMR集成的Hbase是一种非常流行的分布式可扩展列存数据库，可以充分满足各种在线应用需求，同时又可以和其他大数据生态组件结合，形成端到端的方案。
  
  ![](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/KMR2.0/1.4NoSQL.jpg)
