# LVS

LVS，全称Linux Virtual Server，是国人章文嵩发起的一个开源项目。  
 在社区具有很大的热度，是一个基于四层、具有强大性能的反向代理服务器。  
 `早期使用lvs需要修改内核才能使用，但是由于性能优异，现在已经被收入内核。`

LVS通过工作于内核的ipvs模块来实现功能，其主要工作于netfilter 的INPUT链上。  
 而用户需要对ipvs进行操作配置则需要使用ipvsadm这个工具。  
 ipvsadm主要用于设置lvs模型、调度方式以及指定后端主机。

> #### LVS中的角色

**LVS的一些相关术语**

LVS的模型中有两个角色：  
 **调度器:**Director，又称为Dispatcher，Balancer  
 `调度器主要用于接受用户请求。`  
 **真实主机:**Real Server，简称为RS。  
 `用于真正处理用户的请求。`

而为了更好地理解，我们将所在角色的IP地址分为以下三种：  
 **Director Virtual IP:**调度器用于与客户端通信的IP地址，简称为VIP  
 **Director IP**:调度器用于与RealServer通信的IP地址，简称为DIP。  
 **Real Server :** 后端主机的用于与调度器通信的IP地址，简称为RIP。![](//upload-images.jianshu.io/upload_images/3125535-8aea7551f3500db1.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000/format/webp)基本模型

> #### LVS的三种调度模式

#### LVS-NAT`Network Address Transform`

**示意图和调度步骤**

![](//upload-images.jianshu.io/upload_images/3125535-4b5a9caaa13ef764.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000/format/webp)LVS-NAT

**原理：**

基于ip伪装`MASQUERADES`，原理是多目标DNAT。  
 所以请求和响应都经由Director调度器。

**LVS-NAT的优点与缺点**

**优点：**

* 支持端口映射
* RS可以使用任意操作系统
* 节省公有IP地址。  `RIP和DIP都应该使用同一网段私有地址，而且RS的网关要指向DIP。`  `使用nat另外一个好处就是后端的主机相对比较安全。`

**缺点：**

* 请求和响应报文都要经过Director转发;极高负载时，Director可能成为系统瓶颈。  `就是效率低的意思。`

#### LVS-TUN`IP Tuneling`

**示意图和调度步骤**

![](//upload-images.jianshu.io/upload_images/3125535-d1a52b8826d2c175.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000/format/webp)LVS-TUN

**原理：**

基于隧道封装技术。在IP报文的外面再包一层IP报文。  
 当Director接收到请求的时候，选举出调度的RealServer  
 当接受到从Director而来的请求时，RealServer则会使用lo接口上的VIP直接响应CIP。  
 这样CIP请求VIP的资源，收到的也是VIP响应。

**LVS-TUN的优点与缺点**

**优点：**

* RIP,VIP,DIP都应该使用公网地址，且RS网关不指向DIP;  `只接受进站请求，解决了LVS-NAT时的问题，减少负载。`  `请求报文经由Director调度，但是响应报文不需经由Director。`

**缺点：**

* 不指向Director所以不支持端口映射。
* RS的OS必须支持隧道功能。
* 隧道技术会额外花费性能，增大开销。

#### LVS-DR`Direct Routing`

**示意图和调度步骤**

![](//upload-images.jianshu.io/upload_images/3125535-41d19e0b01be1dc0.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000/format/webp)LVS-DR

**原理**

当Director接收到请求之后，通过调度方法选举出RealServer。  
 讲目标地址的MAC地址改为RealServer的MAC地址。  
 RealServer接受到转发而来的请求，发现目标地址是VIP。`RealServer配置在lo接口上。`  
 处理请求之后则使用lo接口上的VIP响应CIP。

**LVS-DR的优点与缺点**

**优点：**

* RIP可以使用私有地址，也可以使用公网地址。  `只要求DIP和RIP的地址在同一个网段内。`
* 请求报文经由Director调度，但是响应报文不经由Director。
* RS可以使用大多数OS

**缺点：**

* 不支持端口映射。
* 不能跨局域网。

**总结：**

三种模型虽然各有利弊，但是由于追求性能和便捷，DR是目前用得最多的LVS模型。

> #### LVS的八种调度方法

**静态方法:仅依据算法本身进行轮询调度**

* RR:Round Robin,轮调  `一个接一个，自上而下`
* WRR:Weighted RR，加权论调  `加权，手动让能者多劳。`
* SH:SourceIP Hash  `来自同一个IP地址的请求都将调度到同一个RealServer`
* DH:Destination Hash  `不管IP，请求特定的东西，都定义到同一个RS上。`

**动态方法:根据算法及RS的当前负载状态进行调度**

* LC:least connections\(最小链接数\)  `链接最少，也就是Overhead最小就调度给谁。`  `假如都一样，就根据配置的RS自上而下调度。`
* WLC:Weighted Least Connection \(加权最小连接数\)  `这个是LVS的默认算法。`
* SED:Shortest Expection Delay\(最小期望延迟\)  `WLC算法的改进。`
* NQ:Never Queue  `SED算法的改进。`
* LBLC:Locality-Based Least-Connection,基于局部的的LC算法  正向代理缓存机制。访问缓存服务器，调高缓存的命中率。  和传统DH算法比较，考虑缓存服务器负载。可以看做是DH+LC  如果有两个缓存服务器  1.只要调度到其中的一个缓存服务器，那缓存服务器内就会记录下来。下一次访问同一个资源的时候也就是这个服务器了。 \(DH\)  2.有一个用户从来没有访问过这两个缓存服务器，那就分配到负载较小的服务器。`LC`

LBLCR:Locality-Based Least-Connection with Replication\(带复制的lblc算法\)  
 缓存服务器中的缓存可以互相复制。  
 因为即使没有，也能立即从另外一个服务器内复制一份，并且均衡负载

`man ipvsadm有讲这几种动态或者静态的rs调度方法`

> **配置LVS-DR**

| 主机名 | 主机地址 | 角色 |
| :--- | :--- | :--- |
| node1 | DIP:192.168.2.201，VIP:192.168.2.211 | Director |
| node3 | RIP:192.168.2.203，VIP:192.168.2.211 | RealServer |
| node4 | RIP:192.168.2.204，VIP:192.168.2.211 | RealServer |

`本文中的主机系统均为CentOS7.1，Apache2.4，数据库：MariaDB-5.5.50`

实验拓扑：  
![](//upload-images.jianshu.io/upload_images/3125535-abd47e0493580138.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/603/format/webp)lvs-dr实验拓扑

**\(1\)在Director上配置VIP和DIP**

```text
  [root@bc ~]# vim /etc/sysconfig/network-scripts/ifcfg-eno16777736
    TYPE=Ethernet
    BOOTPROTO="static"
    DEFROUTE=yes
    PEERDNS=yes
    PEERROUTES=yes
    NAME=eno16777736
    DEVICE=eno16777736
    ONBOOT=yes
    IPADDR="192.168.2.201"
    NETMASK="255.255.255.0"
    DNS1="192.168.2.1"
    GATEWAY="192.168.2.1"

[root@bc ~]# vim /etc/sysconfig/network-scripts/ifcfg-eno16777736:0
    TYPE=Ethernet
    BOOTPROTO="static"
    NAME=eno16777736:0
    ONBOOT=yes
    IPADDR="192.168.2.211"
    NETMASK="255.255.255.0"
    DNS1="192.168.2.1"
    GATEWAY="192.168.2.1"
    ONPARENT=yes
```

重启网络之后查看配置

```text
[root@bc ~]# service NetworkManager stop
  Redirecting to /bin/systemctl stop  NetworkManager.service
[root@bc ~]# service network restart
  Restarting network (via systemctl):                        [  OK  ]
[root@bc ~]# ifconfig
  eno16777736: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.2.201  netmask 255.255.255.0  broadcast 192.168.2.255
        inet6 fe80::250:56ff:fe3c:d757  prefixlen 64  scopeid 0x20<link>
        ether 00:50:56:3c:d7:57  txqueuelen 1000  (Ethernet)
        RX packets 88853  bytes 14843664 (14.1 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 79195  bytes 6551143 (6.2 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

  eno16777736:0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.2.211  netmask 255.255.255.0  broadcast 192.168.2.255
        ether 00:50:56:3c:d7:57  txqueuelen 1000  (Ethernet)

  lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 0  (Local Loopback)
        RX packets 12998  bytes 1140269 (1.0 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 12998  bytes 1140269 (1.0 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

**\(2\)Director使用ipvsadm修改创建ipvs规则**

```text
[root@bc ~]# ipvsadm -A -t 192.168.2.211:80 -s rr
[root@bc ~]# ipvsadm -a -t 192.168.2.211:80 -r 192.168.2.203 -g
[root@bc ~]# ipvsadm -a -t 192.168.2.211:80 -r 192.168.2.204 -g
[root@bc ~]# ipvsadm -L -n
IP Virtual Server version 1.2.1 (size=4096)
Prot LocalAddress:Port Scheduler Flags
  -> RemoteAddress:Port           Forward Weight ActiveConn InActConn
TCP  192.168.2.211:80 rr
  -> 192.168.2.203:80             Route   1      0          0         
  -> 192.168.2.204:80             Route   1      0          0   
```

**\(3\)RealServer安装httpd**

```text
[root@node3 ~]# yum install httpd -y
[root@node4 ~]# yum install httpd -y
```

`可以在里面放一个Wordpress,也可以简单echo几个字到index.html`  
 **\(4\)node3和node4修改RealServer内核参数**

```text
echo "1" > /proc/sys/net/ipv4/ip_forward
echo "2" > /proc/sys/net/ipv4/conf/all/arp_announce
echo "1" > /proc/sys/net/ipv4/conf/all/arp_ignore
echo "1" > /proc/sys/net/ipv4/conf/lo/arp_ignore
echo "2" > /proc/sys/net/ipv4/conf/lo/arp_announce
ifconfig lo:0 192.168.2.211/32 broadcast 192.168.2.211 up
route add -host 192.168.2.211 dev lo:0
```

`修改内核参数，并且配置VIP地址到RealServer的loopback接口上。`  
 **`那样的话，当RealServer接到从Director转发而来的数据报文时，RealServer也不会丢弃报文。`**  
 `同时，修改了RealServer的参数，局域网内的arp表就只有Director有VIP。`  
 `RealServer的的机器上有VIP这件事，只有RealServer自己知道。`  
 **`这样可以保证，当请求到来的时候，第一个会送到Director那里去。`**

**\(5\)测试结果**

```text
[root@node3 httpd]# vim  /var/log/httpd/access_log 
[root@node4 httpd]# vim  /var/log/httpd/access_log 
```

效果差不多就是这样:  
 `因为我们使用了RR静态调度方法,所以这node3和node4的请求是一人一个。`  
![](//upload-images.jianshu.io/upload_images/3125535-9b15f71b5b07602b.gif?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000/format/webp)Flash  
  


