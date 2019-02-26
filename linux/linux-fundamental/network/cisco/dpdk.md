# DPDK

在[X86](https://zh.wikipedia.org/wiki/X86)结构中，处理数据包的传统方式是[CPU](https://zh.wikipedia.org/wiki/%E4%B8%AD%E5%A4%AE%E5%A4%84%E7%90%86%E5%99%A8)中断方式，即网卡驱动接收到数据包后通过中断通知CPU处理，然后由CPU拷贝数据并交给协议栈。在数据量大时，这种方式会产生大量CPU中断，导致CPU无法运行其他程序。

而DPDK则采用[轮询](https://zh.wikipedia.org/wiki/%E8%BC%AA%E8%A9%A2)方式实现数据包处理过程：DPDK重载了网卡驱动，该驱动在收到数据包后不中断通知CPU，而是将数据包通过[零拷贝](https://zh.wikipedia.org/wiki/%E9%9B%B6%E6%8B%B7%E8%B4%9D)技术存入[内存](https://zh.wikipedia.org/wiki/%E5%86%85%E5%AD%98)，这时应用层程序就可以通过DPDK提供的接口，直接从内存读取数据包。

这种处理方式节省了CPU中断时间、内存拷贝时间，并向应用层提供了简单易行且高效的数据包处理方式，使得网络应用的开发更加方便。但同时，由于需要重载网卡驱动，因此该开发包目前只能用在部分采用[Intel](https://zh.wikipedia.org/wiki/%E8%8B%B1%E7%89%B9%E5%B0%94)网络处理芯片的[网卡](https://zh.wikipedia.org/wiki/%E7%BD%91%E5%8D%A1)中。

