## SSH连接指南


　　除了可以通过控制台来执行KMR集群和作业的操作外，您也可以通过SSH来访问集群，执行管理工作或者监控集群状态。

　　在开始连接之前，请确保集群已经绑定了EIP，并且Master节点已经设置了正确的防火墙规则（默认阻止所有公网访问），请参考金山云官方文档 [防火墙配置](http://www.ksyun.com/doc/art/id/376e)
  
  
* [为集群添加SSH密钥](#tian_jia_ssh_mi_yao)
  
* [使用SSH访问集群](#ssh_fang_wen_ji_qun)

<h3 name="tian_jia_ssh_mi_yao" id="tian_jia_ssh_mi_yao">为集群添加SSH密钥</h3>


---



　　KMR集群仅支持SSH 密钥认证方式，在使用SSH之前，您需要为集群添加SSH密钥。

　　1.使用密钥生成工具生成SSH-2 RSA密钥，保存好私钥和公钥

![生成密钥](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/tjmy1.png)

　　windows用户可以使用PuTTYgen.exe工具<br>
    　　http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html
  
　　Linux 用户可以通过 ssh-keygen –t rsa 来生成，默认生成在~/.ssh/目录下，公钥文件是~/.ssh/id_rsa.pub，用户使用ssh-keygen时也可以自己指定公钥目录。


　　2.打开KMR控制台，选择“集群密钥”，点击“创建密钥”按钮，把第1步生成的公钥文件内容粘贴到对话框，并点击“创建”

![创建密钥](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/tjmy2.png)

　　3.选择刚刚创建好的密钥，点击“加载到集群”按钮，把密钥加载到集群，您可以把密钥同时加载到多个集群。至此，密钥加载完成。
![加载到集群](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/tjmy3.png)
  
<h3 name="ssh_fang_wen_ji_qun" id="ssh_fang_wen_ji_qun">使用SSH访问集群</h3>


---
  

　　1.打开KMR控制台，进入集群详情，展开主节点的详细信息，您可以通过公网（如果绑定EIP）IP地址访问集群，或者同一VPC内的云主机通过内网IP地址访问集群。

![绑定EIP](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/fwjq1.png)

　　2.导入[为集群添加SSH密钥](#tian_jia_ssh_mi_yao) 中产生的私钥

![导入私钥](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/fwjq2.png)

　　windows用户可以使用PuTTY.exe工具<br>
　　http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html
  
　　3.指定IP和端口连接KMR主节点，连接到集群，登陆账户名是root。

![连接到集群](http://kmr-bj.ks3-cn-beijing.ksyun.com/doc_pic/fwjq3.png)

　　4.主节点和核心节点已配置了SSH互信，可以在控制台查看核心节点的IP地址，直接从主节点登陆到各个核心节点。
  