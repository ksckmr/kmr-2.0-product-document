## 数据类型

 　　KMR API使用了多种自定义数据类型，本章节将对这些数据类型做详细介绍
   
   
[**1. ClusterConfig**](#ClusterConfig)

[**2. ClusterStatus**](#ClusterStatus)

[**3. StepConfig**](#StepConfig)

[**4. Step**](#Step)

[**5. HadoopJarStepConfig**](#HadoopJarStepConfig)
        
[**6. StepStatus**](#StepStatus)

[**7. ClusterSummary**](#ClusterSummary)

[**8. InstanceGroup**](#InstanceGroup)

[**9. InstanceGroupStatus**](#InstanceGroupStatus)

[**10. Instance**](#Instance)

[**11. InstanceStatus**](#InstanceStatus)

[**12. InstanceGroupConfig**](#InstanceGroupConfig)

[**13. Configuration**](#Configuration)

[**14. BootstrapAction**](#BootstrapAction)
        
[**15. ScriptBootstrapAction**](#ScriptBootstrapAction)
   
<h3 name="ClusterConfig" id="ClusterConfig">1.ClusterConfig</h3>


---



　　**Applications**
  
　　　　集群安装的应用列表。<br>
　　　　类型：String列表<br>
　　　　可选值: 可选值为“hadoop”，“hive”，“pig”与“spark”，区分大小写。任何集群都会默认会带上“hadoop”<br>
　　　　是否必须：否
    
　　**AutoTerminate**
  
　　　　集群在运行完作业后是否自动释放。<br>
　　　　类型：Boolean <br>
　　　　是否必须：否
    
　　**DistributionVersion**
  
　　　　集群选用的Hadoop发行版本信息。现阶段均为“kmr-1.0.0”。<br>
　　　　类型：String<br>
　　　　是否必须：否
    
　　**Id**
  
　　　　集群ID。<br>
　　　　类型：String<br>
　　　　是否必须：否
    
　　**InstanceAttributes**
  
　　　　集群主机的参数，现阶段为空。<br>
　　　　类型：String列表<br>
　　　　是否必须：否
    
　　**LogUri**
  
　　　　日志归集的KS3路径。<br>
　　　　类型：String<br>
　　　　是否必须：否
    
　　**MasterPublicIP**
  
　　　　如果集群创建Enable EIP，则为公网IP地址，否则为空。<br>
　　　　类型：String<br>
　　　　是否必须：否
    
　**　Name**
 
　　　　集群名称。<br>
　　　　类型：String<br>
　　　　是否必须：否
    
　　**NormalizedInstanceMins**
  
　　　　集群运行时间，从实例创建成功到集群释放，以分钟为单位。<br>
　　　　类型：Integer<br>
　　　　是否必须：否
    
　　**ServiceRole**
  
　　　　集群的IAM角色，现阶段金山云IAM还未正式完成，取得的值均为Null。<br>
　　　　类型：String<br>
　　　　是否必须：否
    
　　**Status**
  
　　　　集群的IAM角色，现阶段金山云IAM还未正式完成，取得的值均为Null。<br>
　　　　类型：ClusterStatus  （ClusterStatus）<br>
　　　　是否必须：否
    
　　**TerminationProtected**
  
　　　　集群是否启用释放保护锁。<br>
　　　　类型：Boolean<br>
　　　　是否必须：否

　　**VpcDomainId**
  
　　　　集群所属的虚拟专有网络（VPC）信息。<br>
　　　　类型：String <br>
　　　　是否必须：否

　　**VpcSubnetId**
  
　　　　集群所属的虚拟专有网络（VPC）子网信息。<br>
　　　　类型：String <br>
　　　　是否必须：否

　　**VpcEndpointId**

　　　　集群所属的虚拟专有网络（VPC）的Endpoint子网信息，用于创建KMR部署使用的相关网络资源比如内网LB。<br>
　　　　类型：String <br>
　　　　是否必须：否
    
　　**Configurations**
  
　　　　集群配置信息<br>
　　　　类型：Configuration列表（Configuration）<br>
　　　　是否必须：否
    
　　**BootstrapActions**
  
　　　　集群引导操作列表<br>
　　　　类型：BootstrapAction列表(BootstrapAction)<br>
　　　　是否必须：否
    
<h3 name="ClusterStatus" id="ClusterStatus">2.ClusterStatus</h3>    


---



　　**State**
  
　　　　集群状态。<br>
　　　　类型：String<br>
　　　　可选值：STARTING | RUNNING | TERMINATING | TERMINATED | TERMINATED_WITH_ERRORS<br>
　　　　是否必须：否
    
    
<h3 name="StepConfig" id="StepConfig">3.StepConfig</h3>    


---    
    
　　**ActionOnFailure**
  
　　　　作业失败策略。<br>
　　　　类型：String<br>
　　　　可选值:  TERMINATE_JOB_FLOW | TERMINATE_CLUSTER | CANCEL_AND_WAIT | CONTINUE<br>
　　　　是否必须：否
    
　　**HadoopJarStep**
  
　　　　配置作业使用的jar file。<br>
　　　　类型：HadoopJarStepConfig（HadoopJarStepConfig）<br>
　　　　是否必须：是
    
　　**Name**
  
　　　　作业名称。<br>
　　　　类型：String<br>
　　　　长度限制：0-256<br>
　　　　是否必须：是
    
　　**Type**
  
　　　　作业类型。<br>
　　　　类型：String<br>
　　　　可选值：MapReduce | MapReduce.Streming | Pig | Hive | Spark<br>
　　　　是否必须：是
    
<h3 name="Step" id="Step">4.Step</h3>     

---



　　**ActionOnFailure**
  
　　　　作业失败策略。<br>
　　　　类型：String<br>
　　　　可选值:  TERMINATE_JOB_FLOW | TERMINATE_CLUSTER | CANCEL_AND_WAIT | CONTINUE<br>
　　　　是否必须：否
    
　　**HadoopJarStep**
  
　　　　配置作业使用的jar file。<br>
　　　　类型：HadoopJarStepConfig （HadoopJarStepConfig）<br>
　　　　是否必须：否
    
　　**Name**
  
　　　　作业名称。<br>
　　　　类型：String<br>
　　　　长度限制：0-256<br>
　　　　是否必须：否
 
　　**Type**
  
　　　　作业类型。<br>
　　　　类型：String<br>
　　　　可选值：MapReduce、MapReduce.Streming、Pig、Hive、Spark<br>
　　　　是否必须：是
    
　　**Id**
  
　　　　作业ID。<br>
　　　　类型：String<br>
　　　　是否必须：否
    
　　**Status **
  
　　　　作业状态。<br>
　　　　类型：StepStatus  （StepStatus）<br>
　　　　是否必须：否
    
 <h3 name="HadoopJarStepConfig" id="HadoopJarStepConfig">5.HadoopJarStepConfig</h3>     

---   
   

　　**Args**
  
　　　　指定命令行列表传递给jar file的main函数。<br>
　　　　类型：String列表<br>
　　　　是否必须：否
    
　　**Jar**
  
　　　　指定作业的jar file路径。<br>
　　　　类型：String<br>
　　　　是否必须：是
    
　　**MainClass**
  
　　　　指定jave file中main classs名称。如果没有指定，jar file需要在manifest文件中指定。<br>
　　　　类型：String<br>
　　　　是否必须：否
    
　　**Properties**
  
　　　为作业运行指定key-value列表，你可以在你的主函数中使用这些key-value。<br>
　　　类型：KeyValue 列表<br>
　　　是否必须：否
   
 
<h3 name="StepStatus" id="StepStatus">6.StepStatus</h3>

---     
  

　　**State**
  
　　　　作业运行状态。<br>
　　　　类型：String<br>
　　　　可选值：PENDING | RUNNING | COMPLETED | CANCELLED | FAILED | INTERRUPTED | TRANSFERINGLOG<br> 
　　　　是否必须：否## ClusterSummary

　　**Id**
  
　　　　集群的唯一标识符，通常为UUID格式<br>
　　　　类型：String<br>
　　　　是否必须：否
    
　　**Name**
  
　　　　集群名称<br>
　　　　类型：String<br>
　　　　是否必须：否
    
　　**NormalizedInstanceMins**
  
　　　　集群运行的分钟数。如果集群已经结束，则计时断为创建时间至释放时间；如果集群尚未结束，则为创建时间至现在的分钟数。本时间只是对集群运行时间的预估，并不反应实际记费时间。<br>
　　　　类型：Integer<br>
　　　　是否必须：否
    
　　**Status**
  
　　　　集群当前的状态信息<br>
　　　　类型：ClusterStatus<br>
　　　　是否必须：否
 
  <h3 name="ClusterSummary" id="ClusterSummary">7.ClusterSummary</h3> 


---
  

　　**Id**
  
　　　　集群的唯一标识符，通常为UUID格式<br>
　　　　类型：String<br>
　　　　是否必须：否
    
　　**Name**
  
　　　　集群名称<br>
　　　　类型：String<br>
　　　　是否必须：否
    
　　**NormalizedInstanceMins**
  
　　　　集群运行的分钟数。如果集群已经结束，则计时断为创建时间至释放时间；如果集群尚未结束，则为创建时间至现在的分钟数。本时间只是对集群运行时间的预估，并不反应实际记费时间。<br>
　　　　类型：Integer<br>
　　　　是否必须：否
    
　　**Status**
  
　　　　集群当前的状态信息<br>
　　　　类型：ClusterStatus<br>
　　　　是否必须：否 
   <h3 name="InstanceGroup" id="InstanceGroup">8.InstanceGroup</h3> 


---



　　**Id**
  
　　　　实例组Id<br>
　　　　类型：String<br>
　　　　是否必须：否
    
　　**Name**
  
　　　　实例组名<br>
　　　　类型：String<br>
　　　　是否必须：否
    
　　**InstanceGroupType**
  
　　　　实例组类型<br>
　　　　类型：String<br>
　　　　是否必须：否<br>
　　　　合法值：MASTER | CORE | TASK
    
　　**InstanceType**
  
　　　　实例组中实例的配置类别（flavor信息）<br>
　　　　类型：String<br>
　　　　合法值：kmr.general | kmr.memory | kmr.storage | kmr.compute | kmr.general.2x | kmr.memory.2x | kmr.storage.2x | kmr.compute.2x<br>
　　　　是否必须：否
    
　　**InstanceCount**
  
　　　　实例组中实例个数<br>
　　　　类型：Integer<br>
　　　　是否必须：否
    
　　**Status**
  
　　　　实例组状态<br>
　　　　类型：InstanceGroupStatus  （InstanceGroupStatus）<br>
　　　　是否必须：否
    
　　**Configurations**
  
　　　　实例组配置信息，可以针对每个实例组单独设置配置项<br>
　　　　类型：Configuration列表（Configuration）<br>
　　　　是否必须：否
    
　　**ServiceRoles.Member.N**  
  
　　　　实例组角色列表，如"NameNode", "ResourceManager", "HiveServer"等<br>
　　　　类型：String列表<br>
　　　　是否必须：否 
    
    
  <h3 name="InstanceGroupStatus" id="InstanceGroupStatus">9.InstanceGroupStatus</h3> 

---
 

　　**State**
  
　　　　实例组状态<br>
　　　　类型：String<br>
　　　　是否必须：否<br>
　　　　合法值：PROVISIONING | RUNNING | RESIZING | TERMINATING | TERMINATED | ARRESTING
    
 <h3 name="Instance" id="Instance">10.Instance</h3> 

---    

　　**Id**
  
　　　　实例标识<br>
　　　　类型：String<br>
　　　　是否必须：是
    
　　**PrivateIpAddress**
  
　　　　实例的私有ip地址<br>
　　　　类型：String<br>
　　　　是否必须：是
    
　　**PublicIpAddress**
  
　　　　实例的公网ip地址<br>
　　　　类型：String<br>
　　　　是否必须：否
    
　　**Status**
  
　　　　实例状态<br>
　　　　类型：InstanceStatus  （InstanceStatus）<br>
　　　　是否必须：否
    
  <h3 name="InstanceStatus" id="InstanceStatus">11.InstanceStatus</h3> 

---
   

　　**State**
  
　　　　实例状态信息<br>
　　　　类型：String<br>
　　　　是否必须：否<br>
　　　　合法值：PROVISIONING | RUNNING | RESIZING | TERMINATED
    
   <h3 name="InstanceGroupConfig" id="InstanceGroupConfig">12.InstanceGroupConfig</h3> 

---  


　　**InstanceGroupType**
  
　　　　实例组类型<br>
　　　　类型：String<br>
　　　　是否必须：是<br>
　　　　合法值：MASTER、CORE、TASK
    
　　**InstanceType**
  
　　　　实例组中实例的配置类别（flavor信息）<br>
　　　　类型：String<br>
　　　　合法值：kmr.general | kmr.memory | kmr.storage | kmr.compute | kmr.general.2x | kmr.memory.2x | kmr.storage.2x | kmr.compute.2x<br>
　　　　是否必须：是
    
　　**InstanceCount**
  
　　　　实例组中实例个数<br>
　　　　类型：Integer<br>
　　　　是否必须：是
  
　　**ServiceRoles.Member.N**  
  
　　　　实例组角色列表，如"NameNode", "ResourceManager", "HiveServer"等<br>
　　　　类型：String列表<br>
　　　　是否必须：否   
    
   <h3 name="Configuration" id="Configuration">13.Configuration</h3> 

---  
  

　　所创建集群的配置信息。
  
　　**Classification**
  
　　　　配置信息类别<br>
　　　　类型：String<br>
　　　　是否必须：否<br>
　　　　可选值：
    
|Classification|	FileName|
|:|:|
|core-site|	core-site.xml|
|hdfs-site |	hdfs-site.xml|
|mapred-site|	mapred-site.xml|
|yarn-site	|yarn-site.xml|
|capacity-scheduler|	capacity-scheduler.xml|
|hadoop-env	|hadoop-env.sh|
|httpfs-env.sh|	httpfs-env.sh|
|mapred-env|	mapred-env.sh|
|yarn-env	|yarn-env.sh|
|hadoop-log4j	|log4j.properties|
|hive-env	|hive-env.sh|
|hive-site|	hive-site.xml|
|hive-exec-log4j|	hive-exec-log4j.properties|
|hive-log4j	|hive-log4j.properties|
|spark-env|	spark-env.sh|
|spark-defaults|	spark-defaults.conf|
|spark-log4j|	log4j.properties|
|httpfs-site|	httpfs-site.xml|

　　**Properties**
  
　　　　配置信息属性和值的集合<br>
　　　　Type：```map<string,string>　```<br>　
　　　是否必须：否
       
       
　　**Configurations**
  
　　　　Configuration列表<br>
　　　　类型：Configuration列表<br>
　　　　是否必须：否
    
　　Configuration类型数据示例：


```
{
    "Configurations": [
        {
           "Classification":"yarn-env",
           "Configurations": [
              {
                 "Classification":"export",
                 "Properties":{
                      "YARN_NODEMANAGER_OPTS":" -Xmx2049m"
                 }
               }
           ]
        },
        {
           "Classification":"mapred-site",
           "Properties":{
               "mapred.tasktracker.map.tasks.maximum":"5"
           }
        }
    ]
}
```

 <h3 name="BootstrapAction" id="BootstrapAction">14.BootstrapAction</h3> 



---



　　**Name**

　　　　引导操作名字　<br>
　　　　类型：string<br>
　　　　是否必须：是
    
　　**NodeGroups**
  
　　　　引导操作运行的实例组类型<br>
　　　　类型：string列表<br>
　　　　合法值：MASTER | CORE | TASK<br>
　　　　是否必须：否，如果不填默认在所有节点上都运行
    
　　**ScriptBootstrapAction**
  
　　　　引导操作脚本配置<br>
　　　　类型：ScriptBootstrapAction <br>
　　　　是否必须：是
    
    
    
<h3 name="ScriptBootstrapAction" id="ScriptBootstrapAction">15.ScriptBootstrapAction</h3> 



---    
  

　　**Path**
  
　　　　引导操作脚本位置<br>
　　　　类型：string<br>
　　　　是否必须：是
    
　　**Args**
  
　　　　引导操作参数<br>
　　　　类型：string列表<br>
　　　　是否必须：否
	