## 创建集群－高级选项

　　高级选项提供了更多的集群配置参数，如果您是初次使用KMR，建议切换到“创建集群-快速选项”
  
　　KMR的某些功能依赖于KS3，在创建集群之前，请确认您已经开通KMR和KS3服务，并已经创建AccessKey/SecretKey 参阅KS3官方文档 [创建密钥](http://www.ksyun.com/doc/art/id/612)

　　如需使用KS3存放原始数据，参阅 [数据导入到KS3](shu_ju_dao_ru_zhi_nan.md)。

　　打开金山云控制台，选择KMR服务，点击“新建集群”，选择页面上方的“切换到高级选项”，进入集群配置页面
  
　　顺序完成以下步骤：
  
   　　[1. 集群基本信息](#ji_qun_ji_ben_xin_xi)

   　　[2. 安全与访问](#an_quan_yu_fang_wen)

   　　[3. 添加作业](#tian_jia_zuo_ye)

   　　[4. 确认订单](#que_ren_ding_dan)
  
  <h3 name="ji_qun_ji_ben_xin_xi" id="ji_qun_ji_ben_xin_xi">1.集群基本信息</h3>
  

---


　　1.填写集群的基本信息

![基本信息1](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/jbxx1.png)

| 字段 | 操作 |
| -- | -- |
| **集群名称** | 创建集群时，会根据系统时间戳帮您创建一个默认名称。您也可以为KMR集群输入描述性名称。该名称不必是唯一的。 |
| **选择区域** | 选择KMR集群所在区域。（如果需要使用KS3存储数据，应确保KMR与KS3处于同一区域） |
| **集群自动释放** | 默认情况下，该选项处于关闭状态。集群自动释放开启时，当集群中最后一个作业执行完毕会自动释放集群。**如果需要KMR集群持久运行，或者需要使用HDFS持久存储数据，请确保关闭该选项。**该选项在集群创建完成后不可修改。 |
| **集群释放保护** | 集群保护可确保KMR集群中的云主机实例不会因为意外事故或者错误而被释放。如果集群中包含的数据位于节点实例存储中，而您又必须在这些实例释放前予以恢复，那么这种保护尤其有用。该选项默认开启。该选项**不会影响“集群自动释放”功能** |
| **日志归集** | 日志归集功能可以把集群和作业的日志统一存放在KS3的指定目录中，便于管理和持久保存。该选项默认关闭，开启该选项后需要选择日志在KS3上的存放目录，或在弹出的对话框中新建目录 |
| **日志路径** |您可以键入或浏览用于存储 KMR 日志的KS3 存储桶（bucket），例如 ks3://myemrbucket/logs，也可以让KMR为您生成一个KS3 路径。如果键入的文件夹名称在存储桶中不存在，系统将为您创建该文件夹。<br>各种集群服务和作业的日志在KS3上对应的路径结构，请参考 [KMR日志归集路径](kmrri_zhi_gui_ji_lu_jing.md) |

　　2.配置集群节点

![基本信息2](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/jbxx2.png)

| 字段 | 操作 |
| -- | -- |
| **用户配额** | 开通KMR服务时，会为每个账户分配一个资源配额，如果账户中使用的集群资源超过了该配额，则无法创建集群。如有特殊需求，请联系您的客户经理 |
| **主节点** | 主要用于集群管理，并将计算程序和原始数据集分配到核心实例。此外，它还会跟踪每个计算作业的执行状态，监控实例的运行状况。KMR主节点与Hadoop系统的主节点相对应。一个KMR集群只有一个主节点。 |
| **核心节点** | 主要用于执行各项集群计算作业，同时作为hadoop分布式文件系统的数据节点存储数据。KMR核心节点与Hadoop系统的slave节点相对应。一个KMR集群可以有2至多个核心节点 |
| **任务节点** | 只用于执行各项集群计算作业,不作为分布式文件系统(HDFS)的数据存储节点，一个KMR集群可以有0至多个任务节点 |
| **节点配置** | 可根据实际的业务需求选择集群节点数量和类型，详见 [KMR产品定价与选购](chan_pin_ding_jia_yu_xuan_gou.md) |

　　3.选择集群的软件配置

![基本信息3](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/jbxx3.png)

| 字段 | 操作 |
| -- | -- |
| **平台版本选择** | 选择创建KMR集群所用的平台版本，选择不同版本可提供不同的集群基础配置 |
| **安装应用** | 选择KMR集群中需要安装的Hadoop周边生态应用。*注意，在集群创建完成后这些选项无法更改*|
| **自定义参数** | 您可以通过此功能来自定义各类集群应用的参数配置（如core-site,hadoop-env等）,文本输入框中每一行都可以定义一个参数，注意（KMR不会对参数或者或者配置文件的正确性进行检查），自定义参数的格式为：<br>classification=<*配置文件名*>,properties=[<*配置项*>=<*值*>]<br>例如：<br>classification=mapred-site,properties=[mapred.tasktracker.map.tasks.maximum=4]<br>目前KMR支持以下配置文件的自定义参数（自定义参数时不需要输入文件扩展名）：<br>"core-site.xml"; "hdfs-site.xml"; "mapred-site.xml"; "yarn-site.xml"; "capacity-scheduler.xml"; "hadoop-env.sh"; "httpfs-env.sh"; "mapred-env.sh"; "yarn-env.sh";"log4j.properties"; "hive-env.sh"; "hive-site.xml"; "hive-exec-log4j.properties"; "hive-log4j.properties"; "spark-env.sh"; "spark-defaults.conf"; "log4j.properties"; "httpfs-site.xml" ;|

<h3 name="an_quan_yu_fang_wen" id="an_quan_yu_fang_wen">2.安全与访问</h3>



---



　　1.设置集群网络

　　KMR服务依赖VPC（虚拟专有网络）以及子网、EndPoint等组件，在创建KMR集群时，会创建默认VPC和相关组件。如需创建自定义VPC，请点击“创建VPC”,参考金山云VPC产品相关文档，或者咨询技术支持。
  
  ![安全与访问1](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/aqyfw1.png)
  
| 字段 | 操作 |
| -- | -- |
| **VPC网络** | 您可以使用默认VPC来创建KMR集群，也可以选择自定义VPC |
| **KEC子网** | KEC子网是VPC中用于管理云主机的网络单元，您可以使用默认KEC子网，也可以选择自定义子网。如果使用自定义VPC，请确认VPC中已创建可用的KEC子网 |
| **EndPoint** | EndPoint可以在您的VPC和其他KSC服务之间创建私有连接，使用KMR服务必须指定EndPoint。 如果使用自定义VPC，请确认VPC中已创建可用的EndPoint|

　　2.设置集群管理信息

![安全与访问2](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/aqyfw2.png)

| 字段 | 操作 |
| -- | -- |
| **绑定密钥** | 如果需要通过SSH访问集群，需要为集群绑定SSH密钥，请参阅[SSH连接指南](sshlian_jie_zhi_nan.md) |
| **绑定EIP** | EIP是绑定在集群Master节点上的公网IP地址，主要用于集群的远程管理和作业提交，带宽为1Mbps，暂时无法调节。绑定EIP将产生少量额外的集群使用费。 |


<h3 name="tian_jia_zuo_ye" id="tian_jia_zuo_ye">3.添加作业</h3>


---


　　1.设置引导操作

　　自定义引导操作是一个可选的高级选项，可以在集群启动时执行软件安装和环境准备等自定义操作，大多数情况下无需配置。
  
  ![添加作业1S](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/tjzy1.png)
  
| 字段 | 操作 |
| -- | -- |
| **引导脚本** | 加入引导脚本可以在集群启动时执行软件安装和环境准备等自定义操作，最多可定义5个顺序执行的引导操作。如使用KS3存储它们，该路径值的形式应该是：<br>ks3://BucketName/path/MaperExecutable |
| **参数** | 通过输入参数来自定义引导脚本参数配置 |
| **执行节点** |勾选执行引导操作的节点，有主节点、核心节点和任务节点三种节点可选|
| **添加引导操作** |完成输入引导脚本地址、配置参数和选择执行节点后，点击“添加引导操作“，新增的脚本就会按照添加时间顺序显示在下方|
| **删除脚本** | 您可以点击“删除脚本”超链接，就会删除对应的脚本|

　　2.设置作业信息

![添加作业2](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/tjzy2.png)

| 字段 | 操作 |
| -- | -- |
| **添加作业** | 作业是提交到集群中的一个工作单元，一个作业可能包含一个或多个分布式计算任务。 您可以对一个集群提交多达256个作业。请参阅 [作业创建指南](zuo_ye_chuang_jian_zhi_nan.md) |
| **添加示例作业** | 我们为每种作业预置了一个示例，您可以参考示例来创建新的示例。注意：示例作业使用了公共的KS3存储目录作为数据源，该目录是只读的，创建自定义作业时，请修改成自有的KS3路径 |
| **编辑** | 您可以通过“编辑”超链接，修改已经添加的作业 |
| **删除** | 您可以通过“删除”超链接，删除已经添加的作业 |


<h3 name="que_ren_ding_dan" id="que_ren_ding_dan">4.确认订单</h3>


---


　　订单确认页面，该页面会根据集群的配置估算出KMR费用，点击“确认提交”后开始创建集群
  
  ![订单确认](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/ddqr.png)





