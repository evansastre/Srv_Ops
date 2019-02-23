# Data Storage

开源存储

1.MySQL

2.Redis

3.Redis Cluster

4.Mongo

5.Rabbitmq

6.Influxdb





## 1.MySQL

部署：

```text
192.168.1.3 master
192.168.1.4 slave
```

存储application（元数据和应用表）和user 数据（例如cmdb所有机器信息，job模块task信息和log\)

```text
[root@rbtnode1 sixh]# /data/bkee/service/mysql/bin/mysql -uroot -p
```

主要分两部分，bk系统platform DB和应用DB（每个app一个db\_schema）

```text
MySQL-Plat DBs:
open_paas
cmdb
job
jobLog

MySQL-SaaS：
bk_agent_setup
bk_agent_setup_bkt
bk_bkdata_api
bk_bkdata_datamanager
bk_fta_solutions
bk_fta_solutions_bkt
bk_gsekit
bk_gsekit_bkt
bk_log_search
bk_log_search_bkt
bk_monitor
bk_monitor_bkt
bk_nodeman
bk_nodeman_bkt
bkdata_monitor_alert
bksuite_common
gcloud
gcloud_bkt
```

## 2. Redis

部署：

```text
203.117.xxx.3 master
203.117.xxx.4 master
```

两台redis之间相互独立，存储GSE发起的任务和结果状态，agent状态等，用作缓存队列

### 1. 203.117.xxx.3

```text
Connections:
192.168.1.6 cmdb_eventser/cmdb_datacoll
192.168.1.7 cmdb_eventser/cmdb_datacoll

root     22280  0.0  0.0 637708 14224 ?        Sl   Oct03   3:53 /data/bkee/cmdb/server/bin/cmdb_eventserver --addrport=192.168.1.6:32005 --logtostderr=false --log-dir=/data/bkee/logs/cmdb --v=3 --regdiscv=zk.service.consul:2181
root     22281  0.1  0.0 568748 26248 ?        Sl   Oct03  21:33 /data/bkee/cmdb/server/bin/cmdb_datacollection --logtostderr=false --log-dir=/data/bkee/logs/cmdb --v=3 --regdiscv=zk.service.consul:2181

[root@rbtnode1 sixh]#  redis-cli -h 192.168.1.3 -p 6379
192.168.1.3:6379>
192.168.1.3:6379> auth "***"
OK
192.168.1.3:6379>
192.168.1.3:6379>
192.168.1.3:6379> info
192.168.1.3:6379> keys *
  1) "GSETASK:SUCCESS:GSETASK:20181005185915:179"
  2) "cc:v3:ident:inst_module_106"
  3) "GSETASK:SUCCESS:GSETASK:20181003103524:60"
  4) "cc:v3:ident:inst_host_27"
  5) "GSETASK:SUCCESS:GSETASK:20181003123204:106"
  6) "GSETASK:SUCCESS:GSETASK:20180924172959:33"
  7) "cc:v3:ident:inst_host_47"
  8) "GSETASK:SUCCESS:GSETASK:20181003105055:66"
  9) "cc:v3:snapshot:9"
 10) "GSETASK:SUCCESS:GSETASK:20180921220926:12"
 11) "GSETASK:SUCCESS:GSETASK:20181003154930:140"
 ...
```



### 2.  203.117.xxx.4

```text
Connections:
192.168.1.4 redis-server/gse_dba

./gse_dba -f /data/bkee/etc/gse/dba.conf
redis-server 192.168.1.4:6379

[root@gse-2 sixh]# redis-cli -h 192.168.1.4 -p 6379
192.168.1.4:6379> auth "xxxxx"
OK
192.168.1.4:6379> keys *
  1) "GSETASK:SUCCESS:GSETASK:20181002190636:46"
  2) "GSETASK:SUCCESS:GSETASK:20181003132352:110"
  3) "GSETASK:SUCCESS:GSETASK:20180921220926:12"
  4) "GSETASK:SUCCESS:GSETASK:20180831032507:87"
  5) "GSETASK:SUCCESS:GSETASK:20181002110723:24"
  6) "GSETASK:SUCCESS:GSETASK:20181003132817:112"
  7) "GSETASK:RUNNING:GSETASK:20181003115949:90"
  8) "GSETASK:SUCCESS:GSETASK:20180829180707:81"
  9) "GSETASK:SUCCESS:GSETASK:20181003101843:55"
 10) "GSETASK:FAIL:GSETASK:20181003103539:61"
...
```

## 3. Redis Cluster

部署

```text
192.168.1.7 master
192.168.1.5 slave
192.168.1.6 slave

# Replication
role:master 192.168.1.7
connected_slaves:2
slave0:ip=192.168.1.6,port=6379,state=online,offset=267753526698,lag=0
slave1:ip=192.168.1.5,port=6379,state=online,offset=267753525922,lag=0
```



存储bk系统信息：

```text
[root@rbtnode2 sixh]# redis-cli -h 192.168.1.7 -p 6379
192.168.1.7:6379> auth "lvw($*,j09(*J"
OK
192.168.1.7:6379>
192.168.1.7:6379> keys *
1) "datalist"
2) "spring:session:bk.job:sessions:f9409d9a-e18a-4a05-87d2-46972ec47e4e"
3) "dmonitor_tasks"
4) "dmonitor_worker"
5) "spring:session:bk.job:expirations:1538990340000"
6) "spring:session:bk.job:sessions:expires:f9409d9a-e18a-4a05-87d2-46972ec47e4e"
7) "dmonitor_master"
192.168.1.7:6379>
```

## 4.Mongo

部署：

```text
192.168.1.5
```

版本更新后，用来存储cmdb等信息

```text
root@nginx-1 sixh]# mongo --host 192.168.1.5
MongoDB shell version v3.6.3
connecting to: mongodb://192.168.1.5:27017/
MongoDB server version: 3.6.3
Welcome to the MongoDB shell.
For interactive help, type "help".
For more comprehensive documentation, see
http://docs.mongodb.org/
Questions? Try the support group
http://groups.google.com/group/mongodb-user
>
>
> db.auth('root','XXXXX')
1
>
> show dbs;
admin   0.000GB
cmdb    0.003GB
config  0.000GB
local   0.000GB

> db.stats()
{
    "db" : "admin",
    "collections" : 3,
    "views" : 0,
    "objects" : 5,
    "avgObjSize" : 167.8,
    "dataSize" : 839,
    "storageSize" : 49152,
    "numExtents" : 0,
    "indexes" : 5,
    "indexSize" : 81920,
    "fsUsedSize" : 53948858368,
    "fsTotalSize" : 177961291776,
    "ok" : 1
}

> show users;
{
    "_id" : "cmdb.bk_cmdb",
    "user" : "bk_cmdb",
    "db" : "cmdb",
    "roles" : [
        {
            "role" : "readWrite",
            "db" : "cmdb"
        }
    ]
}
> db.currentOp()
{
    "inprog" : [
        {
            "host" : "nginx-1:27017",
            "desc" : "conn",
            "threadId" : "139996273985280",
            "connectionId" : 117,
            "client" : "192.168.1.5:51874",
            "appName" : "MongoDB Shell",
            "clientMetadata" : {
                "application" : {
                    "name" : "MongoDB Shell"
                },
                "driver" : {
                    "name" : "MongoDB Internal Client",
                    "version" : "3.6.3"
                },
                "os" : {
                    "type" : "Linux",
                    "name" : "CentOS Linux release 7.3.1611 (Core) ",
                    "architecture" : "x86_64",
                    "version" : "Kernel 3.10.0-514.el7.x86_64"
                }
            },
            "active" : true,
            "currentOpTime" : "2018-09-10T16:10:52.005+0800",
            "opid" : 35578773,
            "secs_running" : NumberLong(0),
            "microsecs_running" : NumberLong(2776),
            "op" : "command",
            "ns" : "admin.$cmd.aggregate",
            "command" : {
                "currentOp" : 1,
                "$db" : "admin"
            },
            "numYields" : 0,
            "locks" : {

            },
            "waitingForLock" : false,
            "lockStats" : {

            }
        }
    ],
    "ok" : 1
}
>
```

## 5.Rabbitmq

部署:

```text
Master: 192.168.1.3 rbtnode1
Slave:  192.168.1.7 rbtnode2

Cluster Status:
[{nodes,[{disc,[rabbit@rbtnode1,rabbit@rbtnode2]}]},
 {running_nodes,[rabbit@rbtnode2,rabbit@rbtnode1]},
 {cluster_name,<<"rabbit@rbtnode1">>},
 {partitions,[]},
 {alarms,[{rabbit@rbtnode2,[]},{rabbit@rbtnode1,[]}]}]
```



用作open\_paas与Saas/GSE之间队列

```text
[root@rbtnode1 sixh]# rabbitmqctl authenticate_user "admin" "xxx"

Connections:
bk_bkdata 192.168.1.5
bk_bkdata 192.168.1.6
bk_job 192.168.1.5
bk_job 192.168.1.7
bk_log_search 192.168.1.3
bk_log_search 192.168.1.4
bk_log_search 192.168.1.7
bk_monitor 192.168.1.3
bk_monitor 192.168.1.4
bk_nodeman 192.168.1.3
bk_nodeman 192.168.1.4
bk_nodeman 192.168.1.7
gcloud 192.168.1.3
gcloud 192.168.1.4
```



### 6.Influxdb

存储监控数据

部署：

Influxdb Cluster

```text
192.168.1.5
192.168.1.6
```

```text
[root@nginx-1 sixh]# influx -host 192.168.1.5 -port 5260
Connected to http://192.168.1.5:5260 version 1.3.6
InfluxDB shell version: 1.3.6
> show databases;
name: databases
name
----
_internal
system_8
system_14
system_9
system_17
system_19
mysql_19
nginx_8
mysql_8
system_3
monitor_data_metrics
monitor_custom_metrics
```

