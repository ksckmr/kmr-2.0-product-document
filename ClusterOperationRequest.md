## 集群操作请求

[**1. ListClusters**](#ListClusters)

[**2. DescribeCluster**](#DescribeCluster)

[**3. LaunchCluster**](#LaunchCluster)

[**4. TerminateClusters**](#TerminateClusters)

[**5. SetTerminationProtection**](#SetTerminationProtection)

[**6. ListInstanceGroups**](#ListInstanceGroups)

[**7. AddInstanceGroups**](#AddInstanceGroups)

[**8. ModifyInstanceGroups**](#ModifyInstanceGroups)

[**9. ListInstances**](#ListInstances)

[**10. ListDistributions**](#ListDistributions)


<h3 name="ListClusters" id="ListClusters">1.ListClusters</h3>


---


* **功能描述**

　　列出当前账户可见的所有KMR集群状态信息，允许您基于特定的条件对这些信息进行筛选；例如，基于集群创建日期和时间来筛选。每次调用默认返回100个集群，每次最多返回100个，同时会返回一个Marker来对多次ListClusters请求调用进行分页跟踪。
  
* **请求参数**
 
　　关于所有操作使用的通用参数信息，请参考通用请求 "[公共参数](GeneralRequest.md#gong_gong_can_shu)"部分
  
　　**ClusterStates.member.N**
  
　　　　需要列出的集群状态。<br>
　　　　类型：String列表<br>
　　　　可选值：STARTING | RUNNING | RESIZING | TRANSFERINGLOG | TERMINATED | TERMINATED_WITH_ERRORS<br>
　　　　是否必须：否
  
　　**CreatedAfter**
  
　　　　列出在某个日期和时间之后创建的集群。<br>
　　　　类型：DateTime<br>
　　　　是否必须：否
  
　　**CreatedBefore**
  
　　　　列出在某个日期和时间之前创建的集群。<br>
　　　　类型：DateTime<br>
　　　　是否必须：否
  
　　**Marker**
  
　　　　分页标识。<br>
　　　　类型：String<br>
　　　　是否必须：否
  
* **返回参数**

　　返回结果包含以下字段：
  
　　**Clusters**
  
　　　　当前账户满足请求中给出的过滤条件的集群列表<br>
　　　　类型：ClusterSummary列表 [ClusterSummary](DataType.md#ClusterSummary)
    
　　**Marker**
  
　　　　用于获取下一页结果集的分页标识<br>
　　　　类型：String
    
* **错误信息**

　　关于所有操作使用的通用错误信息，参考通用请求 "[通用错误信息](GeneralRequest.md#tong_yong_cuo_wu_xin_xi)"部分

  
　　**InternalServerError**
  
　　　　当KMR服务出现内部错误时出现该错误信息类型<br>
　　　　HTTP状态码：500
   
　　**BadRequest**
  
　　　　当用户输入信息有误时出现该错误信息<br>
　　　　HTTP状态码：400

* **样例**

　　**请求样例**
  
```
POST / HTTP/1.1
Content-Type: application/json
X-Action: ListClusters
X-Version: 2016-05-20
{
   "ClusterStates": ["RUNNING", "TERMINATED"]
   "CreatedAfter": "2016-01-08T19:00:00"
}
```

　　**返回样例**
  
```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: xxx
{
    "Marker": "offset=15 & limit=5",
    "Clusters": [
        {
            "Status": {
                "State": "RUNNING"
            },
            "NormalizedInstanceMins": 14,
            "Id": "0b875523-9e95-454a-8fff-f9e592303d95",
            "Name": "test-cluster-ops-03"
        },
        {
            "Status": {
                "State": "RUNNING"
            },
            "NormalizedInstanceMins": 15,
            "Id": "26e6d8af-18e2-49b6-b7d1-040dfb170b3b",
            "Name": "test-cluster-ops-01"
        }
    ]
}
```


<h3 name="DescribeCluster" id="DescribeCluster">2.DescribeCluster</h3>


---



* **功能描述**

　　列出某个当前用户可见的集群详细信息，包括状态，硬件，软件设置等。
 
* **请求参数**

　　关于所有操作使用的通用参数信息，请参考通用请求 "[公共参数](GeneralRequest.md#gong_gong_can_shu)"部分
  
　　**ClusterId**
  
　　　　需要列出实例组信息的集群标识。<br>
　　　　类型：String<br>
　　　　是否必须：是
    　　
* **返回参数**

　　返回结果包含以下字段：
  
　　**Cluster**
  
　　　　请求中集群的详细信息<br>
　　　　类型：ClusterConfig  [ClusterConfig](DataType.md#ClusterConfig) 

* **错误信息**

　　关于所有操作使用的通用错误信息，参考通用请求 "[通用错误信息](tong_yong_qing_qiu.md#tong_yong_cuo_wu_xin_xi)"部分


　　**InternalServerError**
  
　　　　当KMR服务出现内部错误时出现该错误信息类型<br>
　　　　HTTP状态码：500
    
　　**BadRequest**
  
　　　　当用户输入信息有误时出现该错误信息<br>
　　　　HTTP状态码：400

* **样例**

　　**请求样例**

```
POST / HTTP/1.1
Content-Type: application/json
X-Action: DescribeCluster
X-Version: 2016-05-20
{
    "ClusterId": "ffd8270a-48e0-4f68-8a35-0f8562302ad6"
}
```


　　**返回样例**
  
```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: xxx
{
  "InstanceAttributes": [],
  "Name": "lxk-quota-test-0",
  "ServiceRole": null,
  "TerminationProtected": false,
  "HadoopVersion": "hadoop 2.6.0",
  "LogUri": "ks3://kmrhkbj/lxk-log",
  "AutoTerminate": false,
  "Status": {
    "State": "RUNNING"
  },
  "MasterPublicDnsName": "120.168.113.60",
  "NormalizedInstanceMins": 1333,
  "Applications": [
    "hadoop"
  ],
  "Id": "ffd8270a-48e0-4f68-8a35-0f8562302ad6"
}
```


<h3 name="LaunchCluster" id="LaunchCluster">3.LaunchCluster</h3>


---




* **功能描述**

　　创建集群操作，操作成功后会创建一个KMR集群，如果参数中带有作业配置，则集群创建成功后将自动运行指定的作业。如果AutoTerminate设置为True，则作业运行完毕后集群不会释放，反之集群会在所有作业完成后自动释放；关于参数中TerminationProtected的设置及原理介绍请参见[SetTerminationProtection](#SetTerminationProtection)部分。
 
* **请求参数**

　　关于所有操作使用的通用参数信息，请参考通用请求 "[公共参数](GeneralRequest.md#gong_gong_can_shu)"部分
  
　　**Distribution**
  
　　　　Hadoop发行版本说明。支持“kmr-1.0.0”与“kmr-2.0.0”。　<br>
　　　　类型：String<br>
　　　　默认：“kmr-2.0.0”<br>
　　　　是否必须：否
    
　　**Applications.member.N**
  
　　　　安装应用列表。可选值为“hadoop”，“hive”，“hbase”，“spark”，“storm”，“kafka”等，区分大小写。如果不填则默认为“hadoop”。<br>
　　　　类型：String列表<br>
　　　　是否必须：否
    
　　**InstanceGroups.member.N**
  
　　　　集群里虚机的配置和数目信息。<br>
　　　　类型：InstanceGroupConfig列表   [InstanceGroupConfig](DataType.md#InstanceGroupConfig)<br>
　　　　是否必须：是
   
　　**IsTransient**
  
　　　　是否为临时集群。<br>
　　　　类型：Boolean <br>
　　　　默认：False      
　　　　是否必须：否
    
　　**ChargeType**
  
　　　　集群计费类型：包年包月"Monthly"，按需付费"Minutely"，免费试用"FreeTrial"。<br/>
　　　　包年包月"Monthly"：包月集群，有到期时间。<br/> 
　　　　按需付费"Minutely"：按分钟计费，按月结算。   
　　　　免费试用"FreeTrial"：用户有试用quota时能创建出免费试用集群。<br> 
　　　　类型：String <br/>
　　　　默认："Minutely"      
　　　　是否必须：否
   
　　**PurchaseTime**
  
　　　　集群购买时长，单位月。“包年包月”必须要选择，有效值1-36；其余计费类无需此项内容（系统按0处理）。<br>
　　　　类型：Integer<br>
　　　　是否必须：否   
   
　　**MetaDatabaseUri**
  
　　　　元数据管理的数据库信息。<br>
　　　　元数据主要指集群监控元数据，Hive的元数据管理等。当用户选择集群外的RDS或者自建MySql来管理元数据时需要填写。<br>
　　　　类型：String <br>
　　　　格式：mysql://{username}:{password}@{hostname}:{port} <br> 
　　　　是否必须：否   
   
　　**TerminationProtected**
  
　　　　集群是否启用释放保护锁。<br>
　　　　类型：Boolean <br>
　　　　默认：True <br> 
　　　　是否必须：否
   
　　**VpcDomainId**
  
　　　　集群所属的虚拟专有网络（VPC）信息。<br>
　　　　类型：String <br>
　　　　是否必须：是

　　**VpcSubnetId**
  
　　　　集群所属的虚拟专有网络（VPC）子网信息。<br>
　　　　类型：String <br>
　　　　是否必须：是

　　**VpcEndpointId**

　　　　集群所属的虚拟专有网络（VPC）的Endpoint子网信息，用于创建KMR部署使用的相关网络资源比如内网LB。<br>
　　　　类型：String <br>
　　　　是否必须：是
   
　　**LogUri**
  
　　　　日志输出的KS3路径，格式为：“KS3://bucket/object_key”。如果不填则日志不会输出到KS3。<br>
　　　　类型：String<br>
　　　　是否必须：否
    
　　**Name**
  
　　　　集群的名称。仅支持大小写字母、数字、减号和下划线。<br>
　　　　类型：String<br>
　　　　是否必须：是
    
　　**Steps.member.N**
  
　　　　自定义需要运行的作业列表。(常驻集群暂不支持)<br>
　　　　类型：StepConfig列表 [StepConfig](DataType.md#StepConfig)<br>
　　　　是否必须：否
    
　　**EnableEIP**
  
　　　　是否启用eip信息，如果设置为True，则集群的Master节点会被分配一个外网ip，默认为False。<br>
　　　　类型：String<br>
　　　　是否必须：否
    
　　**Configurations.member.N**
  
　　　　所创建集群的配置信息。<br>
　　　　类型：Configuration列表 [Configuration](DataType.md#Configuration)<br>
　　　　是否必须：否
    
　　**BootstrapActions.member.N**
  
　　　　集群引导操作列表<br>
　　　　类型：BootstrapAction列表 [BootstrapAction](DataType.md#BootstrapAction)<br>
　　　　是否必须：否
    　　
* **返回参数**

　　返回结果包含以下字段：
  
　　**ClusterId**
  
　　　　创建成功的集群ID<br>
　　　　类型：String 

* **错误信息**

　　关于所有操作使用的通用错误信息，参考通用请求"[通用错误信息](GeneralRequest.md#tong_yong_cuo_wu_xin_xi)"部分


　　**InternalServerError**
  
　　　　当KMR服务出现内部错误时出现该错误信息类型<br>
　　　　HTTP状态码：500
    
　　**BadRequest**
  
　　　　当用户输入信息有误时出现该错误信息<br>
　　　　HTTP状态码：400

* **样例**

　　**请求样例**

```
POST / HTTP/1.1
Content-Type: application/json
X-Action: LaunchCluter
X-Version: 2016-05-20
{
  "Name": "api-test",
  "AutoTerminate": False，
  "InstanceGroups" : [
      {
        "InstanceType" : "kmr.general",
        "InstanceCount" : 1,
        "InstanceGroupType" : "MASTER"
      },
      {
        "InstanceType" : "kmr.general",
        "InstanceCount" : 2,
        "InstanceGroupType" : "CORE"
      }
  ],
  "Steps": [
        {
            "ActionOnFailure": "CONTINUE",
            "Name": "java_test",
            "HadoopJarStep": {
                "Args": [
                    "ks3://kmr-bj-test/input",
                    "ks3://kmr-bj-test/output"
                ],
                "Type": "MapReduce",
                "Jar": "ks3://kmr-bj-test/jobtest/job.jar",
                "MainClass": "org.apache.hadoop.examples.WordCount"
            }
        }
    ]
}
```


　　**返回样例**
  
```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: xxx
{
  "ClusterId": "ffd8270a-48e0-4f68-8a35-0f8562302ad6"
}
```

<h3 name="TerminateClusters" id="TerminateClusters">4.TerminateClusters</h3>



---




* **功能描述**

　　释放指定的一个或者多个集群。当集群释放时，尚未完成的作业将被取消，集群所使用的云主机都将被释放，但如果集群设置了日志归集功能（创建集群时给出了LogUri），则所有日志都会被完整的上传至KS3。
  
　　请求允许释放的最大集群数量为10。集群释放是一个异步操作，请求会立即返回，根据集群的配置，可能需要5-20分钟才能完全释放掉集群所有的资源，比如云主机实例。
 
* **请求参数**

　　关于所有操作使用的通用参数信息，请参考通用请求 "[公共参数](GeneralRequest.md#gong_gong_can_shu)"部分
  
　　**ClusterIds.member.N**
  
　　　　需要释放的集群ID列表。<br>
　　　　类型：String列表<br>
　　　　长度限制：最小0个，最大10个<br>
　　　　是否必须：是
    
* **返回参数**

　　返回结果不包含任何字段

* **错误信息**

　　关于所有操作使用的通用错误信息，参考通用请求 "[通用错误信息](GeneralRequest.md#tong_yong_cuo_wu_xin_xi)"部分


　　**InternalServerError**
  
　　　　当KMR服务出现内部错误时出现该错误信息类型<br>
　　　　HTTP状态码：500
    
　　**BadRequest**
  
　　　　当用户输入信息有误时出现该错误信息<br>
　　　　HTTP状态码：400

* **样例**

　　**请求样例**

```
POST / HTTP/1.1
Content-Type: application/json
X-Action: TerminateClusters
X-Version: 2016-05-20
{
    "ClusterIds": ["26e6d8af-18e2-49b6-b7d1-040dfb170b3b"]
}
```


　　**返回样例**
  
```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 2
{}
```


<h3 name="SetTerminationProtection" id="SetTerminationProtection">5.SetTerminationProtection</h3>


---



* **功能描述**

　　设置集群释放保护锁。保护集群和云主机不会因为用户干预（控制台、API调用等）而被释放。
  
　　如果集群设置了自动释放功能，而且所有作业运行完毕，则集群将不受释放保护功能的影响，可以自动释放。
  
　　如果想释放开启了释放保护锁的集群，则必须要先调通此API，将释放保护设置为false，然后释放集群。
 
* **请求参数**

　　关于所有操作使用的通用参数信息，请参考通用请求 "[公共参数](GeneralRequest.md#gong_gong_can_shu)"部分
  
　　**ClusterIds.member.N**
  
　　　　需要释放的集群ID列表。<br>
　　　　类型：String列表<br>
　　　　长度限制：最小0个，最大10个<br>
　　　　是否必须：是
    
　　**TerminationProtected**
    
　　　　指示是否开启释放保护功能的布尔值。<br>
　　　　类型：Boolean<br>
　　　　是否必须：是
    
* **返回参数**

　　返回结果不包含任何字段

* **错误信息**

　　关于所有操作使用的通用错误信息，参考通用请求 "[通用错误信息](GeneralRequest.md#tong_yong_cuo_wu_xin_xi)"部分


　　**InternalServerError**
  
　　　　当KMR服务出现内部错误时出现该错误信息类型<br>
　　　　HTTP状态码：500
    
　　**BadRequest**
  
　　　　当用户输入信息有误时出现该错误信息<br>
　　　　HTTP状态码：400

* **样例**

　　**请求样例**

```
POST / HTTP/1.1
Content-Type: application/json
X-Action: SetTerminationProtection
X-Version: 2016-05-20
{
    "ClusterIds": ["26e6d8af-18e2-49b6-b7d1-040dfb170b3b"],
    "TerminationProtected": true
}
```


　　**返回样例**
  
```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 2
{}
```


<h3 name="ListInstanceGroups" id="ListInstanceGroups">6.ListInstanceGroups</h3>


---


* **功能描述**

　　提供了集群中每个实例组的详细信息。
 
* **请求参数**

　　关于所有操作使用的通用参数信息，请参考通用请求 "[公共参数](GeneralRequest.md#gong_gong_can_shu)"部分
  
　　**ClusterId**
  
　　　　需要列出实例组信息的集群标识。<br>
　　　　类型：String<br>
　　　　是否必须：是
    
　　**Marker**
    
　　　　分页标识。<br>
　　　　类型：String<br>
　　　　是否必须：否
    
* **返回参数**

　　返回结果包含以下字段：
  
　　**InstanceGroups**
  
　　　　基于给定过滤条件返回指定集群的实例组列表<br>
　　　　类型：InstanceGroup 列表  [InstanceGroup](DataType.md#InstanceGroup)

　　**Marker**
  
　　　　用于获取下一页结果集的分页标识<br>
　　　　类型：String

* **错误信息**

　　关于所有操作使用的通用错误信息，参考通用请求 "[通用错误信息](GeneralRequest.md#tong_yong_cuo_wu_xin_xi)"部分


　　**InternalServerError**
  
　　　　当KMR服务出现内部错误时出现该错误信息类型<br>
　　　　HTTP状态码：500
    
　　**BadRequest**
  
　　　　当用户输入信息有误时出现该错误信息<br>
　　　　HTTP状态码：400

* **样例**

　　**请求样例**

```
POST / HTTP/1.1
Content-Type: application/json
X-Action: ListInstanceGroups
X-Version: 2016-05-20

{
    "ClusterId": "e1b637b5-210d-45b3-bc16-0338b3c8cf8e"
}
```


　　**返回样例**
  
```
HTTP/1.1 200 OK
  Content-Type:application/json
Content-Length: 462
Date: Thu, 07 Jan 2016 02:57:57 GMT
{
  "Marker": null,
  "InstanceGroups": [
    {
      "Status": {
        "State": " RUNNING "
      },
      "InstanceCount": 2,
      "Name": "gn-e51f56af-CORE",
      "InstanceGroupType": "CORE",
      "InstanceType": "kmr.compute",
      "Id": "e1b637b5-210d-45b3-bc16-0338b3c8cf8e-gn-e51f56af-CORE"
    },
    {
      "Status": {
        "State": " RUNNING "
      },
      "InstanceCount": 1,
      "Name": "gn-e51f56af-MASTER",
      "InstanceGroupType": "MASTER",
      "InstanceType": "kmr.compute",
      "Id": "e1b637b5-210d-45b3-bc16-0338b3c8cf8e-gn-e51f56af-MASTER"
    }
  ]
}
```


<h3 name="AddInstanceGroups" id="AddInstanceGroups">7.AddInstanceGroups</h3>


---



* **功能描述**

　　AddInstanceGroups用于添加实例组，目前仅支持添加一个任务实例组。一个集群中最多只能有一个任务实例组。
 
* **请求参数**

　　关于所有操作使用的通用参数信息，请参考通用请求 "[公共参数](GeneralRequest.md#gong_gong_can_shu)"部分
  
　　**ClusterId**
  
　　　　需要添加实例组信息的集群标识。<br>
　　　　类型：String<br>
　　　　是否必须：是
    
　　**InstanceGroups**
  
　　　　需要添加的InstanceGroup配置列表<br>
　　　　类型：InstanceGroupConfig列表  [InstanceGroupConfig](DataType.md#InstanceGroupConfig)<br>
　　　　是否必须：是
    　　
* **返回参数**

　　返回结果包含以下字段：
  
　　**InstanceGroupIds**
  
　　　　添加成功的实例组ID列表。<br>
　　　　类型：String列表
    
* **错误信息**

　　关于所有操作使用的通用错误信息，参考通用请求 "[通用错误信息](GeneralRequest.md#tong_yong_cuo_wu_xin_xi)"部分


　　**InternalServerError**
  
　　　　当KMR服务出现内部错误时出现该错误信息类型<br>
　　　　HTTP状态码：500
    
　　**BadRequest**
  
　　　　当用户输入信息有误时出现该错误信息<br>
　　　　HTTP状态码：400

* **样例**

　　**请求样例**

```
POST / HTTP/1.1
Content-Type: application/json
X-Action: AddInstanceGroups
X-Version: 2016-05-20
{
    "ClusterId": "e1b637b5-210d-45b3-bc16-0338b3c8cf8e",
    "InstanceGroups": [
        {
            "InstanceGroupType": "TASK",
	            "InstanceCount": 1,
	            "InstanceType": "kmr.compute"
        }
    ]
}
```


　　**返回样例**
  
```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 2
{ "InstanceGroupIds": [
    "bb26aa5a-4032-4b0d-9037-82c6b715c241"
  ] 
}
```


<h3 name="ModifyInstanceGroups" id="ModifyInstanceGroups">8.ModifyInstanceGroups</h3>


---



* **功能描述**

　　ModifyInstanceGroups用于修改集群实例组的实例个数或实例组配置信息，如果修改了实例组个数,集群就会进行相应的扩容或缩容。
 
* **请求参数**

　　关于所有操作使用的通用参数信息，请参考通用请求 "[公共参数](GeneralRequest.md#gong_gong_can_shu)"部分
  
　　**ClusterId**
  
　　　　需要列出实例组信息的集群标识。<br>
　　　　类型：String<br>
　　　　是否必须：是
    
　　**InstanceGroups**
    
　　　　InstanceGroup类型列表。<br>
　　　　类型：InstanceGroupConfig列表  [InstanceGroupConfig](DataType.md#InstanceGroupConfig)<br>
　　　　是否必须：是
    
* **返回参数**

　　返回结果不包含任何字段

* **错误信息**

　　关于所有操作使用的通用错误信息，参考通用请求 "[通用错误信息](GeneralRequest.md#tong_yong_cuo_wu_xin_xi)"部分


　　**InternalServerError**
  
　　　　当KMR服务出现内部错误时出现该错误信息类型<br>
　　　　HTTP状态码：500
    
　　**BadRequest**
  
　　　　当用户输入信息有误时出现该错误信息<br>
　　　　HTTP状态码：400

* **样例**

　　**请求样例**

```
POST / HTTP/1.1
Content-Type: application/json
X-Action: ModifyInstanceGroups
X-Version: 2016-05-20
{
    "ClusterId": "e1b637b5-210d-45b3-bc16-0338b3c8cf8e",
    "InstanceGroups": [
        {
            "InstanceGroupId": "e1b637b5-210d-45b3-bc16-0338b3c8cf8e-gn-e51f56af-CORE",
            "InstanceCount": 3,
            "InstanceIdsToTerminate": []
        }
    ]
}
```


　　**返回样例**
  
```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 2
{}
```

<h3 name="ListInstances" id="ListInstances">9.ListInstances</h3>



---




* **功能描述**

　　提供了KMR集群中的实例信息，这些实例是您在创建集群时由 KMR服务帮您申请的虚拟机实例。您可以根据实例组标识、实例组角色选择您想查看的实例，每次调用可以返回最多50个实例，但可以返回一个marker来跟踪跨多个ListInstances簇列表分页调用。
 
* **请求参数**

　　关于所有操作使用的通用参数信息，请参考[通用请求](GeneralRequest.md) "公共参数"部分
  
　　**ClusterId**
  
　　　　需要列出实例组信息的集群标识。<br>
　　　　类型：String<br>
　　　　是否必须：是
    
　　**InstanceGroupId**
  
　　　　需要列出实例的实例组ID，如果不提供默认值，列出所有实例组的实例<br>
　　　　类型：String<br>
　　　　是否必须：否
    
　　**InstanceGroupTypes**
  
　　　　需要列出的实例的实例组角色，合法的实例组角色有: MASTER、CORE、TASK，如果不提供默认提供所有角色的实例组中的实例<br>
　　　　类型：String列表<br>
　　　　是否必须：否
    
　　**Marker**
  
　　　　分页标识。<br>
　　　　类型：String<br>
　　　　是否必须：否
    
* **返回参数**

　　返回结果包含以下字段：
  
　　**Instances**
  
　　　　Instance结果<br>
　　　　类型：Instance列表 [Instance](DataType.md#Instance)
    
　　**Marker**
  
　　　　用于获取下一页结果集的分页标识<br>
　　　　类型：String

* **错误信息**

　　关于所有操作使用的通用错误信息，参考通用请求 "[通用错误信息](GeneralRequest.md#tong_yong_cuo_wu_xin_xi)"部分


　　**InternalServerError**
  
　　　　当KMR服务出现内部错误时出现该错误信息类型<br>
　　　　HTTP状态码：500
    
　　**BadRequest**
  
　　　　当用户输入信息有误时出现该错误信息<br>
　　　　HTTP状态码：400

* **样例**

　　**请求样例**

```
GET / HTTP/1.1
POST / HTTP/1.1
Content-Type: application/json
X-Action: ListInstances
X-Version: 2016-05-20
{
    "ClusterId": "e1b637b5-210d-45b3-bc16-0338b3c8cf8e",
    "InstanceGroupId": "",
    "InstanceGroupTypes": ["MASTER"]
}
```


　　**返回样例**
  
```
HTTP/1.1 200 OK
  Content-Type: application/json
Content-Length: 186
Date: Thu, 07 Jan 2016 02:57:57 GMT
{
  "Marker": null,
  "Instances": [
    {
      "Status": {
        "State": "RUNNING"
      },
      "Id": "079d2b1f-cb1f-4365-acbb-c1b3f7424831",
      "PrivateIpAddress": "10.168.113.134",
      "PublicIpAddress": "10.168.113.134"
    }
  ]
}
```


<h3 name="ListDistributions" id="ListDistributions">10.ListDistributions</h3>



---




* **功能描述**

　　提供了KMR集群可用的发行版信息，以及发行版里面支持的应用信息。
 
* **请求参数**

　　关于所有操作使用的通用参数信息，请参考通用请求 "[公共参数](GeneralRequest.md#gong_gong_can_shu)"部分

    
* **返回参数**

　　返回结果包含以下字段：
  
　　**Distributions**
  
　　　　发行版列表<br>
　　　　类型：Distribution列表 [Distribution](DataType.md#Distribution)

* **错误信息**

　　关于所有操作使用的通用错误信息，参考通用请求 "[通用错误信息](GeneralRequest.md#tong_yong_cuo_wu_xin_xi)"部分


　　**InternalServerError**
  
　　　　当KMR服务出现内部错误时出现该错误信息类型<br>
　　　　HTTP状态码：500
    
　　**BadRequest**
  
　　　　当用户输入信息有误时出现该错误信息<br>
　　　　HTTP状态码：400

* **样例**

　　**请求样例**

```
GET / HTTP/1.1
POST / HTTP/1.1
Content-Type: application/json
X-Action: ListDistributions
X-Version: 2016-05-20
{
}
```


　　**返回样例**
  
```
HTTP/1.1 200 OK
  Content-Type: application/json
Content-Length: 328
Date: Thu, 07 Jan 2016 02:57:57 GMT
{
  "Distributions": 
    [
      {
        "Release": "1.0.0", 
        "Applications": 
          [
            {
              "Release": "2.6.0", 
              "Required": true, 
              "Name": "hadoop"
            }, 
            {
              "Release": "0.14.0", 
              "Required": true, 
              "Name": "hive"
            }, 
            {
              "Release": "0.10.0", 
              "Required": true, 
              "Name": "pig"
            }, 
            {
              "Release": "1.5.2", 
              "Required": false, 
              "Name": "spark"
            }
          ], 
        "Vendor": "KSYUN", 
        "Name": "kmr-1.0.0"
      }
    ]
}
```





