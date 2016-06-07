# 集群操作指南

![集群操作](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/jqcz.png)
　　KMR集群生命周期包含了初始化，运行，调整，错误，释放等状态，您可根据实际需求对集群执行管理操作。*注意：只有集群在“运行中”状态时才会开始执行作业并开始计费*。
  
 * [创建集群-快速选项](chuang_jian_ji_qun_kuai_su_xuan_xiang.md)

 * [创建集群-高级选项](chuang_jian_ji_qun_gao_ji_xuan_xiang.md)

*  [查看集群列表](#cha_kan_ji_qun_lie_biao)
 
* [集群详情](#ji_qun_xiang_qing)

* [作业详情](#zuo_ye_xiang_qing)



<h3 name="cha_kan_ji_qun_lie_biao" id="cha_kan_ji_qun_lie_biao">查看集群列表</h3>

---

　　集群创建完成后可以在集群列表中查看集群的基本信息，并对集群进行简单操作，集群列表会根据创建时间来排序
  
  ![查看集群列表](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/ckjqlb.png)
  
  
　　**新建集群：**您可以点击“新建集群”使用集群创建向导来创建集群，或者点击“集群模板”，进入进群模板管理页面，通过已有的模板来创建集群。
  
　　**集群密钥：**点击“集群密钥”按钮来管理集群密钥，请参考[密钥管理指南](mi_yao_guan_li_zhi_nan.md)
   
　　**集群模板：**点击“集群模板”按钮来管理集群模板,请参考[集群模板管理指南](ji_qun_mu_ban_guan_li_zhi_nan.md)
   
　　**执行计划：**点击“执行计划”按钮来管理执行计划,请参考[执行计划指南](zhi_xing_ji_hua_zhi_nan.md)
  
　　**释放集群：**您可以通过集群列表末尾的“释放”超链接来释放集群，也可以在左侧勾选多个集群，然后选择“释放集群”来批量释放集群
  
　　**刷新：**刷新集群列表
    
　　**集群筛选：**默认情况下，集群列表不会显示已释放的集群，可以勾选“显示已释放的集群”来显示所有集群，同时可以通过搜索集群名称，快速定位到所找的集群。

　　**集群详情：**单击集群列表末尾的“详情”超链接来进入集群详情页面，请参考查看[集群详情](#ji_qun_xiang_qing)

　　**保存为模板：**您可以将已创建的集群直接保存为模板
  
  
  <h3 name="ji_qun_xiang_qing" id="ji_qun_xiang_qing">集群详情</h3>
  
---


　　集群详情页面列出的集群的基本信息，您可以对一些集群配置进行更改

![集群详情](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/jiqxq.png)

　　**绑定/解绑EIP：**可以通过绑定EIP来获取公网地址访问主节点，如果已绑定EIP，也可以解绑EIP。
  
　　**集群保护：**释放保护功能保障集群不会因为意外错误导致销毁，您可以点击超链接来更改状态。
  
　　**自定义参数：**显示集群自定义参数的配置信息，点击“详情”超链接可以查看具体的参数配置信息
  
　　**集群日志：**点击“下载”超链接，可以下载集群的具体日志信息
  
　　**配置信息：**列出了平台版本、已安装应用和集群节点的硬件配置信息，点击“展开”超链接，可以看到节点ID，状态，IP地址等更多信息，点击“添加”超链接，可以添加任务节点。
  
　　**管理工具：**Hadoop和Spark等应用具有丰富的原生管理工具，点击各个工具链接，能够直接进入管理界面，进行相关管理和查询。用户通过此接口进入管理工具界面，无需使用SSH Tunnel方式进入。管理工具包括ResourceManager、NameNode、JobHistory、Ganglia、Oozie和Spark，请参考[监控指南](jian_kong_zhi_nan.md)
  
　　**绑定SSH密钥：**点击该按钮，可以为集群绑定SSH密钥，请参考[SSH连接指南](sshlian_jie_zhi_nan.md)中的"为集群添加SSH密钥”部分
  
　　**变更集群配置：**点击该按钮，您可以根据需求来增加或者减少核心节点和任务节点的数量。<br>
　　*注意：变更核心节点，尤其是减少核心节点的操作在某些极特殊情况下可能会导致HDFS文件系统数据不可用，请您操作前注意，或咨询技术支持。*

　　**释放集群：**点击该按钮，会弹出释放集群对话框。释放集群将会删除掉所有集群节点、HDFS上存储的数据以及正在运行的作业且无法恢复，KS3上面存储的数据将会保留,请慎重操作。释放集群之前请确认“集群释放保护”选项处于关闭状态
  
  
   <h3 name="zuo_ye_xiang_qing" id="zuo_ye_xiang_qing">作业详情</h3>
  
---

　　点击“作业列表”页签，您可以查看该集群中运行的作业状态，并可以为集群添加新的作业，参考[作业创建指南](zuo_ye_chuang_jian_zhi_nan.md)
  
  ![作业详情](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/zyxq.png)  
  ![作业详情](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/zyxq1.png)
