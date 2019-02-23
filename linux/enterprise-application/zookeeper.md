# zookeeper

Download

zookeeper is run by java, so we need install java first

[java download](https://www.oracle.com/technetwork/java/javase/downloads/index.html) 

Get link from website, then copy to linux server

```text
wget  ****
tar xf jdk-11.0.1_linux-x64_bin.tar.gz
vim /etc/profile
#add below content
===================
JAVA_HOME=/[your_java_path]/jdk-11.0.1
JRE_HOME=$JAVA_HOME/jre
PATH=$PATH:$JAVA_HOME/bin
CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
export JAVA_HOME
export JRE_HOME
export PATH
export CLASSPATH
===================

source /etc/profile
java --version
ln -s /[your_java_path]/jdk1.8.0_131/bin/java /usr/bin/java




```

[zookeeper download](http://zookeeper.apache.org/releases.html)

```text
wget https://www-eu.apache.org/dist/zookeeper/zookeeper-3.4.10/zookeeper-3.4.10.tar.gz
tar xf zookeeper-3.4.10.tar.gz
cd zookeeper-3.4.10
```

config  [Clustered \(Multi-Server\) Setup](http://zookeeper.apache.org/doc/r3.3.3/zookeeperAdmin.html#sc_zkMulitServerSetup)

```text
vim conf/zoo.cfg
#for blueking path is  /data/bkee_xxx/service/zk/conf/zoo.cfg

===================
tickTime=2000
initLimit=10
syncLimit=20
#path can be separated by project name
dataDir=/data/bkee_xxx/public/zk/data
dataLogDir=/data/bkee_xxx/public/zk/datalog
clientPortAddress=10.38.0.4
clientPort=2182    #default 2181
maxClientCnxns=60
autopurge.snapRetainCount=5
autopurge.purgeInterval=8
server.1=10.38.0.4:2889:3889    #default :2888:3888
server.2=10.38.0.3:2889:3889   #default 2888:3888
server.3=10.38.0.6:2889:3889   #default 2888:3888
===================

vim /data/bkee_xxx/public/zk/data/myid
#for example, 
your current located is 10.38.0.4, this file content should be "1"
your current located is 10.38.0.3, this file content should be "2"
===================
1
===================

```

Start

\#need start by sequence, from server.1 to server.end

```text
bin/zkServer.sh start    
bin/zkServer.sh status
```

Basic troubleshoot

\#check error log for figure out problems

```text
vim zookeeper.out
```



Test your deployment by connecting to the hosts:

you can run the following command to execute simple operations:

```text
bin/zkCli.sh -server 127.0.0.1:2181
```



Change in script

```text
zk.sh
Delete if statement, define every time
===========================
#!/bin/bash


cd ${BASH_SOURCE%/*} 2>/dev/null
WORKDIR=$PWD

#if [ -z "$BK_HOME" ]; then
    export BK_HOME=${WORKDIR%/service*}
#fi

#if [ -z "$JAVA_HOME" ]; then
    export JAVA_HOME=$BK_HOME/service/java
#fi

#if [ -z "$CONF_HOME" ]; then
    export CONF_HOME=$BK_HOME/etc
#fi

export LOGS_HOME=$BK_HOME/logs/zk
export PATH=$JAVA_HOME/bin:$PATH
export CLASSPATH=$BK_HOME/service/zk/conf:$JAVA_HOME/lib:$CLASSPATH

export ZOO_LOG_DIR=$BK_HOME/logs/zk/
export ZOO_LOG4J_PROP='INFO,ROLLINGFILE'

./zkServer.sh "$@"
===========================
```

