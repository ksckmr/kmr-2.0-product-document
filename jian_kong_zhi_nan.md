## 集群监控告警

　　
  监控和告警对于维护一个集群正常运转以及对集群进行调优排错等工作至关重要，由于KMR临时集群和常驻集群的使用需求不尽相同，我们采用不同的解决方案：
  
*   对于临时集群，KMR集成了通用的集群管理工具-Ganglia来对集群进行监控

  
*   对于常驻集群，KMR对接了金山云监控，管理员可以在云监控页面查看集群的监控图表并对关键指标配置告警策略，同时我们集成了强大集群管理工具ambari，可以对集群实现更加精细的监控和管理。


*   除此之外，hadoop生态组件提供了较为丰富的web管理功能，您也可以通过控制台直接跳转查看
<br/> <br>
  [1. 临时集群监控](#temp_cluster)

  [2. 常驻集群监控告警](#durable_cluster)

  [3. Hadoop原生管理工具](#hadoop_tools)
  
  
<h3 name="temp_cluster" id="temp_cluster">临时集群监控</h3>
  

---


KMR临时集群中集成了Ganglia监控工具，用户可以通过控制台“集群详情”-“管理工具”-“Ganglia”进入

　**　使用Ganglia监控集群状态**

　　Ganglia是UC Berkeley发起的一个开源集群监视项目，设计用于测量数以千计的集群节点，主要用来监控系统性能，如：CPU 、内存和硬盘利用率， I/O负载、网络流量情况等，通过曲线很直观的了解到每个节点的工作状态，对合理调整、分配系统资源，提高系统整体性能起到重要作用。

　　在KMR中，我们为您在集群中集成了Ganglia服务，您可通过“集群详情”-“管理工具”-“Ganglia”直接进入

　　Ganglia服务页面如下图所示：

![ganlia](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/jkzn1.png)


  
<h3 name="durable_cluster" id="durable_cluster">常驻集群监控告警</h3>
  

---
KMR常驻集群中集成了Ambari管理工具，用户可以通过控制台“集群详情”-“管理工具”-“ambari”进入

Ganglia是UC Berkeley发起的一个开源集群监视项目，设计用于测量数以千计的集群节点，主要用来监控系统性能，如：CPU 、内存和硬盘利用率， I/O负载、网络流量情况等，通过曲线很直观的了解到每个节点的工作状态，对合理调整、分配系统资源，提高系统整体性能起到重要作用。

　　在KMR中，我们为您在集群中集成了Ganglia服务，您可通过“集群详情”-“管理工具”-“Ganglia”直接进入

　　Ambari服务页面如下图所示：




  
  
<h3 name="hadoop_tools" id="hadoop_tools">Hadoop原生管理工具</h3>
  

---


　　安装在 KMR集群上的 Hadoop 和其他应用程序会将用户界面发布在主节点上托管的网站，这些页面记录了各类集群服务的统计和监控信息，你可以直接通过“集群详情”-“管理工具”进入各个页面查看。

　**　YARN ResourceManager**

　　YARN ResourceManager管理工具可以查看集群运行的详细信息，包括节点信息、应用信息和调度信息等。


![resourcemanager](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/jkzn2.png)

　　**HDFS Namenode**

　　HDFS Namenode用来查看HDFS的使用状况，包括NameNode和DataNode的具体信息。

![namenode](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/jkzn3.png)


　　**OOZIE**

　　Oozie是服务于Hadoop生态系统的工作流调度工具，Oozie工作流是放置在控制依赖DAG（有向无环图）中的一组动作，把多个Map/Reduce作业组合到一个逻辑工作单元中，来完成更大型的任务。

![oozie](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/jkzn4.png)


　　**YARN HistoryServer**

　　JobHistory是Hadoop自带的历史服务器，可以查看已经运行完的MapReduce作业记录，例如使用的Map数、Reduce数、作业提交时间、作业启动时间、作业完成时间等信息。

![historyserver](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/jkzn5.png)


　　**Spark History Server**

　　运行Spark应用程序的时候，driver会提供一个webUI显示应用程序的运行信息，但是应用程序完成后，将关闭端口，即无法查看应用程序的历史记录。Spark History Server将运行完的应用程序信息义Web的方式提供给用户。
  

![spark](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/jkzn6.png)