# Vlan

[**1 vlan简介**](https://link.jianshu.com?t=http://blog.csdn.net/jesseyoung/article/details/40047749)  


VLAN（Virtual Local Area Network）的中文名为"虚拟局域网"。VLAN是一种将局域网设备从逻辑上划分成一个个网段，从而实现虚拟工作组的新兴数据交换技术。这一新兴技术主要应用于交换机和路由器中，但主流应用还是在交换机之中。但又不是所有交换机都具有此功能，只有VLAN协议的第二层以上交换机才具有此功能。802.1Q的标准的出现打破了虚拟网依赖于单一厂商的僵局，从一个侧面推动了VLAN的迅速发展。

[**2 交换机端口工作模式简介**](https://link.jianshu.com?t=http://blog.csdn.net/jesseyoung/article/details/40047749)

交换机端口有三种工作模式，分别是Access，Hybrid，Trunk。

Access类型的端口只能属于1个VLAN，一般用于连接计算机的端口；

Trunk类型的端口可以允许多个VLAN通过，可以接收和发送多个VLAN的报文，一般用于交换机之间连接的端口；

Hybrid类型的端口可以允许多个VLAN通过，可以接收和发送多个VLAN的报文，可以用于交换机之间连接，也可以用于连接用户的计算机。

Hybrid端口和Trunk端口在接收数据时，处理方法是一样的，唯一不同之处在于发送数据时：Hybrid端口可以允许多个VLAN的报文发送时不打标签，而Trunk端口只允许缺省VLAN的报文发送时不打标签。

[**3 基本概念（tag，untag，802.1Q）**](https://link.jianshu.com?t=http://blog.csdn.net/jesseyoung/article/details/40047749)  


untag就是普通的ethernet报文，普通PC机的网卡是可以识别这样的报文进行通讯；

tag报文结构的变化是在源mac地址和目的mac地址之后，加上了4bytes的vlan信息，也就是vlan tag头；一般来说这样的报文普通PC机的网卡是不能识别的

下图说明了802.1Q封装tag报文帧结构![](//upload-images.jianshu.io/upload_images/6105755-66b37ad347d4430a?imageMogr2/auto-orient/strip%7CimageView2/2/w/553/format/webp)

带802.1Q的帧是在标准以太网帧上插入了4个字节的标识。其中包含：

2个字节的协议标识符（TPID\)，当前置0x8100的固定值，表明该帧带有802.1Q的标记信息。

2个字节的标记控制信息（TCI），包含了三个域。

Priority域，占3bits，表示报文的优先级，取值0到7，7为最高优先级，0为最低优先级。该域被802.1p采用。

规范格式指示符（CFI\)域，占1bit，0表示规范格式，应用于以太网；1表示非规范格式，应用于Token Ring。

VLAN ID域，占12bit，用于标示VLAN的归属。

[**4 交换机接口出入数据处理过程**](https://link.jianshu.com?t=http://blog.csdn.net/jesseyoung/article/details/40047749)  


**4.1 端口接收报文时的处理：**

![](//upload-images.jianshu.io/upload_images/6105755-1088c25430d470d6?imageMogr2/auto-orient/strip%7CimageView2/2/w/554/format/webp)

Acess端口收报文:

收到一个报文,判断是否有VLAN信息：如果没有则打上端口的PVID，并进行交换转发,如果有则直接丢弃（缺省）

trunk端口收报文：

收到一个报文，判断是否有VLAN信息：如果没有则打上端口的PVID，并进行交换转发，如果有判断该trunk端口是否允许该 VLAN的数据进入：如果允许则报文携带原有VLAN标记进行转发，否则丢弃该报文。

hybrid端口收报文：

收到一个报文,判断是否有VLAN信息：如果没有则打上端口的PVID，并进行交换转发，如果有则判断该hybrid端口是否允许该VLAN的数据进入：如果可以则转发，否则丢弃。

**4.2 端口发送报文时的处理**

![](//upload-images.jianshu.io/upload_images/6105755-9bcb54ecf53948f9?imageMogr2/auto-orient/strip%7CimageView2/2/w/558/format/webp)

Acess端口发报文：

将报文的VLAN信息剥离，直接发送出去

trunk端口发报文：

比较端口的PVID和将要发送报文的VLAN信息，如果两者相等则剥离VLAN信息，再发送，否则报文将携带原有的VLAN标记进行转发。

hybrid端口发报文：

1、判断该VLAN在本端口的属性

2、如果是untag则剥离VLAN信息，再发送，如果是tag则比较端口的PVID和将要发送报文的VLAN信息，如果两者相等则剥离VLAN信息，再发送，否则报文将携带原有的VLAN标记进行转发。  
  


