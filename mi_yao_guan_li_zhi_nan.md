## 密钥管理指南


　　用户除了通过控制台来管理集群和作业外，也可以通过SSH来访问管理集群，而KMR集群仅支持SSH 密钥认证方式，因此密钥管理模块用来管理通过SSH方式访问集群的密钥。

* [创建密钥](#chuang_jian_mi_yao)

* [密钥列表](#mi_yao_lie_biao)

<h3 name="chuang_jian_mi_yao" id="chuang_jian_mi_yao">创建密钥</h3>


---



　　打开金山云控制台，选择KMR服务，选择“集群密钥”，点击“创建密钥”，进入创建密钥页面

![创建密钥](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/mygl1.png)

| 字段 | 操作 |
| -- | -- |
| **名称** | 您可以为密钥输入描述性名称 |
| **描述** | 输入对该密钥的描述语言 |
| **公钥** | 输入用密钥生成工具生成的公钥，格式形如“ssh-rsaAAAAB3NzaC1yc2EAAAABJQAAAQEAxljLUF//ygzu1Dy/sArs1hpoN……”详情见 [SSH连接指南](sshlian_jie_zhi_nan.md)中的“为集群添加SSH密钥”部分 |

<h3 name="mi_yao_lie_biao" id="mi_yao_lie_biao">密钥列表</h3>


---


　　密钥创建完成后可以在密钥列表中查看密钥的基本信息，并对密钥进行简单操作，密钥列表会根据创建时间来排序

![密钥列表](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/mygl2.png)

　　**创建密钥：**您可以创建密钥，详情参考[创建密钥](#chuang_jian_mi_yao)
  
　　**加载到集群：**您可以在左侧勾选一个或多个密钥，然后选择“加载到集群”将密钥加载到集群，加载到的集群也可以选择多个
  
　　**删除：**您可以在左侧勾选一个或多个计划，然后选择“删除密钥”来删除密钥
  
　　**刷新：**您可以刷新密钥列表
  
　　**查看公钥：**您可以查看公钥详细内容