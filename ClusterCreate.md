## 集群创建



　　KMR的某些功能依赖于KS3，在创建集群之前，请确认您已经开通KMR和KS3服务，并已经创建AccessKey/SecretKey ，参阅KS3官方文档 [创建密钥](http://ks3.ksyun.com/doc/console/key/create.html)

　　如需使用KS3存放原始数据，参阅 [数据导入](DataImport.md)
  
　　KMR提供了临时集群和常驻集群两种类型，临时集群在作业执行完毕后会自动释放，适合批量数据计算；常驻集群提供了更高的可用性，集成了更丰富的Hadoop生态组件，适合流计算、实时数据查询或者较为复杂的数据分析场景。不同类型集群的创建步骤略有不同
  

###   创建步骤



　　1.登录金山云控制台，选择数据分析->托管Hadoop

　　2.选择“集群管理”,点击“新建集群”按钮，进入集群创建向导

　　3.填写以下内容完成集群创建：
  
   　　[基本信息](#ji_qun_ji_ben_xin_xi)

   　　[软件与节点配置](#Software_And_Node)

   　　[网络设置与其他](#wang_luo_she_zhi)

   　　[引导与作业设置（仅临时集群）](#zuo_ye_she_zhi)
     
　　  
  <h3 name="ji_qun_ji_ben_xin_xi" id="ji_qun_ji_ben_xin_xi">基本信息</h3>
  

---



![](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/KMR2.0/2.2-basicInfo.png)

**集群类型** ：KMR提供临时集群和常驻集群两种类型，临时集群在作业执行完毕后会自动释放，适合批量数据计算；常驻集群提供了更高的可用性，集成了更丰富的Hadoop生态组件，适合流计算、实时数据查询或者较为复杂的数据分析场景

**集群名称** ：创建集群时，会根据系统时间戳生成一个默认名称。您也可以为KMR集群输入描述性名称。长度限制为1-25个字符,支持数字、字母、特殊符号（_和-）该名称不必是唯一的

**数据中心** ：选择KMR集群所在数据中心。（如果需要使用KS3存储数据，应确保KMR与KS3 bucket 处于同一区域）

**计费方式** ：KMR计费方式根据不同的集群类型有所区别：常驻集群可选择按需计费和包年包月两种计费方式；临时集群仅可选择按需计费方式。若用户在试用期内，创建临时集群和常驻集群都可选择免费试用类型，详见 [KMR产品定价与选购](ProductPrice.md)

　　

  <h3 name="Software_And_Node" id="Software_And_Node">软件与节点配置</h3>
  
  
---



![](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/KMR2.0/2.2-node.png)


**产品版本** ：选择创建KMR集群所用的产品版本，选择不同版本可提供不同的集群基础配置和应用组件 

**应用程序** ：选择KMR集群中需要安装的Hadoop周边生态应用。对于常驻集群，可以将一些特殊的应用（如Kafka）部署到独立的节点组中 

 **用户配额** ：开通KMR服务时，会为每个账户分配一个资源配额，如果账户中使用的集群资源超过了该配额，则无法创建集群。如有特殊需求，请联系您的客户经理 
 
 **主节点** ：主要用于集群管理，并将计算程序和原始数据集分配到核心实例。此外，它还会跟踪每个计算作业的执行状态，监控实例的运行状况。KMR主节点与Hadoop系统的主节点相对应。临时集群集群只有一个主节点，常驻集群具有主、备两个主节点

 **核心节点** ：主要用于执行各项集群计算作业，同时作为hadoop分布式文件系统的数据节点存储数据。KMR核心节点与Hadoop系统的slave节点相对应

**任务节点** ：只有临时集群有任务节点，只用于执行各项集群计算作业,不作为分布式文件系统(HDFS)的数据存储节点，一个KMR临时集群可以有0至多个任务节点 

**节点配置** ：可根据实际的业务需求选择集群节点数量和类型，详见 [KMR产品定价与选购](ProductPrice.md) 

　　

  <h3 name="wang_luo_she_zhi" id="wang_luo_she_zhi">网络设置与其他</h3>
  
---

![](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/KMR2.0/2.2-internet.png)

**EIP绑定** ：EIP是绑定在集群Master节点上的公网IP地址，主要用于集群的远程管理和作业提交，带宽为1Mbps，暂时无法调节

**VPC网络** ：您可以使用默认VPC来创建KMR集群，也可以选择自定义VPC

**VPC子网** ：VPC子网是VPC中用于管理云主机的网络单元，您可以使用默认VPC子网，也可以选择自定义子网。如果使用自定义VPC，请确认VPC中已创建可用的VPC子网

**EndPoint子网** ：EndPoint可以在您的VPC和其他金山云服务之间创建私有连接，使用KMR服务必须指定EndPoint。 如果使用自定义VPC，请确认VPC中已创建可用的EndPoint

**SSH密钥（可选）** ：如果需要通过SSH访问集群，需要点击“绑定密钥”超链接为集群绑定SSH密钥，请参阅[SSH密钥管理](mi_yao_guan_li_zhi_nan.md) 

**自定义参数（可选）** ：您可以通过此功能来自定义各类集群应用的参数配置（如core-site,hadoop-env等）,点击“配置参数”超链接，在弹出对话框中选择配置文件，并填写该配置文件的自定义参数，（注意KMR不会对参数的正确性进行检查），自定义参数的格式为"Key1=value1,Key2=value2",配置多个参数时用逗号分隔

**元数据高可用（仅常驻集群、可选）** ：您可以通过该选项配置常驻集群的高可用元数据库，使用RDS实例元数据库能够提升元数据的可靠性和读写性能。通过选择同一机房的RDS实例，填写RDS实例端口、RDS用户名和RDS密码来配置

**日志归集（仅临时集群）** ：日志归集功能可以把集群和作业的日志统一存放在KS3的指定目录中，便于管理和持久保存。该选项默认关闭，开启该选项后需要选择日志在KS3上的存放目录，或在弹出的对话框中新建目录

**日志路径（仅临时集群）** ：您可以键入或浏览用于存储 KMR 日志的KS3 存储桶（bucket），例如 ks3://myemrbucket/logs，也可以让KMR为您生成一个KS3 路径。如果键入的文件夹名称在存储桶中不存在，系统将为您创建该文件夹。<br>各种集群服务和作业的日志在KS3上对应的路径结构，请参考 [KMR日志归集路径](LogPath.md) 

  <h3 name="zuo_ye_she_zhi" id="zuo_ye_she_zhi">引导与作业设置（仅临时集群）</h3>
  
---

![](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/KMR2.0/2.2-jobConfig.png)


**引导操作（可选）** ：　自定义引导操作是一个可选的高级选项，可以在集群启动时执行软件安装和环境准备等自定义操作，大多数情况下无需配置。如需配置，点击“设置”超链接，您可以在弹出的对话框中添加引导操作，包括填写引导脚本（使用存储在KS3中的脚本或者直接输入命令行），填写执行参数和勾选该脚本的执行节点。您也可以删除已添加的引导脚本

**作业设置** ：作业是提交到集群中的一个工作单元，一个作业可能包含一个或多个分布式计算任务，您需要为临时集群添加作业，并且对一个集群可提交多达256个作业，作业运行结束后，集群自动释放。您可以通过“添加作业”超链接添加作业，详情请参考[作业创建指南](StepCreate.md)，也可以对已添加的作业进行编辑和删除

