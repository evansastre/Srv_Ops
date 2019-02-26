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

\(1\).pvid是什么

PVID英文解释为Port-base VLAN ID，是基于端口的VLAN ID，一个端口可以属于多个vlan，但是只能有一个PVID，收到一个不带tag头的数据包时，会打上PVID所表示的vlan号，视同该vlan的数据包处理，所以也有人说PVID就是某个端口默认的vlan ID号。

作者：lanlicen 来源：CSDN 原文：[https://blog.csdn.net/lanlicen/article/details/6333245](https://blog.csdn.net/lanlicen/article/details/6333245) 版权声明：本文为博主原创文章，转载请附上博文链接！

注意：PVID并不是加在帧头的标记，而是端口的属性，用来标识端口接收到的未标记的帧。也就是说，当端口收到一个未标记的帧时，则把该帧转发到VID和本端口PVID相等的VLAN中去。

\(2\).vid是什么

VID（VLAN ID）是VLAN的标识，定义其中的端口可以接收发自这个VLAN的包；而PVID（Port VLAN ID）定义这个**untag端口**可以**转发**哪个VLAN的包。比如，当端口1同时属于VLAN1、VLAN2和VLAN3时，而它的PVID为1，那么端口1可以接收到VLAN1，2，3的数据，但发出的包只能发到VLAN1中。

\(3\).vid和pvid的作用

vid的作用在于当VLAN跨设备时（即switch1和switch2中都有VLAN2），各个设备需要和其他设备中的相同VLAN实现通信时，就必须在数据帧中加入vlan tag，来标示该数据帧应该被转发的vlan id。简而言之，vid是用在设备之间互联时用来决定一个二层帧属于哪个vlan的标记。

pvid更多的时候是用于设备和计算机互联时，用来标示计算机发出的未携带TAG的数据帧属于哪个vlan。





[**4 交换机接口出入数据处理过程**](https://link.jianshu.com?t=http://blog.csdn.net/jesseyoung/article/details/40047749)  


**4.1 端口接收报文时的处理：**

![](//upload-images.jianshu.io/upload_images/6105755-1088c25430d470d6?imageMogr2/auto-orient/strip%7CimageView2/2/w/554/format/webp)

Acess端口收报文:

收到一个报文,判断是否有VLAN信息：如果没有则打上端口的PVID，并进行交换转发,如果有则直接丢弃（缺省）

trunk端口收报文：

收到一个报文，判断是否有VLAN信息：如果没有则打上端口的PVID，并进行交换转发，如果有判断该trunk端口是否允许该 VLAN的数据进入：如果允许则报文携带原有VLAN标记进行转发，否则丢弃该报文。

hybrid端口收报文：

收到一个报文,判断是否有VLAN信息：如果没有则打上端口的PVID，并进行交换转发，如果有则判断该hybrid端口是否允许该VLAN的数据进入：如果可以则转发，否则丢弃。



1、一个数据包要进入一个tagged端口，如果其原来是untagged，则给其打上为tag，号码为pvid，如果其已经为tagged则原样输入； 

2、一个数据包要进入一个untagged端口，如果其原来是untagged，则给其打上tag，号码为pvid，如果其已经打上了tagged，则丢弃 该包；

3、一个数据包要出一个tagged端口，如果其原来是untagged包，则给其打上tag,号码为pvid，如果其原来是tagged包，则原样输出；4、一个数据包要出一个untagged端口，如果其原来是untagged包，则原样输出，如果其原来是tagged包，则去掉其tag头部，变为untagged。



**4.2 端口发送报文时的处理**

![](//upload-images.jianshu.io/upload_images/6105755-9bcb54ecf53948f9?imageMogr2/auto-orient/strip%7CimageView2/2/w/558/format/webp)

Acess端口发报文：

将报文的VLAN信息剥离，直接发送出去

trunk端口发报文：

比较端口的PVID和将要发送报文的VLAN信息，如果两者相等则剥离VLAN信息，再发送，否则报文将携带原有的VLAN标记进行转发。

hybrid端口发报文：

1、判断该VLAN在本端口的属性

2、如果是untag则剥离VLAN信息，再发送，如果是tag则比较端口的PVID和将要发送报文的VLAN信息，如果两者相等则剥离VLAN信息，再发送，否则报文将携带原有的VLAN标记进行转发。  


  


