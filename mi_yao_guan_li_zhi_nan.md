## SSH密钥管理


　　用户除了通过控制台来管理集群和作业外，也可以通过SSH来访问管理集群，而KMR集群仅支持SSH 密钥认证方式，因此密钥管理模块用来管理通过SSH方式访问集群的密钥。
  
　　在使用SSH连接集群之前，请确保集群已经绑定了EIP，绑定EIP的过程请参考[集群操作](ji_qun_cao_zuo_zhi_nan)的集群详情部分。

* [创建密钥](#chuang_jian_mi_yao)

* [密钥列表](#mi_yao_lie_biao)

* [使用SSH访问集群](#fang_wen_ji_qun)

<h3 name="chuang_jian_mi_yao" id="chuang_jian_mi_yao">创建密钥</h3>


---

1.使用密钥生成工具生成SSH-2 RSA密钥，保存好私钥和公钥

![生成密钥](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/tjmy1.png)

　　windows用户可以使用PuTTYgen.exe工具<br>
    　　http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html
  
　　Linux 用户可以通过 ssh-keygen –t rsa 来生成，默认生成在~/.ssh/目录下，公钥文件是~/.ssh/id_rsa.pub，用户使用ssh-keygen时也可以自己指定公钥目录。


　　2.打开KMR控制台，选择“集群密钥”，点击“创建密钥”按钮，进入创建密钥界面。
　　
  ![创建密钥](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/mygl1.png)
  
  | 字段 | 操作 |
| -- | -- |
| **名称** | 您可以为密钥输入描述性名称 |
| **描述** | 输入对该密钥的描述语言 |
| **公钥** | 把第一步生成的公钥文件内容粘贴到这里，格式形如“ssh-rsaAAAAB3NzaC1yc2EAAAABJQAAAQEAxljLUF//ygzu1Dy/sArs1hpoN……” |
  


<h3 name="mi_yao_lie_biao" id="mi_yao_lie_biao">密钥列表</h3>


---


　　密钥创建完成后可以在密钥列表中查看密钥的基本信息，并对密钥进行简单操作，密钥列表会根据创建时间来排序

![密钥列表](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/mygl2.png)

　　**创建密钥：**您可以创建密钥，详情参考[创建密钥](#chuang_jian_mi_yao)
  
　　**加载到集群：**您可以在左侧勾选一个或多个密钥，然后选择“加载到集群”将密钥加载到集群，加载到的集群也可以选择多个,将密钥加载到集群之后，即可通过SSH访问集群
  
　　**删除：**您可以在左侧勾选一个或多个计划，然后选择“删除密钥”来删除密钥
  
　　**刷新：**您可以刷新密钥列表
  
　　**查看公钥：**您可以查看公钥详细内容
  
  
<h3 name="fang_wen_ji_qun" id="fang_wen_ji_qun">使用SSH访问集群</h3>


---

  
 　　 1.选择创建密钥时创建好的密钥，点击“加载到集群”按钮，把密钥加载到集群

　　2.导入创建密钥时产生的私钥

![导入私钥](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/fwjq2.png)

　　windows用户可以使用PuTTY.exe工具<br>
　　http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html
  
　　3.指定IP和端口连接KMR主节点，连接到集群，登陆账户名是root。
　　　
　　用此方法获得IP端口：打开KMR控制台，进入集群详情，展开主节点的详细信息，您可以通过公网（如果绑定EIP）IP地址访问集群，或者同一VPC内的云主机通过内网IP地址访问集群。

![绑定EIP](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/fwjq1.png)

![连接到集群](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/fwjq3.png)

　　4.主节点和核心节点已配置了SSH互信，可以在控制台查看核心节点的IP地址，直接从主节点登陆到各个核心节点。
  