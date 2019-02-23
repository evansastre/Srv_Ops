# DB Migration Testing

#### 数据存储：

1.MySQL

2.Mongodb

#### 测试资源：

BlueKing 测试服务器

#### 测试目标：

两套版本一致的BK集群数据切换

1.源数据直接替换

2.使用数据源IP进行切换



## 一、源数据直接替换

### 1.MySQL （不涉及cmdb模块）

#### 资源：

Test1 MySQL 集群

Test2 MySQL 集群

#### 备份数据：

```text
/data/bkee/service/mysql/bin/mysqldump --all-databases > Test1_dump_20181025.sql
/data/bkee/service/mysql/bin/mysqldump --all-databases > Test2_dump_20181025.sql
/data/bkee/service/mysql/bin/mysqldump open_paas > Test2_open_paas.sql
/data/bkee/service/mysql/bin/mysqldump job > Test2_job.sql
```

#### 恢复数据：

```text
source Test1_dump_20181025.sql;
```





#### 测试过程：

1.清理Test2 MySQL集群数据，灌入Test1 MySQL 集群数据

结果：

1.节点管理等app可用

2.job 不可用

2.清理Test2 MySQL 集群数据，灌入Test1 MySQL 集群数据，保留Test2 job 数据

结果：

1.节点管理等app可用

2.job 不可用

2.清理Test2 MySQL 集群数据，灌入Test1 MySQL 集群数据，保留Test2 open\_paas 数据

结果：

各个模块均可用，显示Test1 集群数据

### 2.MongoDB （cmdb模块）

#### 资源：

Test1 MongoDB集群

Test2 MongoDB集群

#### 备份数据：

```text
/data/bkee/service/mongodb/bin/mongodump -u 'xxx' -p 'xxx' --host 127.0.0.1 --port 27017 --authenticationDatabase cmdb -d cmdb -o /data/bkee/public/mongodb_backup
```

#### 恢复数据：

```text
/data/bkee/service/mongodb/bin/mongorestore -u 'xxx' -p 'xxxx' --host 127.0.0.1 --port 27017 --authenticationDatabase cmdb -d cmdb cmdb/
```

#### 测试过程：

1.Test2 环境下，删除Test2 MongoDB内cmdb库数据

结果：配置平台功能正常，但显示无业务权限，job不可用，显示无业务权限 （配置平台和job相互依赖，以cmdb为基础数据）

2.Test2环境下，灌入Test1 MongoDB内cmdb数据

结果：各功能正常，cmdb模块显示Test1 cmdb数据

3.Test2环境下，不清理Test2 MongoDB数据情况下，直接用Test1 MongoDB覆盖Test2 数据，部分collections出现数据重复（系统表）

结果：各功能正常，cmdb模块显示Test1+Test2 cmdb数据





## 二、使用数据源IP进行切换

#### 资源：

1.Test1 MySQL + MongoDB 集群

2.Test2 MySQL + MongoDB集群

#### 数据源切换：

1.Test2环境下，更改配置MySQL+MongoDB为Test1配置

2.Test1 MySQL+MongoDB添加Test2 资源权限

```text
MySQL：
root用户，添加Test2集群权限；
MongoDB：
cmdb重新creatuser bk_cmdb

注意：MongoDB需保持集群内mongodb.key一致
```

3.变更Test2 环境内各个模块（job/cmdb/paas）db连接配置

```text
例如：
cmdb：
[root@gse-2 conf]# ls /data/bkee/cmdb/server/conf
apiserver.conf  auditcontroller.conf  datacollection.conf  eventserver.conf  host.conf  hostcontroller.conf  migrate.conf  objectcontroller.conf  proc.conf  proccontroller.conf  topo.conf  webserver.conf

可通过重新下发配置，重装进行配置
```



#### 测试结果：

1.配置中心和job 可以正常显示Test1环境内容

2.所有server agent需要重新安装

3.其他SaaS app可用并显示Test1数据（节点管理可用，其他SaaS app卸载后安装失败，待解决 --）















