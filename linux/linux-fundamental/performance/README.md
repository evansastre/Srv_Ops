# Performance

![](../../../.gitbook/assets/image.png)



### CPU方面

**处理器指标**

* CPU使用率: 每个处理器的利用率
* user time: CPU执行用户代码的时间，包括nice time
* system time: CPU执行内核代码的时间，包括IRQ和softirq time
* waiting: CPU等待IO的时间
* Idle time: CPU空闲并等待任务的时间
* nice time: CPU花在改变进程优先级以及执行顺序的时间
* load average: 任务队列中，等待被CPU执行的任务的总数，以及那些等待不可中断任务完成的任务的总数，它们的平均值。也就是，系统中处于**TASK\_RUNNABLE**以及**TASK\_UNINTERRUPTIBLE**状态的任务的总数的平均值。
* Runnable process: 等待被CPU执行的任务的总数
* Blocked: 那些因为IO操作被挂起的进程的数量
* Context switch: 系统中线程切换的总数。
* Interrupt: 硬中断和软中断的次数。

**消除CPU瓶颈的方法**

* 确保后台没有不必要的程序
* 给那些不重要并且是CPU密集型的应用调整优先级，让其优先级相对较低一些
* 更新CPU

### 内存方面

**内存指标**

* Free memory: 空闲内存。在Linux中，内核会将没有使用的内存中的大部分分配给文件系统缓存。所以，Free memory减去buffers以及cache占用的内存的数量，才是系统中真正的空闲内存的数量。
* swap usage: swap in/out衡量内存是否出现了瓶颈才更加正确。因为Linux内核如果发现内存中的一些page，长时间没有被用到，就回将它放到swap中。而并不是说，只有当内存不足的时候，才会将page放到swap中。如果每秒有200-300次 swap in/out，那么说明系统的内存可能是瓶颈。
* Buffer and cache: 为文件系统和block size分配的缓存
* slab: 内核使用的内存数量。需要注意的是，内核使用的page不能被page out到磁盘中
* active versus inactive memory: inactive memory将会被**kswapd** daemon swap out到磁盘中。

**free工具输出解释**

![](//upload-images.jianshu.io/upload_images/4108852-e614309bcbe1d7ac.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/688/format/webp)0.png

**消除内存瓶颈的方法**

* 调整page的大小
* 调整处理active和inactive内存的方式
* 降低page-out的速度
* 限制服务器上每个用户能够使用的内存的数量
* 停止不需要的service
* 增加内存

### 文件系统方面

**文件系统指标**

* IOWait: CPU等待IO操作的时间
* Average queue length: 未完成的IO请求的数量
* Average wait: IO请求等待被处理的时间，毫秒级
* Transfers per second: 每秒有多少IO操作被执行
* Blocks read/write per seconds: 每秒中读和写block的数量。在2.6版本的内核中，以block大小为1KB衡量。不同的内核版本中，block大小不同，从512bytes到4KB不等
* Kilobytes per second read/write: 每秒读写block device的数据量，用kilobytes来衡量

**Linux中常见的文件系统**

* Ext2
* Ext3
* ReiserFS
* Journal File System\(JFS\)
* XFS

其中，Ext3能够保证数据的一致性。而且，还能够通过配置journal mode，在数据的完整性和速度之间取得一个较好的平衡。

而JFS和XFS，主要用在需要支持大文件的场景中。

**消除文件系统瓶颈的方法**

* 如果程序访问磁盘的方式是顺序访问，那么就换一个更好的磁盘控制器。如果是随机访问的，那么就增加更多的磁盘控制器
* 使用RAID。RAID的读性能比较高，但是写性能低一些。而且，优先使用基于硬件实现的RAID。
* 给磁盘合理分区
* 增加内存
* 通过**/proc/sys/vm/dirty\_background\_ratio**来调整内存中有多少脏数据时，pdflush daemon才将这些数据写入到磁盘
* 通过**ionice**来分配IO操作的优先级：
  * idle: 最低的优先级，只有当没有高优先级的进程访问磁盘时，才有资格访问磁盘
  * Best-effort: 默认优先级。从CPU优先级中继承
  * Real time: 最高的优先级。进程总是能够访问磁盘。
* 禁止access time updates
* 选择合适的文件系统，以及合适的journal模式
* 调整block size:  如果你的服务器，更多的是处理小的文件，那么将block size调小一点，可能会提高性能。但是如果处理大文件更多，那么调大一点可能会提高性能。但是这一项对性能提升并不大，所以，默认使用操作系统的4k的block size就好。

### 网络方面

**网络指标**

* Packets received and sent
* Bytes received and sent
* Collisions per second: 网络中发生的碰撞数量。一个配置正确的网络中，应当很少发生碰撞
* Packet dropped: 被丢弃的包的数量。包括被防火墙过滤掉的，以及由于buffer空间不够而丢掉的
* Overruns: buffer空间溢出的次数
* Errors: 出错的包的数量

**数据传输的过程**

* 应用程序开启一个Socket并将数据写入到这个Socket的buffer中
* 数据经过TCP/IP协议栈一层层地做一些处理，包装。数据并不会层层复制，因为这样性能不好。在内核中，只是修改buffer中的引用，将其传递给下一层
* 数据通过网络到达另一台主机，我们暂且称它为主机B
* 如果这个包的MAC地址就是主机B，那么把它放到主机B的socket buffer中
* 主机B给CPU发出一个硬中断
* 主机B再将数据通过TCP/IP协议栈的层层处理，传递给应用层

Linux中的协议栈，更注重的是可靠性和低延迟，而不是低开销和高吞吐量。

由于每一个数据包都会引发一次中断，所以，Linux中引入了一项叫做NAPI的技术。当第一个数据包到来时，还是跟之前一样，会引发一次中断。但是从此之后，网络接口会启动轮训模式，即，当有数据包到达时，不会发出中断，而是直到buffer都满了的时候，才发出一个中断。这样就能减少中断的次数。

**TCP/IP传输窗口**

TCP/IP传输窗口指的是，在收到ACK响应之前，最多能够发送的数据量。接收主机会通过TCP首部中的**window size**字段告诉发送主机传输窗口的大小。通过使用传输窗口，TCP能够处理地效率更高一些，因为发送主机不需要等待每一个数据包的ACK。

高速网络中，可以使用一种叫做**窗口伸缩**的技术，来增加传输窗口的大小。

**Offload**

如果你的网络适配器支持offload功能，那么你可以内核就可以将一部分工作转移到网络适配器，来减少CPU的工作量，进而提高性能。

常见的offload功能有：

* Checksum Offload: 每一个数据包中，都会有一个校验码，用于验证这个数据包是否在传输过程中出现了问题
* TCP segmentation offload: 当要传输的数据量大于MTU的时候，就要对数据进行分段处理。

**消除网络瓶颈的方法**

* 确保网卡的配置和路由器以及交换机的配置配套
* 调整网络的拓扑结构
* 使用更快的网卡
* 在内核中调整关于网络的参数
  * MTU
  * 接收和发送缓冲区的大小
  * 传输窗口
  * 通过调整**net.ipv4.tcp\_tw\_reuse**参数让处于`TIME_WAIT`状态的Socket对新连接可重用
  * 通过调整**tcp\_fin\_timeout**参数，让处于`FIN-WAIT-2`状态的Socket可以早一些关闭，进而节省内存
  * 通过调整**tcp\_keepalive\_time**参数，调整keepalive连接的关闭时间
  * 通过调整**tcp\_max\_syn\_backlog**参数来调整最大能够容纳的处于半连接状态的socket的数量
* 关闭一些不需要的服务，以及端口号

### Linux的工具

**性能监控工具**

* top
* vmstat
* uptime, w
* ps, pstree
* free
* iostat
* sar
* mpstat
* numastat
* pmap
* netstat
* iptraf
* tcpdump, etheral
* nmon
* strace
* proc file system
* KDE System guard
* Gnome System Monitor

**分析工具**

* lmbench
* iozone
* netperf

**/proc**

**/proc**目录中的内容，对于查看系统状态，应用程序的状态至关重要。

**/proc**目录中，又有这么几块：

* 名称为数字的目录：每一个这样的目录，里面都包含了pid为这个数字的对应的进程的信息，比如，进程使用的虚拟内存
* acpi: ACPI中包含一些高级配置，以及电源管理等信息。因为ACPI主要是用在笔记本，或者个人PC中，所以，在服务器上，一般是禁用的
* bus: 包含了一些和bus相关的信息，比如PCI bus或者USB接口
* irq: 包含和中断相关的信息。每个子目录都对应一种中断。我们可以通过直接修改对应子目录的信息，来将中断绑定到一个CPU上
* net: 包含和网络相关的统计信息
* scsi: 包含和SCSI相关的信息
* sys: 包含和内核相关的参数
* tty: 包含和tty相关的信息

### 从安装Linux就开始调优

考虑下面几个问题：

* 安装什么版本的Linux?
  * 商业版的还是开源版本的？
  * 选择商业版的哪一个版本？
* 选择正确的内核  有这么几种内核。
  * standard: 应用在单处理器上
  * SMP: 支持SMP以及超线程技术。一些实现也支持NUMA.
  * Xen: 包括一个可以在Xen虚拟机上运行的Linux版本
* 如何给磁盘分区？  尽可能使用交换分区而不是交换文件。交换分区相对于交换文件来讲，没有文件系统上的开销。
* 使用什么文件系统？
* 安装时，尽可能少安装包还是安装全部的包？
* 防火墙配置
* SELinux
* Runlevel选择  除非有特别需求，否则服务器上都是使用runlevel 3.

  
  
作者：AlstonWilliams  
链接：https://www.jianshu.com/p/1dfcd9e925a6  
來源：简书  
简书著作权归作者所有，任何形式的转载都请联系作者获得授权并注明出处。

