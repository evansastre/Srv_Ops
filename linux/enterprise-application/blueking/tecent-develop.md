# Tecent develop

## 1.BlueKing basic configuration environment

If use integrated installation, the maximum parititon \(/data\) is selected as the installation path by default.

```text
[root@nginx-1 data]# pwd
/data
[root@nginx-1 data]# ls -lah
total 24K
drwxr-xr-x   6 root root 4.0K May  4 15:26 .
dr-xr-xr-x. 19 root root 4.0K Jan 31  2018 ..
drwxrwxr-x  14 root root 4.0K Sep 11 11:48 bkee  # Tencent/OpenSource Parts安装目录
drwxr-xr-x  12 root root 4.0K Sep 10 21:57 install # 安装所需配置目录
drwxrwxr-x  10 root root 4.0K Sep 11 11:48 src  #Tencent/OpenSource Parts 预编译安装包、安装脚本等

[root@gse-2 bkee]# ls -lh /data/bkee/
total 52K
drwxr-xr-x  3 root  root  4.0K Sep 11 11:48 bin  
drwxr-xr-x  3 root  root  4.0K Sep 21 21:56 cert  
drwxr-xr-x  7 root  root  4.0K Sep 26 15:13 etc  #通用配置目录
drwxr-xr-x 11 30020 30020 4.0K Sep 11 16:40 gse 
drwxr-xr-x  4 root  root  4.0K May 10 14:55 license
drwxrwxrwt 13 root  root  4.0K Sep  9 02:16 logs #通用log目录
drwxr-xr-x  9 30020 30020 4.0K May 30 16:00 open_paas
drwxr-xr-x  5 30020 30020 4.0K Sep  7 11:14 paas_agent
-rwxr-xr-x  1 root  root   761 Mar 27  2018 paas_agent_config.yaml
drwxr-xr-x  5 root  root  4.0K Mar  2  2018 paas_plugins
drwxrwxrwt 13 mysql mysql 4.0K Jun 19 15:53 public #实例目录，包括Tencent组件和开源组件
drwxr-xr-x  4 root  root  4.0K Jun 14 20:23 service
drwxr-xr-x  7 root  root  4.0K Dec 27  2017 zabbix
```

2.每台机器上均有安装gse\_agent，供监控等使用

Gse\_agent目录：/usr/local/ gse/agent/

Gse\_agent log目录：/var/log/gse/

```text
root     30045 0.0  0.0 34948 804 ?        Ss Sep06 0:00 ./gse_agent -f /usr/local/gse/agent/etc/agent.conf
root     30047 0.0  0.0 1885980 12360 ?       Sl Sep06 15:24 ./gse_agent -f /usr/local/gse/agent/etc/agent.conf
```

## 2.PaaS components

基于uwsgi+django搭建的核心平台，负责用户管理，蓝鲸基础界面等功能，其中包括login,console,appengine,esb,paas

安装目录：/data/bkee/open\_paas

配置目录：/data/bkee/etc

运行目录：/data/bkee/.envs + supervisor 守护进程

```text
[root@gse-2 open_paas]# ls -lah
total 976K
drwxr-xr-x  9 30020 30020 4.0K May 30 16:00 .
drwxrwxr-x 15 root  root 4.0K Sep 11 11:48 ..
-rw-r--r--  1 30020 30020  37K May 30 16:00 README.md
-rw-r--r--  1 30020 30020 884K May 30 16:00 README.pdf
-rw-r--r--  1 30020 30020    7 May 30 16:00 VERSION
drwxr-xr-x  4 30020 30020 4.0K Sep 25 18:44 appengine #Django controller
drwxr-xr-x  2 30020 30020 4.0K Sep 25 18:48 bin 
drwxr-xr-x 21 30020 30020 4.0K Aug 29 12:27 console #界面管理中心，包括user_centre等
drwxr-xr-x 11 30020 30020 4.0K Sep 25 18:56 esb #数据中心管道，负责所有消息传送
drwxr-xr-x 12 30020 30020 4.0K Aug 29 12:27 login #用户登录管理，和Lisence模块交互验证
drwxr-xr-x 35 30020 30020 4.0K Sep  6 19:32 paas #协调管理saas app
-rw-r--r--  1 30020 30020 9.7K May 30 16:00 release.md
drwxr-xr-x  5 root root  4.0K Jan 18 2018 support-files
```

## 3.PaaS\_plugins 

PaaS插件，管理log，监控等数据，需要配合使用bkdata



```text
[root@gse-2 paas_plugins]# pwd
/data/bkee/paas_plugins
[root@gse-2 paas_plugins]# ls
log_agent  log_alert log_parser
```

## 4.CMDB

蓝鲸中典型的基于django后端框架并结合mysql/redis/mongo存储搭建的saas app

安装目录

```text
[root@rbtnode2 cmdb]# pwd
/data/bkee/cmdb
[root@rbtnode2 cmdb]# ls -lah
total 48K
drwxr-xr-x  8 30020 30020 4.0K Sep  6 18:03 .
drwxrwxr-x 15 root  root 4.0K Sep 11 11:48 ..
-rw-r--r--  1 30020 30020    7 Aug 22 16:08 VERSION
drwxr-xr-x  4 30020 30020 4.0K Aug 22 16:07 errors
drwxr-xr-x  4 30020 30020 4.0K Aug 22 16:07 language
drwxr-xr-x  2 root root  4.0K Sep 11 18:59 pid
-rw-r--r--  1 30020 30020  10K Aug 22 16:08 release.md
drwxr-xr-x  4 30020 30020 4.0K Aug 22 16:08 server #cmdb启动命令和配置目录
drwxr-xr-x  4 30020 30020 4.0K Jun  4 19:34 support-files
drwxr-xr-x  7 30020 30020 4.0K Aug 22 16:08 web   #django后端资源
[root@rbtnode2 cmdb]# ls -R server/
server/:
bin  conf on_migrate

server/bin:
cmdb_adminserver  cmdb_apiserver cmdb_auditcontroller  cmdb_datacollection cmdb_eventserver cmdb_hostcontroller  cmdb_hostserver cmdb_objectcontroller cmdb_proccontroller cmdb_procserver  cmdb_toposerver cmdb_webserver

server/conf:
apiserver.conf  auditcontroller.conf  datacollection.conf eventserver.conf  host.conf hostcontroller.conf migrate.conf  objectcontroller.conf proc.conf proccontroller.conf  topo.conf webserver.conf
[root@rbtnode2 cmdb]#
[root@rbtnode2 cmdb]# ls -R web/
web/:
css  favicon.ico  fonts img index.html  js svg
```

进程状态

```text
[root@rbtnode2 cmdb]# ps aux|grep cmdb
root     12485 0.0  0.0 9092 664 pts/1    S+ 16:32 0:00 grep --color=auto cmdb
root     17809 0.0  0.0 216828 16052 ?        Ss Sep11 21:14 /opt/py27/bin/python /opt/py27/bin/supervisord -c /data/bkee/etc/supervisor-cmdb-server.conf
root     17838 0.0  0.0 632660 23732 ?        Sl Sep11 14:53 /data/bkee/cmdb/server/bin/cmdb_hostcontroller --addrport=192.168.1.7:31002 --logtostderr=false --log-dir=/data/bkee/logs/cmdb --v=3 --regdiscv=zk.service.consul:2181
root     17839 0.1  0.0 645892 31332 ?        Sl Sep11 25:11 /data/bkee/cmdb/server/bin/cmdb_hostserver --addrport=192.168.1.7:32001 --logtostderr=false --log-dir=/data/bkee/logs/cmdb --v=3 --regdiscv=zk.service.consul:2181
root     17840 0.0  0.0 507476 24776 ?        Sl Sep11 15:10 /data/bkee/cmdb/server/bin/cmdb_toposerver --addrport=192.168.1.7:32002 --logtostderr=false --log-dir=/data/bkee/logs/cmdb --v=3 --regdiscv=zk.service.consul:2181
root     17841 0.1  0.0 637676 28320 ?        Sl Sep11 32:43 /data/bkee/cmdb/server/bin/cmdb_objectcontroller --addrport=192.168.1.7:31001 --logtostderr=false --log-dir=/data/bkee/logs/cmdb --v=3 --regdiscv=zk.service.consul:2181
root     17846 0.0  0.0 567604 17232 ?        Sl Sep11 4:15 /data/bkee/cmdb/server/bin/cmdb_webserver --addrport=192.168.1.7:33083 --logtostderr=false --log-dir=/data/bkee/logs/cmdb --v=3 --regdiscv=zk.service.consul:2181
root     17847 0.0  0.0 564808 21272 ?        Sl Sep11 5:45 /data/bkee/cmdb/server/bin/cmdb_procserver --addrport=192.168.1.7:32003 --logtostderr=false --log-dir=/data/bkee/logs/cmdb --v=3 --regdiscv=zk.service.consul:2181
root     17855 0.0  0.0 767536 17892 ?        Sl Sep11 5:11 /data/bkee/cmdb/server/bin/cmdb_auditcontroller --addrport=192.168.1.7:31004 --logtostderr=false --log-dir=/data/bkee/logs/cmdb --v=3 --regdiscv=zk.service.consul:2181
root     17857 0.1  0.0 658288 31076 ?        Sl Sep11 24:10 /data/bkee/cmdb/server/bin/cmdb_apiserver --addrport=192.168.1.7:33031 --logtostderr=false --log-dir=/data/bkee/logs/cmdb --v=3 --regdiscv=zk.service.consul:2181
root     17861 0.0  0.0 705360 22580 ?        Sl Sep11 6:56 /data/bkee/cmdb/server/bin/cmdb_eventserver --addrport=192.168.1.7:32005 --logtostderr=false --log-dir=/data/bkee/logs/cmdb --v=3 --regdiscv=zk.service.consul:2181
root     17868 0.0  0.0 627416 18152 ?        Sl Sep11 11:10 /data/bkee/cmdb/server/bin/cmdb_datacollection --logtostderr=false --log-dir=/data/bkee/logs/cmdb --v=3 --regdiscv=zk.service.consul:2181
root     17880 0.0  0.0 701536 16432 ?        Sl Sep11 5:08 /data/bkee/cmdb/server/bin/cmdb_adminserver --addrport=192.168.1.7:32004 --config=/data/bkee/cmdb/server/conf/migrate.conf
root     17884 0.0  0.0 571380 18756 ?        Sl Sep11 5:13 /data/bkee/cmdb/server/bin/cmdb_proccontroller --addrport=192.168.1.7:31003 --logtostderr=false --log-dir=/data/bkee/logs/cmdb --v=3 --regdiscv=zk.service.consul:2181
```

## 5.JOB

基于java编写负责任务下发，执行命令等的基础模块

安装目录

```text
[root@rbtnode2 job]# pwd
/data/bkee/job
[root@rbtnode2 job]# ls
README.md  VERSION job  release.md
[root@rbtnode2 job]# ls -R job/
job/:
WEB-INF  bin config  job-exec.war rundata
```

进程状态

```text
root     29636 0.7  2.8 14436624 926548 ?     Sl Sep21 53:06 /data/bkee/service/java/bin/java -Djob.listen.ip=192.168.1.7 -server -Dfile.encoding=UTF-8 -Djava.security.egd=file:/dev/./urandom -Dapp=job -Dbk_home=/data/bkee -Djob_conf=/data/bkee/etc/job.conf -Djob.pc.dir=/data/bkee/job/job/config -Djob.certs.dir=/data/bkee/cert -Djob.log.dir=/data/bkee/logs/job -Dlogging.config=/data/bkee/job/job/config/logback-spring.xml -Djob.web.basedir=/data/bkee/job/job/rundata -XX:ParallelGCThreads=8 -XX:+UseConcMarkSweepGC -XX:MaxGCPauseMillis=800 -XX:+PrintGCDetails -XX:+PrintGCDateStamps -XX:+PrintGCTimeStamps -Xloggc:/data/bkee/logs/job/gc_job.log -classpath /data/bkee/job/job/config:.:/data/bkee/service/java/lib/dt.jar:/data/bkee/service/java/lib/tools.jar -jar /data/bkee/job/job/job-exec.war #使用8008和8443端口进行交互

```

## 6.APP-o/t

管理所有测试/线上环境的saas app，每一个app都是基于django开发，有独立的后端资源，运行在docker中独立的container

安装目录：/data/bkee/paas\_agent

docker数据目录：/data/bkee/public/paas\_agent/docker

paas\_agent和docker log目录：/data/bkee/logs/paas\_agent/

App log目录：/data/bkee/paas\_agent/apps/logs

进程状态:

进程示例，每个app拥有一个独立的docker进程

```text
root      9120 0.1 0.0 940860 24632 ?        Sl Jun19 183:33 dockerd --graph=/data/bkee/public/paas_agent/docker --exec-opt native.cgroupdriver=cgroupfs -H unix:///var/run/docker.sock --iptables=false --ip-forward=false --bridge=none
root      9148 0.0 0.0 748624 13560 ?        Ssl Jun19 39:51 docker-containerd -l unix:///var/run/docker/libcontainerd/docker-containerd.sock --shim docker-containerd-shim --metrics-interval=0 --start-timeout 2m --state-dir /var/run/docker/libcontainerd/containerd --runtime docker-runc
root     14216 0.0  0.0 416512 7084 ?        Sl Jun19 39:30 docker-containerd-shim a26d83edc0b3a03fb8602e296adc66158d3cc8ded1198836a91e41892c5a451e /var/run/docker/libcontainerd/a26d83edc0b3a03fb8602e296adc66158d3cc8ded1198836a91e41892c5a451e docker-runc
root     15805 0.0  0.0 416768 4404 ?        Sl Sep10 0:01 docker-containerd-shim 61c1d16a2ae1137211f168969c50df6511774530e6370501f26e55099214be6f /var/run/docker/libcontainerd/61c1d16a2ae1137211f168969c50df6511774530e6370501f26e55099214be6f docker-runc
root     27097 0.0  0.0 548096 4120 ?        Sl Sep10 0:00 docker-containerd-shim 699448fd6df6241e37b8f710673600663ffa8c65e1149d6c62dedc7a28739a67 /var/run/docker/libcontainerd/699448fd6df6241e37b8f710673600663ffa8c65e1149d6c62dedc7a28739a67 docker-runc
```

## 7.GSE

指令和文件下发模块

安装目录：/data/bkee/gse

log目录：/data/bkee/logs/gse/

Gse\_agent目录：/usr/local/gse/agent/

Gse\_agent log目录：/var/log/gse/

进程状态

```text
root     14510 0.0  0.0 113176 1208 ?        Ss 17:50 0:00 /bin/sh -c export INSTALL_PATH=/data/bkee; /data/bkee/bin/process_watch gse >/dev/null 2>&1
root     14511 6.0  0.0 114892 3260 ?        S 17:50 0:00 /bin/bash /data/bkee/bin/process_watch gse
root     31542 0.0  0.0 30560 1836 ?        Ss Sep25 0:00 ./gse_api -f /data/bkee/etc/gse/api.conf
root     31544 0.0  0.1 810316 45560 ?        Sl Sep25 0:03 ./gse_api -f /data/bkee/etc/gse/api.conf
root     31589 0.0  0.0 32768 1860 ?        Ss Sep25 0:00 ./gse_btsvr -f /data/bkee/etc/gse/btsvr.conf
root     31591 0.0  0.0 1803440 13640 ?       Sl Sep25 1:15 ./gse_btsvr -f /data/bkee/etc/gse/btsvr.conf
root     31635 0.0  0.0 28796 1628 ?        Ss Sep25 0:00 ./gse_data -f /data/bkee/etc/gse/data.conf
root     31636 7.7  0.1 5605048 42624 ?       Sl Sep25 136:39 ./gse_data -f /data/bkee/etc/gse/data.conf
root     31763 0.0  0.0 28368 1628 ?        Ss Sep25 0:00 ./gse_dba -f /data/bkee/etc/gse/dba.conf
root     31774 1.5  0.0 1838276 8824 ?        Sl Sep25 28:07 ./gse_dba -f /data/bkee/etc/gse/dba.conf
root     31889 0.0  0.0 33056 1832 ?        Ss Sep25 0:00 ./gse_task -f /data/bkee/etc/gse/task.conf
root     31890 0.2  0.0 3968012 20240 ?       Sl Sep25 4:14 ./gse_task -f /data/bkee/etc/gse/task.conf
root     31981 0.0  0.0 28088 1604 ?        Ss Sep25 0:00 ./gse_ops -f /data/bkee/etc/gse/ops.conf
root     31987 0.0  0.0 801916 7776 ?        Sl Sep25 0:25 ./gse_ops -f /data/bkee/etc/gse/ops.conf
root     32050 0.0  0.0 28060 1592 ?        Ss Sep25 0:00 ./gse_alarm -f /data/bkee/etc/gse/alarm.conf
root     32052 0.0  0.0 658264 6048 ?        Sl Sep25 0:04 ./gse_alarm -f /data/bkee/etc/gse/alarm.conf
root     32102 0.0  0.0 37216 1900 ?        Ss Sep25 0:00 ./gse_proc -f /data/bkee/etc/gse/proc.conf
root     32103 0.0  0.0 1617864 10520 ?       Sl Sep25 0:08 ./gse_proc -f /data/bkee/etc/gse/proc.conf
root     32181 0.0  0.0 28296 1632 ?        Ss Sep25 0:00 ./gse_opts -f /data/bkee/etc/gse/opts.conf
root     32183 0.0  0.0 576952 4020 ?        Sl Sep25 0:39 ./gse_opts -f /data/bkee/etc/gse/opts.conf
```

## 8.License

验证模块，根据cert对登陆等操作进行认证

安装目录: /data/bkee/license

Cert目录: /data/bkee/cert

配置文件: /data/bkee/etc/license.json

```text
[root@gse-2 cert]# cat /data/bkee/etc/license.json
{
       "Daemon":true,
       "IP":"192.168.1.4",
       "Port":443,
       "LogPath":"/data/bkee/logs/license",
       "CertPath":"/data/bkee/cert",
       "CertPasswordPath":"/data/bkee/cert/cert_encrypt.key"
}
```



进程状态:

```text
root     22515 0.0  0.0 619936 9800 ?        Sl Jun19 3:45 ./license_server -config /data/bkee/etc/license.json
```



















