# multicast



> 单播用于两个主机之间的端对端通信，但平时开发中有这样的场景，要向一组N个主机发送相同的数据，如果基于TCP提供服务器，则需要维护N个套接字连接，即使使用UDP套接字提供服务器，也需要N次的数据发送。像这样，向大量客户端发送相同数据时，也会对服务器端和网络流量产生负面影响，可以使用多播和广播技术解决该问题。

前面几篇文章讲解了有关TCP套接字和UDP套接字通信代码及原理，今天在UDP套接字通信的基础上探讨下广播和多播相关。

## 一、多播

多播\(Multicast\)也叫组播，传输数据传输时基于UDP完成的，因此与UDP通信的服务器和客户端非常相近。区别在于UDP数据只能向单一目的地址传输，而多播数据可以同时传递到加入\(注册\)特定的多个主机

### **1. 多播传输数据特点：**

* 多播发送者针对特定的多播组织发送一次数据
* 加入特定组的接收者都可以收到多播数据

### **2. 多播地址：**

多播地址是D类IP地址：224.0.0.0~239.255.255.255，并被划分为局部链接多播地址、预留多播地址和管理权限多播地址三类。  
 **局部链接多播地址**：224.0.0.0~224.0.0.255，这是为路由协议和其它用途保留的地址，路由器并不转发属于此范围的IP包  
 **预留多播地址**：224.0.1.0~238.255.255.255，可用于全球范围（如Internet）或网络协议  
 **管理权限多播地址**：239.0.0.0~239.255.255.255，可供组织内部使用，类似于私有IP地址，不能用于Internet，可限制多播范围

### **3. 多播传输原理：**

多播是基于UDP套接字传输数据的基础完成，数据包格式与前面讲到的UDP数据包相同，以前的传输数据包的地址改成多播地址，向网络传递一个多播数据包时，路由器将复制该数据包并传递到多个主机，多播的传输需要借助路由器完成，正是由于这样的特性，大大节省了网络流量，减少了占用带宽，同时也减少了发送端的重复无用的工作，多播主要用于“多媒体数据的实时传输”。  
 要实现多播通信，要求介于多播源和接收者之间的路由器、集线器、交换机以及主机均需支持IP多播。目前，IP多播技术已得到硬件、软件厂商的广泛支持。

多播可以跨网传输，传输流程如下：![](//upload-images.jianshu.io/upload_images/4322526-dd5d7eb8e78efae3.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000/format/webp)组播传输流程.jpg

### **4**  播也要通过设置UDP套接字的相关参数完后  下面是加入组播关闭时离开组播的代码示例**. 多播实现：**

有关多播的实现需要设置UDP套接字的一些可选项，在前面的一片文章[套接字\(Socket\)编程\(三\) 套接字可选项](https://www.jianshu.com/p/fad573d12e66)里面有提到设置方法和设置参数，有需要了解的可以点击链接查看。

|  **IPPROTO\_IP** 选项名 | 说明 | 数据类型 |
| :--- | :--- | :--- |
| IP\_MULTICAST\_TTL | 生存时间\(Time To Live\)，组播传送距离 | int |
| IP\_ADD\_MEMBERSHIP | 加入组播 | struct ip\_mreq |
| IP\_DROP\_MEMBERSHIP | 离开组播 | struct ip\_mreq |
| IP\_MULTICAST\_IF | 获取默认接口或设置接口 | int |
| IP\_MULTICAST\_LOOP | 组播数据回送，缺省默认回送 | int |

**多播发送端**

  
 发送端为了实现多播的传递，必须设置TTL，TTL是Time to Live的简写，是解决“数据包传递距离”的主要因素，TTL用整数表示，并且没经过一个路由器就减一，TTL变为0时，该数据包无法再被传递，只能销毁，此值可以阻止将数据报转发到单个子网之外。  
 TTL的值设置过大将影响网络流量，当然设置过小也会导致数据无法传递到目的端，需要注意下。缺省情况下，发送 IP 多播数据报时其生存时间 \(time-to-live, TTL\) 值为 1。  
 使用套接字选项 IP\_MULTICAST\_TTL，可以将后续多播数据报的 TTL 设置为 0 到 255 之间的任何值。此功能用于控制多播的范围，这些阈值将针对具有以下初始 TTL 值的多播数据报强制实施相应约定  
 0 : 限定在同一主机  
 1 : 限定在同一子网  
 32 : 限定在同一站点  
 64 : 限定在同一地区  
 128 : 限定在同一洲  
 255 : 范围不受限制  
 站点和地区并未严格定义，站点可以根据实际情况再分为更小的管理单元![](//upload-images.jianshu.io/upload_images/4322526-37c81e25052238c4.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000/format/webp)TTL和多播路由.jpg

接下来给出设置TTL的代码示例，重复多播固定字符串

```text
#include <stdio.h>
#include <unistd.h>
#include <string.h>
#include <sys/socket.h>
#include <arpa/inet.h>
#include <errno.h>

int createMulticastSender(char* ip, uint16_t port);

int main(int argc, const char * argv[]) {
    
    char *ip = "239.145.145.145";
    uint16_t port = 9190;
    
    if (createMulticastSender(ip, port) == 0) {
        printf("开启多播发送端失败\n");
    }
    return 0;
}

#pragma mark ---开启多播发送端
int createMulticastSender(char* ip, uint16_t port)
{
    int sock;
    struct sockaddr_in mAddr;
    
    mAddr.sin_len = sizeof(mAddr);
    mAddr.sin_family = AF_INET;
    mAddr.sin_port = htons(port);
    mAddr.sin_addr.s_addr = inet_addr(ip);
    
    sock = socket(AF_INET, SOCK_DGRAM, 0);
    
    int opval = 64;
    if (setsockopt(sock, IPPROTO_IP, IP_MULTICAST_TTL, &opval, sizeof(opval)) == -1) {
        printf("设置多播的生命周期失败 code:%d description:%s\n",errno,strerror(errno));
        return 0;
    }
    /*
    //禁止组播回送
    int loop = 0;
    if (setsockopt(sock, IPPROTO_IP, IP_MULTICAST_LOOP, &loop, sizeof(loop)) == -1) {
        printf("禁止组播数据回送失败 code:%d description:%s\n",errno,strerror(errno));
    }
    */
    char *buffer = "Hello, World!";
    ssize_t buffer_len = strlen(buffer);
    while (1) {
        ssize_t sendLen = sendto(sock, buffer, buffer_len, 0, (struct sockaddr*)&mAddr, mAddr.sin_len);
        if (sendLen == buffer_len) {
            printf("成功多播 %zd 字节数据\n",sendLen);
        }else if (sendLen  == -1) {
            printf("多播失败  code:%d description:%s\n",errno,strerror(errno));
            break;
        }else {
            printf("多播数据不对 需要发送字节数为 %lu 字节，而实际发送 %zd 字节\n",sizeof(buffer),sendLen);
        }
        sleep(2);
    }
    
    printf("关闭多播发送端\n");
    close(sock);
    return 1;
}
```

**多播接收端**

```text
#include <stdio.h>
#include <unistd.h>
#include <string.h>
#include <sys/socket.h>
#include <arpa/inet.h>
#include <errno.h>

int createMulticastReceiver(char* ip, uint16_t port);

int main(int argc, const char * argv[]) {
    
    char *ip = "239.145.145.145";
    uint16_t port = 9190;
    
    if (createMulticastReceiver(ip, port) == 0) {
        printf("开启多播接收端失败\n");
    }
    return 0;
}

#pragma mark ---开启多播接收端
int createMulticastReceiver(char* ip, uint16_t port)
{
    int sock;
    struct sockaddr_in addr,peerAddr;
    memset(&peerAddr, 0, sizeof(peerAddr));
    memset(&addr, 0, sizeof(addr));
    struct ip_mreq join_adr;
    
    addr.sin_len = sizeof(addr);
    addr.sin_family = AF_INET;
    addr.sin_port = htons(port);
    addr.sin_addr.s_addr = htonl(INADDR_ANY);
    
    sock = socket(AF_INET, SOCK_DGRAM, 0);
    if (bind(sock, (struct sockaddr*)&addr, sizeof(addr)) == -1) {
        printf("绑定多播地址失败 code:%d description:%s\n",errno,strerror(errno));
        return 0;
    }
    
    join_adr.imr_interface.s_addr = htonl(INADDR_ANY);
    join_adr.imr_multiaddr.s_addr = inet_addr(ip);
    if (setsockopt(sock, IPPROTO_IP, IP_ADD_MEMBERSHIP, &join_adr, sizeof(join_adr)) == -1) {
        printf("加入组播失败 code:%d description:%s\n",errno,strerror(errno));
        return 0;
    }
    
    printf("准备工作完成，开始接收组播\n");
    char buffer[64];
    while (1) {
        memset(buffer, 0, sizeof(buffer));
        ssize_t recvLen = recvfrom(sock, buffer, sizeof(buffer), 0, (struct sockaddr*)&peerAddr, 0);
        if (recvLen > 0) {
            printf("peer IP:%s  peer Port:%d  buffer:%s\n",inet_ntoa(peerAddr.sin_addr),ntohs(peerAddr.sin_port),buffer);
            if (buffer[0] == 'C') break;
        }else {
            printf("接收多播错误 code:%d description:%s\n",errno,strerror(errno));
            break;
        }
    }
    
    printf("准备离开组播组\n");
    if (setsockopt(sock, IPPROTO_IP, IP_DROP_MEMBERSHIP, &join_adr, sizeof(join_adr)) == -1) {
        printf("离开组播失败 code:%d description:%s\n",errno,strerror(errno));
    }
    
    printf("关闭多播接收端\n");
    close(sock);
    return 1;
}
```

## 二、广播

广播的数据传输和多播相似，广播是一次性向网络内的所有主机发送数据，并且只能在局域网内传播，而不能跨网传播，广播也是基于UDP套接字传输数据实现。

## **1. 广播分类**

根据广播的地址不同，分为直接广播\(Directed Broadcast\)和本地广播\(Local Broadcast\)。  
 **直接广播**：广播的IP地址除了网络好外，其余主机地合作位全部设置为1，例如希望向 192.168.1.32 所在网络中的所有主机发送广播数据时可以向 192.168.1.255 传输。换而言之，可以采用直接广播的方式向特定区域内的所有主机传输数据。  
 **本地广播**：本地广播的IP地址是 255.255.255.255，向该主机所在网络的所有主机发送广播数据。

## **2. 广播实现**

有关广播的实现需要设置UDP套接字的一些可选项，在前面的一片文章[套接字\(Socket\)编程\(三\) 套接字可选项](https://www.jianshu.com/p/fad573d12e66)里面有提到设置方法和设置参数，有需要了解的可以点击链接查看。

| \*\* SOL\_SOCKET\*\* 选项名 | 说明 | 数据类型 |
| :--- | :--- | :--- |
| SO\_BROADCAST | 允许或禁止发送广播数据\(1启用，0不启用\) | int |

**广播发送端**  
 要实现广播的发送必须设置允许广播可选项，具体看下面示例

```text
#include <stdio.h>
#include <unistd.h>
#include <string.h>
#include <sys/socket.h>
#include <arpa/inet.h>
#include <errno.h>

int createBroadcastSender(char* ip, uint16_t port);

int main(int argc, const char * argv[]) {
    
    char *ip = "255.255.255.255";
    uint16_t port = 9190;
    
    if (createBroadcastSender(ip, port) == 0) {
        printf("开启广播发送端失败\n");
    }
    return 0;
}

#pragma mark ---开启广播发送端
int createBroadcastSender(char* ip, uint16_t port)
{
    int sock;
    struct sockaddr_in bAddr;
    memset(&bAddr, 0, sizeof(bAddr));
    
    bAddr.sin_len = sizeof(bAddr);
    bAddr.sin_family = AF_INET;
    bAddr.sin_port = htons(port);
    bAddr.sin_addr.s_addr = inet_addr(ip);
    
    sock = socket(AF_INET, SOCK_DGRAM, 0);
    
    int opval = 1;
    if (setsockopt(sock, SOL_SOCKET, SO_BROADCAST, &opval, sizeof(opval)) == -1) {
        printf("启用广播失败 code:%d description:%s\n",errno,strerror(errno));
        return 0;
    }
    
    char *buffer = "Hello, World!";
    ssize_t buffer_len = strlen(buffer);
    while (1) {
        ssize_t sendLen = sendto(sock, buffer, buffer_len, 0, (struct sockaddr*)&bAddr, sizeof(bAddr));
        if (sendLen == buffer_len) {
            printf("成功广播 %zd 字节数据\n",sendLen);
        }else if (sendLen  == -1) {
            printf("广播失败  code:%d description:%s\n",errno,strerror(errno));
            break;
        }else {
            printf("广播数据不对 需要发送字节数为 %lu 字节，而实际发送 %zd 字节\n",sizeof(buffer),sendLen);
        }
        sleep(5);
    }
    
    printf("关闭广播发送端\n");
    close(sock);
    return 1;
}
```

**广播接收端**

```text
#include <stdio.h>
#include <unistd.h>
#include <string.h>
#include <sys/socket.h>
#include <arpa/inet.h>
#include <errno.h>

int createBroadcastReceiver(uint16_t port);

int main(int argc, const char * argv[]) {
    
    uint16_t port = 9190;
    if (createBroadcastReceiver(port) == 0) {
        printf("开启广播接收端失败\n");
    }
    return 0;
}

#pragma mark ---开启广播接收端
int createBroadcastReceiver(uint16_t port)
{
    int sock;
    struct sockaddr_in addr;
    memset(&addr, 0, sizeof(addr));

    addr.sin_len = sizeof(addr);
    addr.sin_family = AF_INET;
    addr.sin_port = htons(port);
    addr.sin_addr.s_addr = htonl(INADDR_ANY);
    
    sock = socket(AF_INET, SOCK_DGRAM, 0);
    if (bind(sock, (struct sockaddr*)&addr, sizeof(addr)) == -1) {
        printf("绑定广播地址失败 code:%d description:%s\n",errno,strerror(errno));
        return 0;
    }
    
    printf("准备工作完成，开始接收广播\n");
    char buffer[64];
    while (1) {
        memset(buffer, 0, sizeof(buffer));
        ssize_t recvLen = recvfrom(sock, buffer, sizeof(buffer), 0, NULL, 0);
        if (recvLen > 0) {
            printf("buffer: %s\n",buffer);
            if (buffer[0] == 'C') break;
        }else {
            printf("接收广播错误 code:%d description:%s\n",errno,strerror(errno));
            break;
        }
    }
    
    printf("关闭广播接收端\n");
    close(sock);
    return 1;
}
```



关于广播和多播部分的实现很简单，都是基于UDP套接字。  


## **三、**组播IP地址到底是谁的IP？？

CTV source server \(Multicast Source IP\) = 1.1.1.1

CTV Channel1 \(Multicast Group IP\) =238.1.1.1 Server.

RP\(Rendezvous Point\) IP=2.2.2.2 This client network.

RP - &gt; CTV - &gt; join 238.1.1.1\(RPT\) -&gt; find 1.1.1.1 -&gt; join 1.1.1.1 \(SPT\)-&gt;  quit RP

IPTV is an application of IGMPv2 and PIM SM mode   


SPT = Source Path Tree





