## KMR日志归集路径

　　**Master Node**

　　1.resource_manager

　　原始日志位置： /mnt/yarn/logs<br>
　　KS3归集日志位置：ks3://<日志归集路径>/<ClusterID>/resource_manager_log

　　2.name_node

　　原始日志位置： /mnt/log/hadoop/hadoop<br>
　　KS3归集日志位置：ks3://<日志归集路径>/<ClusterID>/namenode_log

　　3.history_server

　　原始日志位置： /opt/hadoop/logs/<br>
　　KS3归集日志位置:  ks3://<日志归集路径>/<ClusterID>/ history_server_log

　　4.history job

　　原始日志位置： /tmp/hadoop-yarn/staging/history/done <br>
　　KS3归集日志位置:  ks3://<日志归集路径>/<ClusterID>/ history_job_log

　　**Core Node**

　　1.data_node

　　原始日志位置： /mnt/hadoop/logs <br>
　　KS3归集日志位置:  ks3://<日志归集路径>/<ClusterID>/ datanode_log

　　2.node_manager

　　原始日志位置： /mnt/yarn/logs <br>
　　KS3归集日志位置:  ks3://<日志归集路径>/<ClusterID>/ node_manager_log

　　3.application log

　　原始日志位置： /mnt/yarn/logs/userlogs <br>
　　KS3归集日志位置:  ks3://<日志归集路径>/<ClusterID>/<JobID>/ application_log
