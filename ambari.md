## Ambari

　　Apache Ambari是一种基于Web的工具，支持Hadoop集群的供应、监控和管理。

　　Ambari支持HDFS、MapRedue、Hive、SPark、Storm、Pig、Hbase、Zookeeper等的集中管理，也是5个顶级Hadoop管理工具之一。

　　更多资料参见 [Apache Ambari](http://ambari.apache.org/) 官网

　　KMR对Ambari对了权限控制，暂时只开放只读权限，您可以查看集群的监控和配置信息，不支持更改配置。


### 准备
---

您已成功创建一个常驻集群，登录控制台，进入集群详情页面，通过管理工具进入“Ambari控制台”，用户名和密码均为“kmr"，登录成功后，即进入Ambari页面。

![](AmbariEntrance.png)


Ambari Dashboard页面展示了集群的整体情况，可以点击各个图表查看具体信息
![](AmbariDashboard.png)


### 服务级别的监控管理
---

服务级别监控管理包括对HDFS,MapReduce，Storm,Spark等的管理，通过左边导航点击对应的服务，可以查看该服务的概况和使用图表，也可以通过“+”自定义需要显示的指标

### 机器级别的监控管理
---

### 模块级别的监控管理
---



