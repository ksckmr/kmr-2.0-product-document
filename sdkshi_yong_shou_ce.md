## SDK使用手册


## 1 概述
KMR是金山云公司提供的大数据服务平台，用户使用KMR可以创建自己的hadoop集群并运行hadoop、hive、pig、spark任务。此SDK基于KMR API构建，适用于Java 5及以上版本。
## 2 环境准备
配置Java 5以上开发环境；
下载KMR SDK For Java https://github.com/kmr-sdk/kmr-java-sdk 
在kmr-java-sdk目录下，运行mvn clean install；
使用sdk时，添加Maven依赖

       <dependency>
            <groupId>com.kingsoft.services.kmr</groupId>
            <artifactId>kmr-java-sdk</artifactId>
            <version>0.0.1-SNAPSHOT</version>
       </dependency>
sdk使用样例请参考：https://github.com/kmr-sdk/kmr-java-sample
## 3 初始化
### 3.1 获取密钥
1、开通KMR服务
2、获取AK/SK
进入控制台: http://ks3.ksyun.com/console.html#/ ，点击页面左侧“帐号设置”，获取AccessKey、SecretKey.
### 3.2 初始化客户端
1、同步式客户端
通过同步式客户端调用KMR服务时，客户端会一直等待直到服务返回结果。

    KSCCredentials credential = new BasicKSCCredentials(
	    "<您的AccessKeyID>", "<您的AccessKeySecret>");
    KSCMapReduceClient kmrClient = new KSCMapReduceClient(
	    "<endpoint>", credential);

说明：目前可用endpoint为

　`•　北京地区：kmr.cn-beijing-6.api.ksyun.com`
 
　`•　上海地区：kmr.cn-shanghai-2.api.ksyun.com`


2、异步式客户端
异步式客户端通过Java Future模式实现。异步式客户端调用KMR API时，客户端可以立即返回，去做其他事情，需要时再获取服务返回结果。

    KSCCredentials credential = new BasicKSCCredentials(
	    "<您的AccessKeyID>", "<您的AccessKeySecret>");
    KSCMapReduceAsyncClient kmrAsyncClient = new    KSCMapReduceAsyncClient("<endpoint>", credential);

## 4 快速入门
说明：以下所有request中的参数，仅作为示例，用户使用时需按照自己的需求配置。
### 4.1 创建cluster
1、创建request

    Map cl_env_conf = new HashMap<String, String>();
    cl_env_conf.put("YARN_NODEMANAGER_OPTS", "-Xmx2048m");

    Map cl_xml_conf = new HashMap<String, String>();
    cl_xml_conf.put(
        "mapred.tasktracker.map.tasks.maximum","4");

    RunJobFlowRequest request = new RunJobFlowRequest()
       .withName("<clusterName>")
       .withLogUri("<log在KS3上的存放路径>")
       .withApplications("hadoop","spark","hive","pig")
       .withInstances(new JobFlowInstancesConfig()
            .withKeepJobFlowAliveWhenNoSteps(true)
            .withInstanceGroups(
	            new InstanceGroupConfig()
		            .withInstanceRole("MASTER")
	                .withInstanceCount(1)
	                .withInstanceType("kmr.general"),
                new InstanceGroupConfig()
				    .withInstanceType("kmr.general")
                    .withInstanceCount(5)
                    .withInstanceRole("CORE")
               )
             )
        .withConfigurations(
            new Configuration()
                .withClassification("yarn-env")
                .withConfigurations(
                    new Configuration()
                        .withClassification("export")
                        .withProperties(cl_env_conf)
                ),
            new Configuration()
               .withClassification("mapred-site")
               .withProperties(cl_xml_conf)
        );
request必需参数：

> withName：JobFlow名称<br/>
 withInstances：创建cluster的节点配置<br/>
 withInstanceGroups：节点组配置<br/>
 withInstanceRole: 节点类型，Master／Core<br/>
withInstanceCount: 节点数量<br/>
withInstanceType: 节点配置类型<br/>

说明：节点配置类型如下

| type      |  说明  | cpu  |   内存   |硬盘   |
| :-------- | :--------|:--------| :------ |
| kmr.general |一般通用型 |4核| 15GB |400GB
| kmr.compute   | 计算优化型|  8核 |  15GB  | 300GB
| kmr.memory   |  内存优化型| 4核 |  30GB  |400GB
| kmr.storage   |  存储优化型| 4核 |  7.5GB  |2000GB
| kmr.genera.2x   | 内存优化型.2x | 8核 |  30GB  |800GB
| kmr.compute.2x   | 存储优化型.2x | 16核 |  30GB  |600GB
| kmr.memory.2x   | 内存优化型.2x | 8核 |  60GB  |800GB
| kmr.storage.2x   | 存储优化型.2x | 8核 |  15GB  |4000GB


request可选参数：

> withLogUri: log在KS3上的存放路径，省略此选项时不会将日志保存到KS3上。<br/>
withApplications：cluster支持的应用，如hadoop、hive等，默认支持hadoop<br/>
withKeepJobFlowAliveWhenNoSteps: Cluster上没有任务运行时，是否继续保持Cluster Alive，默认为True。<br/>
withTerminationProtected：该项为True，cluster不能直接被关闭。默认为False。创建cluster后可通过调用setTerminationProtection接口来设置该选项。<br/>
withEnableHighAvailability: 是否支持高可用性，默认为False。<br/>
withHadoopVersion：Hadoop版本，默认为hadoop 2.6.0<br/>
withSteps：创建cluster后需要运行的任务，可省略。创建cluster后，可通过调用addJobFlowSteps接口来添加Steps。<br/>
withEnableEip：使节点具备外网IP，以便用户从外网访问节点，默认为False。<br/>
withSshKeyIds：登录cluster节点时用的sshKey，默认为None。<br/>
withConfigurations：集群软件配置项，默认为None。<br/>

Configuration支持的Classification如下：

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

2、同步式客户端调用API

    RunJobFlowResult result = kmrClient.runJobFlow(request);
3、异步式客户端调用API

    Future<RunJobFlowResult> result = kmrAsyncClient.runJobFlowAsync(request);
    ListClustersResult res = result.get();

###    4.2 添加JobFlowSteps
1、创建request
创建普通java hadoop任务：

    StepConfig test_java_step = new StepConfig()
        .withName("test_java_step")
        .withActionOnFailure("CONTINUE")
        .withHadoopJarStep(new HadoopJarStepConfig()
            .withArgs("<输入在KS3上的路径>",
                      "<输出在KS3上的路径>")
            .withJar("<java任务jar包在KS3上的路径>")
            .withMainClass("<MainClass路径>"));

创建hadoop streaming任务：

    StepConfig test_streaming_step = new StepConfig()
        .withName("test_streaming_step")
        .withActionOnFailure("CONTINUE")
        .withHadoopJarStep(new StreamingStep()
             .withInputs("<输入在KS3上的路径>")
             .withOutput("<输出在KS3上的路径>")
             .withMapper( "<mapper在KS3上的路径>")
             .withReducer("<reducer在KS3上的路径>")
             .withNumMapTasks("<maptask数量>")
             .withNumReduceTasks("<reducetask数量>")
             .toHadoopJarStepConfig()
             );

创建pig任务：

    StepConfig test_pig_step = new StepConfig()
        .withName("test_pig_step")
        .withActionOnFailure("CONTINUE")
        .withHadoopJarStep(new PigStep()
             .withScript("<pig任务脚本在KS3上的路径>")
             .withInputs("<输入在KS3上的路径>")
             .withOutput("<输出在KS3上的路径>")
             .withNumMapTasks("<maptask数量>")
             .withNumReduceTasks("<reducetask数量>")
             .toHadoopJarStepConfig());

创建hive任务：

    StepConfig test_hive_step = new StepConfig()
        .withName("test_hive_step")
        .withActionOnFailure("CONTINUE")
        .withHadoopJarStep(new HiveStep()
             .withScript("<hive任务脚本在KS3上的路径>")
             .withInputs("<输入在KS3上的路径>")
             .withOutput("<输出在KS3上的路径>")
             .withNumMapTasks("<maptask数量>")
             .withNumReduceTasks("<reducetask数量>")
             .toHadoopJarStepConfig());

创建spark任务：

    StepConfig test_spark_step = new StepConfig()
        .withName("test_spark_step_2")
        .withActionOnFailure("CONTINUE")
        .withHadoopJarStep(new SparkStep()
             .withSubmitArgs("<spark任务参数列表>")
             .toHadoopJarStepConfig()
             .withArgs("<输入在KS3上的路径>",
                       "<输出在KS3上的路径>")
             .withMainJar("<spark任务jar包在KS3上的路径>")
             .withMainClass("<MainClass路径>")
                    );

创建AddJobFlowStepsRequest：

    AddJobFlowStepsRequest request = 
    new AddJobFlowStepsRequest()
	      .withJobFlowId(clusterId)
	      .withSteps(test_java_step, test_steaming_step, test_hive_step, test_pig_step, test_spark_step);
	      

request必需参数：
> withJobFlowId：添加step的JobFlowId
withSteps：添加的steps

2、同步式客户端调用API

    AddJobFlowStepsResult result = kmrClient.addJobFlowSteps(request);
3、异步式客户端调用API

    Future<AddJobFlowStepsResult> result = kmrAsyncClient.addJobFlowStepsAsync(request);
    AddJobFlowStepsResult res = result.get();

### 4.3  describeCluster
1、创建request

    DescribeClusterRequest request = new DescribeClusterRequest()
                    .withClusterId(clusterId);

2、同步式客户端调用API

    DescribeClusterResult result = kmrClient.describeCluster(request);

3、异步式客户端调用API

    Future<DescribeClusterResult> result = kmrAsyncClient.describeClusterAsync(request);
    DescribeClusterResult res = result.get();

### 4.4 describeStep
1、创建request

    DescribeStepRequest request = new DescribeStepRequest()
                    .withClusterId(clusterId)
                    .withStepId(stepId);

2、同步式客户端调用API

    DescribeStepResult result = kmrClient.describeStep(request);

3、异步式客户端调用API

    Future<DescribeStepResult> result = kmrAsyncClient.describeStepAsync(request);
    DescribeStepResult res = result.get();

### 4.5 listClusters
1、创建request

    ListClustersRequest request = new ListClustersRequest()
                    .withClusterStates("RUNNING")
                    .withCreatedAfter(createAfter)
                    .withCreatedBefore(createBefore);

request可选参数：
> withClusterStates：cluster状态筛选条件。
withCreatedAfter：cluster创建时间筛选条件，晚于该参数指定的时间
withCreatedBefore：cluster创建时间筛选条件，早于该参数指定的时间
withMarker：分页显示参数，从第几个开始显示及每页显示数量，默认为从第1个开始显示，每页显示100个。

说明：createAfter和createBefore格式：`yyyy-mm-dd hh:mm:ss`
cluster状态包含：

| Cluster状态     |     说明 | 
| :-------- | :--------| 
| STARTING    |  启动阶段 | 
| RUNNING    |  运行阶段|
| WAITING    |  等待阶段，等待scaling等|
| RESIZING    |  启动阶段|
| TERMINATING    | 正在关闭 |
| TERMINATED    | 已经关闭 |
| TERMINATED_WITH_ERRORS    | 非正常关闭 |


2、同步式客户端调用API

    ListClustersResult result = kmrClient.listClusters(request);

3、异步式客户端调用API

    Future<ListClustersResult> result = kmrAsyncClient.listClustersAsync(request);
    ListClustersResult res = result.get();

### 4.6 listInstanceGroups
1、创建request

    ListInstanceGroupsRequest request = new ListInstanceGroupsRequest()
                    .withClusterId(clusterId)
                    .withMarker("offset=0 & limit=100");
               
request必需参数：

> withClusterId：需要显示节点组信息的集群Id

request可选参数：
> withMarker：分页显示参数，从第几个开始显示及每页显示数量，默认为从第1个开始显示，每页显示100个。


2、同步式客户端调用API

    ListInstanceGroupsResult result = kmrClient.listInstanceGroups(request);

3、异步式客户端调用API

    Future<ListInstanceGroupsResult> result = kmrAsyncClient.listInstanceGroupsAsync(request);
    ListInstanceGroupsResult res = result.get();

### 4.7 listInstances
1、创建request

    ListInstancesRequest request = new ListInstancesRequest()
                    .withClusterId(clusterId)
                    .withMarker("offset=0 & limit=100")
                    .withInstanceGroupId("<instanceGroupId>")
                    .withInstanceGroupTypes("CORE");
request必需参数：

> withClusterId：需要显示节点信息的集群Id

request可选参数：

> withInstanceGroupId：需要显示节点信息的组Id
> withInstanceGroupTypes：需要显示节点信息的组类型（MASTER／CORE）
> withMarker：分页显示参数，从第几个开始显示及每页显示数量，默认为从第1个开始显示，每页显示100个。

2、同步式客户端调用API

    ListInstancesResult result = kmrClient.listInstances(request);

3、异步式客户端调用API

    Future<ListInstancesResult> result = kmrAsyncClient.listInstancesAsync(request);
    ListInstancesResult res = result.get();

### 4.8 listSteps
1、创建request

    ListStepsRequest request = new ListStepsRequest()
                    .withClusterId(clusterId)
                    .withMarker("offset=0 & limit=100")
                    .withStepIds(stepId)
                    .withStepStates("FAILED");
request必需参数：

> withClusterId：需要显示Step信息的集群Id

request可选参数：

> withStepStates：需要显示Step信息的Step状态筛选条件
> withStepIds：需要显示Step信息的StepId
> withMarker：分页显示参数，从第几个开始显示及每页显示数量，默认为从第1个开始显示，每页显示100个。

Step状态包含：

| Step状态      |     说明 |   
| :-------- | --------:| :------: |
| PENDING    |  等待被执行状态 |
|  RUNNING  |  运行中 |
|  TRANSFERINGLOG  | 传输日志中  |
|  COMPLETED  |  运行完成 |
|  CANCELLED  |  已被取消 |
|  FAILED  |  运行失败 |
|  INTERRUPTED  |　|


2、同步式客户端调用API

     ListStepsResult result = kmrClient.listSteps(request);

3、异步式客户端调用API

    Future<ListStepsResult> result = kmrAsyncClient.listStepsAsync(request);
    ListStepsResult res = result.get();

### 4.9 modifyInstanceGroups
1、创建request

    ModifyInstanceGroupsRequest request = new ModifyInstanceGroupsRequest()
      .withClusterId(clusterId)
      .withInstanceGroups(new InstanceGroupModifyConfig()
           .withInstanceGroupId("<instanceGroupId>")
           .withInstanceCount("<instanceCount>")
           .withInstanceIdsToTerminate("<instanceId>"));

request必需参数：

> withClusterId：需要调整节点组大小的集群Id

request可选参数：

> withInstanceGroups：需要调整的节点组信息
> withInstanceGroupId：需要调整的节点组Id
> withInstanceCount：调整后节点组大小
> withInstanceIdsToTerminate：需要关闭的节点Id列表

2、同步式客户端调用API

    kmrClient.modifyInstanceGroups(request);

3、异步式客户端调用API

    kmrAsyncClient.modifyInstanceGroupsAsync(request);
说明：该API调用无返回值。
### 4.10 setTerminationProtection
1、创建request

    SetTerminationProtectionRequest request = new SetTerminationProtectionRequest()
        .withJobFlowIds(clusterId)
        .withTerminationProtected(terminateProtection);
    
 request必需参数：
 
> withJobFlowIds：需要设置关闭保护的集群Id
> withTerminationProtected：True／False

       
2、同步式客户端调用API

    kmrClient.setTerminationProtection(request);

3、异步式客户端调用API

    kmrAsyncClient.setTerminationProtectionAsync(request);
说明：该API调用无返回值。
### 4.11 terminateJobFlows
1、创建request

    TerminateJobFlowsRequest request = new TerminateJobFlowsRequest()
                    .withJobFlowIds(clusterId);
request必需参数：

> withJobFlowIds：需要关闭的集群Id

2、同步式客户端调用API

    kmrClient.terminateJobFlows(request);

3、异步式客户端调用API

    kmrAsyncClient.terminateJobFlowsAsync(request);
说明：该API调用无返回值。
### 4.12 addInstanceGroups
1、创建request

    AddInstanceGroupsRequest request = new AddInstanceGroupsRequest()
      .withClusterId(clusterId)
      .withInstanceGroups(new InstanceGroupConfig()
                            .withInstanceRole("TASK")
                            .withInstanceCount(1)
                            .withInstanceType("kmr.compute"));

request必需参数：

> withClusterId：需要添加节点组的集群Id
> withInstanceGroups：需要添加的节点组信息


2、同步式客户端调用API

    kmrClient.addInstanceGroups(request);

3、异步式客户端调用API

    kmrAsyncClient.addInstanceGroupsAsync(request);

## 5 异常处理
kmr sdk会抛出KSCServiceException、KSCClientException两类异常。KSCServiceException表示KMR服务内部出现异常；KSCClientException表示连接KMR服务的客户端出现异常。用户使用SDK时，需要对这两类异常进行捕获处理。

    try {
	    ListClustersRequest request = 
        new ListClustersRequest()
                    .withClusterStates("RUNNING");
	    ListClustersResult result 
		    = kmrClient.listClusters(request);

        System.out.println(result.toString());
    } catch (KSCServiceException kse) {
        System.out.println("Caught an KSCServiceException");
        System.out.println("Error Message:" + kse.getMessage());
    } catch (KSCClientException kce) {
        System.out.println("Caught an KSCClientException");
        System.out.println("Error Message:" + kce.getMessage());
    }
