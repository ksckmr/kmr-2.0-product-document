## 作业操作请求

[**1. ListSteps**](#ListSteps)

[**2. DescribeStep**](#DescribeStep)

[**3. AddSteps**](#AddSteps)

<h3 name="ListSteps" id="ListSteps">1.ListSteps</h3>


---




* **功能描述**

　　列出指定集群的作业状态信息，允许您基于特定的条件对这些信息进行筛选；例如，基于作业状态筛选。每次调用默认返回100个作业，每次最多返回100个，同时会返回一个Marker来对多次ListSteps请求调用进行分页跟踪。
 
* **请求参数**

　　关于所有操作使用的通用参数信息，请参考[通用请求](tong_yong_qing_qiu.md) "公共参数"部分
  
　　**ClusterId**
  
　　　　需要查询的集群ID。<br>
　　　　类型：String<br>
　　　　是否必须：是
    
　　**StepIds**
  
　　　　需要列出的作业ID，用于过滤条件。<br>
　　　　类型：Sting列表<br>
　　　　是否必须：否

　　**StepStates.member.N**
  
　　　　需要列出的集群状态。<br>
　　　　类型：String列表<br>
　　　　可选值：PENDING | RUNNING | COMPLETED | CANCELLED | FAILED | INTERRUPTED | TRANSFERINGLOG <br>
　　　　是否必须：否
    
　　**Marker**
  
　　　　分页标识。<br>
　　　　类型：String<br>
　　　　是否必须：否
    
* **返回参数**

　　返回结果包含以下字段：
  
　　**Steps**
  
　　　　满足请求中给出的过滤条件的作业列表。<br>
　　　　类型：Step列表 （Step）
    
　　**Marker**
  
　　　　用于获取下一页结果集的分页标识。<br>
　　　　类型：String

* **错误信息**

　　关于所有操作使用的通用错误信息，参考[通用请求](tong_yong_qing_qiu.md) "通用错误信息"部分

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
X-Action: ListSteps
X-Version: 2016-05-20
{
    "StepStates": ["RUNNING", "PENDING"]
}
```


　　**返回样例**
  
```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: xxx
{
    "Marker": null,
    "Steps": [
        {
            "Status": {
                "State": "RUNNING"
            },
            "HadoopJarStep": {
                "Args": [
                    "-input",
                    "ks3://yourbucket/input",
                    "-output",
                    "ks3://yourbucket/output",
                    "-mapper",
                    "ks3://yourbucket/mapper.py",
                    "-reducer"
                    "ks3://yourbucket/reducer.py",
                    "-numMapTasks",
                    "1",
                    "-numReduceTasks",
                    "1",
                    "-args",
                    ""
                ],
                "Jar": "ks3://kmr/libs/hadoop-streaming.jar",
                "Properties": {}
            },
            "DurationMins": 2,
            "Name": "streaming-type-job"
            "ActionOnFailure": "CONTINUE",
            "StepType": "MapReduce",
            "Id": "56964e88c-cb6e-4592-be97-53a5e2a2bfde",
            "CreatedAt": "2016-01-08T12:10:07"
        }
    ]
}
```

<h3 name="DescribeStep" id="DescribeStep">2.DescribeStep</h3>


---


* **功能描述**

　　查询指定集群中一个指定作业的详细信息
 
* **请求参数**

　　关于所有操作使用的通用参数信息，请参考[通用请求](tong_yong_qing_qiu.md) "公共参数"部分
  
　　**ClusterId**
  
　　　　需要查询的集群ID。<br>
　　　　类型：String<br>
　　　　是否必须：是
    
　　**StepId**
  
　　　　需要列出的作业ID<br>
　　　　类型：Sting<br>
　　　　是否必须：是

    
* **返回参数**

　　返回结果包含以下字段：
  
　　**Step**
  
　　　　需要查询作业的详细信息。<br>
　　　　类型：Step （Step）
    
* **错误信息**

　　关于所有操作使用的通用错误信息，参考[通用请求](tong_yong_qing_qiu.md) "通用错误信息"部分

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
X-Action: DescribeStep
X-Version: 2016-05-20
{
    "ClusterId": "366bb23b-ef63-494d-acb8-3d26d6375da9",
    "StepId": "56964e88c-cb6e-4592-be97-53a5e2a2bfde"
}
```


　　**返回样例**
  
```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 2
{
    "Step": {
            "Status": {
                "State": "RUNNING"
            },
           "HadoopJarStep": {
                "Args": [
                    "-input",
                    "ks3://yourbucket/input",
                    "-output",
                    "ks3://yourbucket/output",
                    "-mapper",
                    "ks3://yourbucket/mapper.py",
                    "-reducer"
                    "ks3://yourbucket/reducer.py",
                    "-numMapTasks",
                    "1",
                    "-numReduceTasks",
                    "1",
                    "-args",
                    ""
                ],
                "Jar": "ks3://kmr/libs/hadoop-streaming.jar",
                "Properties": {}
            },
            "Name": "streaming-type-job"
            "ActionOnFailure": "CONTINUE",
            "Id": "56964e88c-cb6e-4592-be97-53a5e2a2bfde"
    }
}
```
<h3 name="AddSteps" id="AddSteps">3.AddSteps</h3>


---



* **功能描述**

　　向指定集群批量添加作业。您需要指定集群ID以及相应的作业参数。支持MapReduce、MapReduce.Streming、Pig、Hive、Spark 共5种类型作业。
 
* **请求参数**

　　关于所有操作使用的通用参数信息，请参考[通用请求](tong_yong_qing_qiu.md) "公共参数"部分
  
　　**ClusterId**
  
　　　　需要添加作业的目标集群ID。<br>
　　　　类型：String<br>
　　　　是否必须：是
    
　　**Steps.member.N**
  
　　　　需要添加的自定义作业列表。<br>
　　　　类型：StepConfig 列表 （StepConfig）<br>
　　　　是否必须：是　
    
* **返回参数**

　　返回结果包含以下字段：
  
　　**StepIds**
  
　　　　添加成功的作业ID列表。<br>
　　　　类型：String列表

* **错误信息**

　　关于所有操作使用的通用错误信息，参考[通用请求](tong_yong_qing_qiu.md) "通用错误信息"部分

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
X-Action: AddSteps
X-Version: 2016-05-20
{
    "JobFlowId": "366bb23b-ef63-494d-acb8-3d26d6375da9",
    "Steps": [
        {
"HadoopJarStep": {
                "Args": [
                    "-input",
                    "ks3://yourbucket/input",
                    "-output",
                    "ks3://yourbucket/output",
                    "-mapper",
                    "ks3://yourbucket/mapper.py",
                    "-reducer"
                    "ks3://yourbucket/reducer.py",
                    "-numMapTasks",
                    "1",
                    "-numReduceTasks",
                    "1",
                    "-args",
                    ""],
                "Jar": "ks3://kmr/libs/hadoop-streaming.jar",
                "Properties": {}
            },
            "ActionOnFailure": "CONTINUE",
            "Name": "streaming-type-job"
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
    "StepIds": [
         "56964e88c-cb6e-4592-be97-53a5e2a2bfde"
      ]
}
```




