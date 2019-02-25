# Kernel parameter tuning

```text
#add tuning lines in this file
sudo vim /etc/sysctl.conf
#let it work now
sudo /sbin/sysctl -p
```



abi.vsyscall32 = 1  
crypto.fips\_enabled = 0  
debug.exception-trace = 1  
debug.kprobes-optimization = 1  
debug.panic\_on\_rcu\_stall = 0  
dev.cdrom.autoclose = 1  
dev.cdrom.autoeject = 0  
dev.cdrom.check\_media = 0  
dev.cdrom.debug = 0  
dev.cdrom.info = CD-ROM information, Id: cdrom.c 3.20 2003/12/17  
dev.cdrom.info =   
dev.cdrom.info = drive name: sr0  
dev.cdrom.info = drive speed: 1  
dev.cdrom.info = drive \# of slots: 1  
dev.cdrom.info = Can close tray: 1  
dev.cdrom.info = Can open tray: 1  
dev.cdrom.info = Can lock tray: 1  
dev.cdrom.info = Can change speed: 1  
dev.cdrom.info = Can select disk: 0  
dev.cdrom.info = Can read multisession: 1  
dev.cdrom.info = Can read MCN: 1  
dev.cdrom.info = Reports media changed: 1  
dev.cdrom.info = Can play audio: 1  
dev.cdrom.info = Can write CD-R: 1  
dev.cdrom.info = Can write CD-RW: 1  
dev.cdrom.info = Can read DVD: 1  
dev.cdrom.info = Can write DVD-R: 1  
dev.cdrom.info = Can write DVD-RAM: 1  
dev.cdrom.info = Can read MRW: 1  
dev.cdrom.info = Can write MRW: 1  
dev.cdrom.info = Can write RAM: 1  
dev.cdrom.info =   
dev.cdrom.info =   
dev.cdrom.lock = 1  
dev.hpet.max-user-freq = 64  
dev.mac\_hid.mouse\_button2\_keycode = 97  
dev.mac\_hid.mouse\_button3\_keycode = 100  
dev.mac\_hid.mouse\_button\_emulation = 0  
dev.parport.default.spintime = 500  
dev.parport.default.timeslice = 200  
**dev.raid.speed\_limit\_max = 200000 \#RAID最大读取速率，如果RAID性能较高，可以修改此上限来提升IO性能**  
dev.raid.speed\_limit\_min = 1000 \#RAID最小读取速率  
dev.scsi.logging\_level = 0 \#是否开启scsi磁盘的日志功能，一般情况不建议开启  
fs.aio-max-nr = 65536  
fs.aio-nr = 0  
fs.binfmt\_misc.status = enabled  
fs.dentry-state = 23528 10917 45 0 0 0  
fs.dir-notify-enable = 1  
fs.epoll.max\_user\_watches = 411340  
fs.file-max = 197872  
fs.file-nr = 1120 0 197872  
fs.inode-nr = 20574 298  
fs.inode-state = 20574 298 0 0 0 0 0  
fs.inotify.max\_queued\_events = 16384  
fs.inotify.max\_user\_instances = 128  
fs.inotify.max\_user\_watches = 8192  
fs.lease-break-time = 45  
fs.leases-enable = 1  
fs.may\_detach\_mounts = 0  
fs.mount-max = 100000  
fs.mqueue.msg\_default = 10  
fs.mqueue.msg\_max = 10  
fs.mqueue.msgsize\_default = 8192  
fs.mqueue.msgsize\_max = 8192  
fs.mqueue.queues\_max = 256  
fs.nr\_open = 1048576  
fs.overflowgid = 65534  
fs.overflowuid = 65534  
fs.pipe-max-size = 1048576  
fs.pipe-user-pages-hard = 0  
fs.pipe-user-pages-soft = 16384  
fs.protected\_hardlinks = 1  
fs.protected\_symlinks = 1  
fs.quota.allocated\_dquots = 0  
fs.quota.cache\_hits = 0  
fs.quota.drops = 0  
fs.quota.free\_dquots = 0  
fs.quota.lookups = 0  
fs.quota.reads = 0  
fs.quota.syncs = 0  
fs.quota.warnings = 1  
fs.quota.writes = 0  
fs.suid\_dumpable = 0  
kernel.acct = 4 2 30  
kernel.acpi\_video\_flags = 0  
kernel.auto\_msgmni = 1  
kernel.bootloader\_type = 114  
kernel.bootloader\_version = 2  
kernel.cad\_pid = 1  
kernel.cap\_last\_cap = 36  
kernel.compat-log = 1  
kernel.core\_pattern = core  
kernel.core\_pipe\_limit = 0  
kernel.core\_uses\_pid = 1  
kernel.ctrl-alt-del = 0  
kernel.dmesg\_restrict = 0  
kernel.domainname = \(none\)  
kernel.ftrace\_dump\_on\_oops = 0  
kernel.ftrace\_enabled = 1  
kernel.hardlockup\_all\_cpu\_backtrace = 0  
kernel.hardlockup\_panic = 1  
kernel.hostname = example\_server.com \#由此可以看出，主机名是属于内核的  
kernel.hotplug =   
kernel.hung\_task\_check\_count = 4194304  
kernel.hung\_task\_panic = 0  
kernel.hung\_task\_timeout\_secs = 120  
kernel.hung\_task\_warnings = 10  
kernel.io\_delay\_type = 0  
kernel.kexec\_load\_disabled = 0  
kernel.keys.gc\_delay = 300  
kernel.keys.maxbytes = 20000  
kernel.keys.maxkeys = 200  
kernel.keys.persistent\_keyring\_expiry = 259200  
kernel.keys.root\_maxbytes = 25000000  
kernel.keys.root\_maxkeys = 1000000  
kernel.kptr\_restrict = 0  
kernel.max\_lock\_depth = 1024  
kernel.modprobe = /sbin/modprobe  
kernel.modules\_disabled = 0  
kernel.msg\_next\_id = -1  
kernel.msgmax = 8192  
kernel.msgmnb = 16384  
kernel.msgmni = 3958  
kernel.ngroups\_max = 65536  
kernel.nmi\_watchdog = 1  
kernel.ns\_last\_pid = 1651  
kernel.numa\_balancing = 0  
kernel.numa\_balancing\_scan\_delay\_ms = 1000  
kernel.numa\_balancing\_scan\_period\_max\_ms = 60000  
kernel.numa\_balancing\_scan\_period\_min\_ms = 1000  
kernel.numa\_balancing\_scan\_size\_mb = 256  
kernel.numa\_balancing\_settle\_count = 4  
kernel.osrelease = 3.10.0-862.el7.x86\_64  
kernel.ostype = Linux  
kernel.overflowgid = 65534  
kernel.overflowuid = 65534  
kernel.panic = 0  
kernel.panic\_on\_io\_nmi = 0  
kernel.panic\_on\_oops = 1  
kernel.panic\_on\_stackoverflow = 0  
kernel.panic\_on\_unrecovered\_nmi = 0  
kernel.panic\_on\_warn = 0  
kernel.perf\_cpu\_time\_max\_percent = 25  
kernel.perf\_event\_max\_sample\_rate = 100000  
kernel.perf\_event\_mlock\_kb = 516  
kernel.perf\_event\_paranoid = 2  
kernel.pid\_max = 131072  
kernel.poweroff\_cmd = /sbin/poweroff  
kernel.print-fatal-signals = 0  
kernel.printk = 4 4 1 7  
kernel.printk\_delay = 0  
kernel.printk\_ratelimit = 5  
kernel.printk\_ratelimit\_burst = 10  
kernel.pty.max = 4096  
kernel.pty.nr = 1  
kernel.pty.reserve = 1024  
kernel.random.boot\_id = b91ea354-c5d0-4c48-abcd-18da3dcd6741  
kernel.random.entropy\_avail = 978  
kernel.random.poolsize = 4096  
kernel.random.read\_wakeup\_threshold = 64  
kernel.random.urandom\_min\_reseed\_secs = 60  
kernel.random.uuid = 923d2748-02d8-47b8-968d-9c2b7c420bec  
kernel.random.write\_wakeup\_threshold = 896  
kernel.randomize\_va\_space = 2  
kernel.real-root-dev = 0  
kernel.sched\_autogroup\_enabled = 0  
kernel.sched\_cfs\_bandwidth\_slice\_us = 5000  
kernel.sched\_child\_runs\_first = 0  
kernel.sched\_domain.cpu0.domain0.busy\_factor = 32  
kernel.sched\_domain.cpu0.domain0.busy\_idx = 2  
kernel.sched\_domain.cpu0.domain0.cache\_nice\_tries = 1  
kernel.sched\_domain.cpu0.domain0.flags = 559  
kernel.sched\_domain.cpu0.domain0.forkexec\_idx = 0  
kernel.sched\_domain.cpu0.domain0.idle\_idx = 0  
kernel.sched\_domain.cpu0.domain0.imbalance\_pct = 117  
kernel.sched\_domain.cpu0.domain0.max\_interval = 4  
kernel.sched\_domain.cpu0.domain0.max\_newidle\_lb\_cost = 17063  
kernel.sched\_domain.cpu0.domain0.min\_interval = 2  
kernel.sched\_domain.cpu0.domain0.name = MC  
kernel.sched\_domain.cpu0.domain0.newidle\_idx = 0  
kernel.sched\_domain.cpu0.domain0.wake\_idx = 0  
kernel.sched\_domain.cpu1.domain0.busy\_factor = 32  
kernel.sched\_domain.cpu1.domain0.busy\_idx = 2  
kernel.sched\_domain.cpu1.domain0.cache\_nice\_tries = 1  
kernel.sched\_domain.cpu1.domain0.flags = 559  
kernel.sched\_domain.cpu1.domain0.forkexec\_idx = 0  
kernel.sched\_domain.cpu1.domain0.idle\_idx = 0  
kernel.sched\_domain.cpu1.domain0.imbalance\_pct = 117  
kernel.sched\_domain.cpu1.domain0.max\_interval = 4  
kernel.sched\_domain.cpu1.domain0.max\_newidle\_lb\_cost = 1898  
kernel.sched\_domain.cpu1.domain0.min\_interval = 2  
kernel.sched\_domain.cpu1.domain0.name = MC  
kernel.sched\_domain.cpu1.domain0.newidle\_idx = 0  
kernel.sched\_domain.cpu1.domain0.wake\_idx = 0  
kernel.sched\_latency\_ns = 12000000  
kernel.sched\_migration\_cost\_ns = 500000  
kernel.sched\_min\_granularity\_ns = 10000000  
kernel.sched\_nr\_migrate = 32  
kernel.sched\_rr\_timeslice\_ms = 100  
kernel.sched\_rt\_period\_us = 1000000  
kernel.sched\_rt\_runtime\_us = 950000  
kernel.sched\_schedstats = 0  
kernel.sched\_shares\_window\_ns = 10000000  
kernel.sched\_time\_avg\_ms = 1000  
kernel.sched\_tunable\_scaling = 1  
kernel.sched\_wakeup\_granularity\_ns = 15000000  
kernel.sem = 250 32000 32 128  
kernel.sem\_next\_id = -1  
kernel.shm\_next\_id = -1  
kernel.shm\_rmid\_forced = 0  
kernel.shmall = 18446744073692774399  
kernel.shmmax = 18446744073692774399  
kernel.shmmni = 4096  
kernel.softlockup\_all\_cpu\_backtrace = 0  
kernel.softlockup\_panic = 0  
kernel.stack\_tracer\_enabled = 0  
kernel.sysctl\_writes\_strict = 1  
kernel.sysrq = 16  
kernel.tainted = 0  
kernel.threads-max = 15691  
kernel.timer\_migration = 1  
kernel.traceoff\_on\_warning = 0  
kernel.unknown\_nmi\_panic = 0  
kernel.usermodehelper.bset = 4294967295 31  
kernel.usermodehelper.inheritable = 4294967295 31  
kernel.version = \#1 SMP Fri Apr 20 16:44:24 UTC 2018  
kernel.watchdog = 1  
kernel.watchdog\_cpumask = 0-127  
kernel.watchdog\_thresh = 10  
kernel.yama.ptrace\_scope = 0  
net.core.bpf\_jit\_enable = 0  
net.core.busy\_poll = 0  
net.core.busy\_read = 0  
net.core.default\_qdisc = pfifo\_fast  
net.core.dev\_weight = 64  
net.core.dev\_weight\_rx\_bias = 1  
net.core.dev\_weight\_tx\_bias = 1  
net.core.message\_burst = 10  
net.core.message\_cost = 5  
net.core.netdev\_budget = 300  
net.core.netdev\_max\_backlog = 1000 \#网络设备监听队列的最大长度（此值决定了全局并发能力，但不可大过65535，建议值10000）  
net.core.netdev\_rss\_key = 00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00  
net.core.netdev\_tstamp\_prequeue = 1 \#网络设备预置队列序号，意味着从指定值开始顺延序列化  
net.core.optmem\_max = 20480 \#每个套接字所允许的最大缓冲区的大小  
net.core.rmem\_default = 212992 \#网络协议栈默认接收内存  
net.core.rmem\_max = 212992 \#网络协议栈最大接收内存  
net.core.rps\_sock\_flow\_entries = 0  
net.core.somaxconn = 128 \#定义了系统中每一个端口最大的监听队列长度，这是个全局的参数 建议值1280  
net.core.warnings = 1  
net.core.wmem\_default = 212992 \#网络协议栈默认发送内存  
net.core.wmem\_max = 212992 \#网络协议栈最大发送内存  
net.core.xfrm\_acq\_expires = 30  
net.core.xfrm\_aevent\_etime = 10  
net.core.xfrm\_aevent\_rseqth = 2  
net.core.xfrm\_larval\_drop = 1  
net.ipv4.cipso\_cache\_bucket\_size = 10  
net.ipv4.cipso\_cache\_enable = 1  
net.ipv4.cipso\_rbm\_optfmt = 0  
net.ipv4.cipso\_rbm\_strictvalid = 1  
net.ipv4.conf.all.accept\_local = 0 \#是否允许所有接口接收从本机IP地址上发送给本机的数据包  
net.ipv4.conf.all.accept\_redirects = 1 \#是否接收重写过的数据包（用作路由器时默认值为0）  
net.ipv4.conf.all.accept\_source\_route = 0 \#是否接收无源路由的数据包  
net.ipv4.conf.all.arp\_accept = 0 \#默认对不在ARP表中的IP地址发出的APR包的处理方式:0不在ARP表中创建对应IP地址的表项;1在ARP表中创建对应IP地址的表项  
net.ipv4.conf.all.arp\_announce = 0 \#对网络接口上，本地IP地址的发出的，ARP回应，作出相应级别的限制: 确定不同程度的限制,宣布对来自本地源IP地址发出Arp请求的接口  
\#0： 在任意网络接口（eth0,eth1，lo）上的任何本地地址  
\#1：尽量避免不在该网络接口子网段的本地地址做出arp回应. 当发起ARP请求的源IP地址是被设置应该经由路由达到此网络接口的时候很有用.此时会检查来访IP是否为所有接口上的子网段内ip之一.如果改来访IP不属于各个网络接口上的子网段内,那么将采用级别2的方式来进行处理.   
\#2：对查询目标使用最适当的本地地址.在此模式下将忽略这个IP数据包的源地址并尝试选择与能与该地址通信的本地地址.首要是选择所有的网络接口的子网中外出访问子网中包含该目标IP地址的本地地址. 如果没有合适的地址被发现,将选择当前的发送网络接口或其他的有可能接受到该ARP回应的网络接口来进行发送.  
net.ipv4.conf.all.arp\_filter = 0 \# 0：内核设置每个网络接口各自应答其地址上的arp询问。这项看似会错误的设置却经常能非常有效，因为它增加了成功通讯的机会。在Linux主机上，每个IP地址是网络接口独立的，而非一个复合的接口。只有在一些特殊的设置的时候，比如负载均衡的时候会带来麻烦  
\#1：允许多个网络介质位于同一子网段内，每个网络界面依据是否内核指派路由该数据包经过此接口来确认是否回答ARP查询\(这个实现是由来源地址确定路由的时候决定的\),换句话说，允许控制使用某一块网卡（通常是第一块）回应arp询问  
net.ipv4.conf.all.arp\_ignore = 0 \#定义对目标地址为本地IP的ARP询问不同的应答模式（LVS负载均衡时此值需要修改为2）  
\#0：回应任何网络接口上对任何本地IP地址的arp查询请求  
\#1：只回答目标IP地址是来访网络接口本地地址的ARP查询请求  
\#2：只回答目标IP地址是来访网络接口本地地址的ARP查询请求,且来访IP必须在该网络接口的子网段内  
\#3：不回应该网络界面的arp请求，而只对设置的唯一和连接地址做出回应  
\#8：不回应所有（本地地址）的arp查询  
net.ipv4.conf.all.arp\_notify = 0 \#是否开启arp通知链操作：0不做任何操作，1当设备或硬件地址改变时自动产生一个arp请求  
net.ipv4.conf.all.bootp\_relay = 0 \#是否接收源地址为0.a.b.c，目的地址不是本机的数据包，是为了支持bootp服务  
net.ipv4.conf.all.disable\_policy = 0 \#是否禁止internet协议安全性验证  
net.ipv4.conf.all.disable\_xfrm = 0 \#是否禁止internet协议安全性加密  
net.ipv4.conf.all.force\_igmp\_version = 0  
net.ipv4.conf.all.forwarding = 0  
net.ipv4.conf.all.log\_martians = 0 \#是否开启并记录欺骗，源路由和重定向数据包:记录带有不允许的地址的数据报到内核日志中（如果是路由器建议值为1）  
net.ipv4.conf.all.mc\_forwarding = 0 \#是否进行多播路由（只有内核编译有CONFIG\_MROUTE并且有路由服务程序在运行该参数才有效）  
net.ipv4.conf.all.medium\_id = 0 \#用来区分不同媒介.两个网络设备可以使用不同的值,使他们只有其中之一接收到广播包.通常,这个参数被用来配合proxy\_arp实现roxy\_arp的特性即是允许arp报文在两个不同的网络介质中转发.  
\#0：表示各个网络介质接受他们自己介质上的媒介  
\#-1：表示该媒介未知  
net.ipv4.conf.all.promote\_secondaries = 1 \#主备IP地址切换控制机制（建议值1）0当接口的主IP地址被移除时，删除所有次IP地址；1当接口的主IP地址被移除时，将次IP地址提升为主IP地址  
net.ipv4.conf.all.proxy\_arp = 0 \#是否启用arp代理功能  
net.ipv4.conf.all.proxy\_arp\_pvlan = 0 \#回应代理ARP的数据包从接收到此代理ARP请求的网络接口出去  
net.ipv4.conf.all.route\_localnet = 0 \#是否允许外部访问localhost  
net.ipv4.conf.all.rp\_filter = 1 \#是否开启反向路径过滤  
net.ipv4.conf.all.secure\_redirects = 1 \#是否支持安全重定向数据包  
net.ipv4.conf.all.send\_redirects = 1 \#是否发送重定向数据包  
net.ipv4.conf.all.shared\_media = 1 \#发送或接收RFC1620 共享媒体重定向 会覆盖ip\_secure\_redirects的值  
net.ipv4.conf.all.src\_valid\_mark = 0 \#是否为所有接口上源地址有效的数据包打标记  
net.ipv4.conf.all.tag = 0  
net.ipv4.conf.default.accept\_local = 0 \#默认是否允许接收从本机IP地址上发送给本机的数据包  
net.ipv4.conf.default.accept\_redirects = 1 \#默认是否接收重写过的数据包（建议值1）  
net.ipv4.conf.default.accept\_source\_route = 0 \#默认是否接收无源路由的数据包  
net.ipv4.conf.default.arp\_accept = 0  
net.ipv4.conf.default.arp\_announce = 0  
net.ipv4.conf.default.arp\_filter = 0  
net.ipv4.conf.default.arp\_ignore = 0 \#LVS负载均衡需要修改此值为1  
net.ipv4.conf.default.arp\_notify = 0  
net.ipv4.conf.default.bootp\_relay = 0  
net.ipv4.conf.default.disable\_policy = 0  
net.ipv4.conf.default.disable\_xfrm = 0  
net.ipv4.conf.default.force\_igmp\_version = 0  
net.ipv4.conf.default.forwarding = 0  
net.ipv4.conf.default.log\_martians = 0 \#默认是否开启并记录欺骗，源路由和重定向数据包（如果是路由器建议值为1）  
net.ipv4.conf.default.mc\_forwarding = 0  
net.ipv4.conf.default.medium\_id = 0  
net.ipv4.conf.default.promote\_secondaries = 1  
net.ipv4.conf.default.proxy\_arp = 0  
net.ipv4.conf.default.proxy\_arp\_pvlan = 0  
net.ipv4.conf.default.route\_localnet = 0  
net.ipv4.conf.default.rp\_filter = 1 \#默认是否开启反向路径过滤  
net.ipv4.conf.default.secure\_redirects = 1 \#默认是否支持安全重定向数据包  
net.ipv4.conf.default.send\_redirects = 1 \#默认是否发送重定向数据包  
net.ipv4.conf.default.shared\_media = 1  
net.ipv4.conf.default.src\_valid\_mark = 0 \#默认是否为源地址有效的数据包打标记  
net.ipv4.conf.default.tag = 0  
net.ipv4.conf.eth0.accept\_local = 0  
net.ipv4.conf.eth0.accept\_redirects = 1  
net.ipv4.conf.eth0.accept\_source\_route = 0  
net.ipv4.conf.eth0.arp\_accept = 0  
net.ipv4.conf.eth0.arp\_announce = 0  
net.ipv4.conf.eth0.arp\_filter = 0  
net.ipv4.conf.eth0.arp\_ignore = 0  
net.ipv4.conf.eth0.arp\_notify = 0  
net.ipv4.conf.eth0.bootp\_relay = 0  
net.ipv4.conf.eth0.disable\_policy = 0  
net.ipv4.conf.eth0.disable\_xfrm = 0  
net.ipv4.conf.eth0.force\_igmp\_version = 0  
net.ipv4.conf.eth0.forwarding = 0  
net.ipv4.conf.eth0.log\_martians = 0  
net.ipv4.conf.eth0.mc\_forwarding = 0  
net.ipv4.conf.eth0.medium\_id = 0  
net.ipv4.conf.eth0.promote\_secondaries = 1  
net.ipv4.conf.eth0.proxy\_arp = 0  
net.ipv4.conf.eth0.proxy\_arp\_pvlan = 0  
net.ipv4.conf.eth0.route\_localnet = 0  
net.ipv4.conf.eth0.rp\_filter = 1  
net.ipv4.conf.eth0.secure\_redirects = 1  
net.ipv4.conf.eth0.send\_redirects = 1  
net.ipv4.conf.eth0.shared\_media = 1  
net.ipv4.conf.eth0.src\_valid\_mark = 0  
net.ipv4.conf.eth0.tag = 0  
net.ipv4.conf.lo.accept\_local = 0  
net.ipv4.conf.lo.accept\_redirects = 1  
net.ipv4.conf.lo.accept\_source\_route = 1  
net.ipv4.conf.lo.arp\_accept = 0  
net.ipv4.conf.lo.arp\_announce = 0  
net.ipv4.conf.lo.arp\_filter = 0  
net.ipv4.conf.lo.arp\_ignore = 0  
net.ipv4.conf.lo.arp\_notify = 0  
net.ipv4.conf.lo.bootp\_relay = 0  
net.ipv4.conf.lo.disable\_policy = 1  
net.ipv4.conf.lo.disable\_xfrm = 1  
net.ipv4.conf.lo.force\_igmp\_version = 0  
net.ipv4.conf.lo.forwarding = 0  
net.ipv4.conf.lo.log\_martians = 0  
net.ipv4.conf.lo.mc\_forwarding = 0  
net.ipv4.conf.lo.medium\_id = 0  
net.ipv4.conf.lo.promote\_secondaries = 0  
net.ipv4.conf.lo.proxy\_arp = 0  
net.ipv4.conf.lo.proxy\_arp\_pvlan = 0  
net.ipv4.conf.lo.route\_localnet = 0  
net.ipv4.conf.lo.rp\_filter = 0  
net.ipv4.conf.lo.secure\_redirects = 1  
net.ipv4.conf.lo.send\_redirects = 1  
net.ipv4.conf.lo.shared\_media = 1  
net.ipv4.conf.lo.src\_valid\_mark = 0  
net.ipv4.conf.lo.tag = 0  
net.ipv4.fwmark\_reflect = 0  
net.ipv4.icmp\_echo\_ignore\_all = 0  
net.ipv4.icmp\_echo\_ignore\_broadcasts = 1  
net.ipv4.icmp\_errors\_use\_inbound\_ifaddr = 0  
net.ipv4.icmp\_ignore\_bogus\_error\_responses = 1  
net.ipv4.icmp\_msgs\_burst = 50  
net.ipv4.icmp\_msgs\_per\_sec = 1000  
net.ipv4.icmp\_ratelimit = 1000  
net.ipv4.icmp\_ratemask = 6168  
net.ipv4.igmp\_max\_memberships = 20  
net.ipv4.igmp\_max\_msf = 10  
net.ipv4.igmp\_qrv = 2  
net.ipv4.inet\_peer\_maxttl = 600  
net.ipv4.inet\_peer\_minttl = 120  
net.ipv4.inet\_peer\_threshold = 65664  
net.ipv4.ip\_default\_ttl = 64 \#定义数据报的生存周期:最多经过多少路由器后数据将被丢弃  
net.ipv4.ip\_dynaddr = 0  
net.ipv4.ip\_early\_demux = 1  
net.ipv4.ip\_forward = 0 \#是否启用IP转发（如果做路由需要开启此项）  
net.ipv4.ip\_forward\_use\_pmtu = 0 \#是否支持巨型帧转发（使用LVS做负载均衡器时建议此值为1）  
net.ipv4.ip\_local\_port\_range = 32768 60999 \#服务器端可用端口范围（建议值 1024 65535）  
net.ipv4.ip\_local\_reserved\_ports = \#系统预留端口列表：可以防止并发时占用服务端口  
net.ipv4.ip\_no\_pmtu\_disc = 0 \#是否关闭路径MTU探测功能  
net.ipv4.ip\_nonlocal\_bind = 0  
net.ipv4.ipfrag\_high\_thresh = 4194304  
net.ipv4.ipfrag\_low\_thresh = 3145728  
net.ipv4.ipfrag\_max\_dist = 64  
net.ipv4.ipfrag\_secret\_interval = 600  
net.ipv4.ipfrag\_time = 30  
net.ipv4.neigh.default.anycast\_delay = 100  
net.ipv4.neigh.default.app\_solicit = 0  
net.ipv4.neigh.default.base\_reachable\_time\_ms = 30000  
net.ipv4.neigh.default.delay\_first\_probe\_time = 5  
net.ipv4.neigh.default.gc\_interval = 30  
net.ipv4.neigh.default.gc\_stale\_time = 60  
net.ipv4.neigh.default.gc\_thresh1 = 128  
net.ipv4.neigh.default.gc\_thresh2 = 512  
net.ipv4.neigh.default.gc\_thresh3 = 1024  
net.ipv4.neigh.default.locktime = 100  
net.ipv4.neigh.default.mcast\_solicit = 3  
net.ipv4.neigh.default.proxy\_delay = 80  
net.ipv4.neigh.default.proxy\_qlen = 64  
net.ipv4.neigh.default.retrans\_time\_ms = 1000  
net.ipv4.neigh.default.ucast\_solicit = 3  
net.ipv4.neigh.default.unres\_qlen = 31  
net.ipv4.neigh.default.unres\_qlen\_bytes = 65536  
net.ipv4.neigh.eth0.anycast\_delay = 100  
net.ipv4.neigh.eth0.app\_solicit = 0  
net.ipv4.neigh.eth0.base\_reachable\_time\_ms = 30000  
net.ipv4.neigh.eth0.delay\_first\_probe\_time = 5  
net.ipv4.neigh.eth0.gc\_stale\_time = 60  
net.ipv4.neigh.eth0.locktime = 100  
net.ipv4.neigh.eth0.mcast\_solicit = 3  
net.ipv4.neigh.eth0.proxy\_delay = 80  
net.ipv4.neigh.eth0.proxy\_qlen = 64  
net.ipv4.neigh.eth0.retrans\_time\_ms = 1000  
net.ipv4.neigh.eth0.ucast\_solicit = 3  
net.ipv4.neigh.eth0.unres\_qlen = 31  
net.ipv4.neigh.eth0.unres\_qlen\_bytes = 65536  
net.ipv4.neigh.lo.anycast\_delay = 100  
net.ipv4.neigh.lo.app\_solicit = 0  
net.ipv4.neigh.lo.base\_reachable\_time\_ms = 30000  
net.ipv4.neigh.lo.delay\_first\_probe\_time = 5  
net.ipv4.neigh.lo.gc\_stale\_time = 60  
net.ipv4.neigh.lo.locktime = 100  
net.ipv4.neigh.lo.mcast\_solicit = 3  
net.ipv4.neigh.lo.proxy\_delay = 80  
net.ipv4.neigh.lo.proxy\_qlen = 64  
net.ipv4.neigh.lo.retrans\_time\_ms = 1000  
net.ipv4.neigh.lo.ucast\_solicit = 3  
net.ipv4.neigh.lo.unres\_qlen = 31  
net.ipv4.neigh.lo.unres\_qlen\_bytes = 65536  
net.ipv4.ping\_group\_range = 1 0  
net.ipv4.route.error\_burst = 5000  
net.ipv4.route.error\_cost = 1000  
net.ipv4.route.gc\_elasticity = 8  
net.ipv4.route.gc\_interval = 60  
net.ipv4.route.gc\_min\_interval = 0  
net.ipv4.route.gc\_min\_interval\_ms = 500  
net.ipv4.route.gc\_thresh = -1  
net.ipv4.route.gc\_timeout = 300  
net.ipv4.route.max\_size = 2147483647  
net.ipv4.route.min\_adv\_mss = 256  
net.ipv4.route.min\_pmtu = 552  
net.ipv4.route.mtu\_expires = 600  
net.ipv4.route.redirect\_load = 20  
net.ipv4.route.redirect\_number = 9  
net.ipv4.route.redirect\_silence = 20480  
net.ipv4.tcp\_abort\_on\_overflow = 0  
net.ipv4.tcp\_adv\_win\_scale = 1  
net.ipv4.tcp\_allowed\_congestion\_control = cubic reno \#IPV4 TCP允许的拥塞控制算法  
net.ipv4.tcp\_app\_win = 31  
net.ipv4.tcp\_autocorking = 1  
net.ipv4.tcp\_available\_congestion\_control = cubic reno \#内核中可用的TCP拥塞控制算法  
net.ipv4.tcp\_base\_mss = 512  
net.ipv4.tcp\_challenge\_ack\_limit = 1000  
net.ipv4.tcp\_congestion\_control = cubic \#当前正在使用的TCP拥塞控制算法  
net.ipv4.tcp\_dsack = 1 \#是否允许TCP发送“两个完全相同”的SACK  
net.ipv4.tcp\_early\_retrans = 3  
net.ipv4.tcp\_ecn = 2  
net.ipv4.tcp\_fack = 1 \#启用转发应答（Forward Acknowledgment 建议值1），可以进行有选择应答（SACK）从而减少拥塞情况的发生  
net.ipv4.tcp\_fastopen = 0  
net.ipv4.tcp\_fastopen\_key = 00000000-00000000-00000000-00000000  
net.ipv4.tcp\_fin\_timeout = 60 \#server端主动发起断开连接后保持在FIN-WAIT-2状态的时间（建议30s）  
net.ipv4.tcp\_frto = 2  
net.ipv4.tcp\_invalid\_ratelimit = 500 \#无效数据包发送速率时间限制（单位：毫秒）  
net.ipv4.tcp\_keepalive\_intvl = 75 \#探测消息未获得响应时，重发该消息的间隔时间（单位：秒 建议值 30）  
net.ipv4.tcp\_keepalive\_probes = 9 \#在认定TCP连接失效之前，最多发送多少个keepalive探测消息（建议值3）  
net.ipv4.tcp\_keepalive\_time = 7200 \#TCP发送keepalive探测消息的间隔时间（秒），用于确认TCP连接是否有效（建议值1800）  
net.ipv4.tcp\_limit\_output\_bytes = 262144 \#单个套接字限制最大输出字节数（建议保持默认256KB）  
net.ipv4.tcp\_low\_latency = 0 \#是否允许TCP/IP栈适应在高吞吐量情况下低延时的情况（此选项建议为0）  
net.ipv4.tcp\_max\_orphans = 8192 \#允许保留的僵尸套接字的最大值（此值设置过大会给CC×××带来便利）  
net.ipv4.tcp\_max\_ssthresh = 0  
net.ipv4.tcp\_max\_syn\_backlog = 128 \#SYN队列的长度,增大其值可以增大服务器接收并发的能力 （建议值1280）  
net.ipv4.tcp\_max\_tw\_buckets = 8192 \#针对TIME-WAIT数量配置其上限（此值配置太大很容易给CC×××提供便利）  
net.ipv4.tcp\_mem = 45918 61225 91836 \#TCP协议栈缓冲区的最小值、压力值、最大值;高于最大值,TCP拒绝分配socket  
net.ipv4.tcp\_min\_tso\_segs = 2  
net.ipv4.tcp\_moderate\_rcvbuf = 1 \#是否开启TCP缓冲内存自动调整功能  
net.ipv4.tcp\_mtu\_probing = 0 \#是否开启tcp层路径mtu发现  
net.ipv4.tcp\_no\_metrics\_save = 0 \#是否将LAST\_ACK状态保存各种连接信息到路由缓存中：方便下次连接时快速恢复现场  
net.ipv4.tcp\_notsent\_lowat = -1  
net.ipv4.tcp\_orphan\_retries = 0 \#僵尸套接字的重试次数  
net.ipv4.tcp\_reordering = 3  
net.ipv4.tcp\_retrans\_collapse = 1  
net.ipv4.tcp\_retries1 = 3 \#放弃回应一个TCP连接请求前进行重试的次数  
net.ipv4.tcp\_retries2 = 15 \#放弃一个已经建立的TCP连接前进行重试的次数  
net.ipv4.tcp\_rfc1337 = 0  
net.ipv4.tcp\_rmem = 4096 87380 6291456 \#TCP套接字接收缓冲区的最小值、压力值、最大值;高于最大值,TCP拒绝分配socket  
net.ipv4.tcp\_sack = 1 \#是否启用有选择的应答（Selective Acknowledgment 建议值1），使TCP只重新发送交互过程中丢失的包，不用发送后续所有的包，而且提供相应机制使接收方能告诉发送方哪些数据丢失，哪些数据重发了，哪些数据已经提前收到了。如此大大提高了客户端与服务器端数据交互的效率  
net.ipv4.tcp\_slow\_start\_after\_idle = 1 \#拥塞窗口在经过一段时间空闲后是否需要重新初始化（建议值1）  
net.ipv4.tcp\_stdurg = 0  
net.ipv4.tcp\_syn\_retries = 6 \#server主动连接client时发送syn的重试次数（没有特殊需求，建议保持此值）  
net.ipv4.tcp\_synack\_retries = 5 \#server应答client的synack的重试次数  
net.ipv4.tcp\_syncookies = 1 \#是否打开SYN Cookie功能（启用此功能可以防止部分SYN×××）  
net.ipv4.tcp\_thin\_dupack = 0  
net.ipv4.tcp\_thin\_linear\_timeouts = 0  
net.ipv4.tcp\_timestamps = 1 \#是否启用TCP时间戳（会在TCP包头增加12个字节），增加了报文大小，但实现了更好的TCP性能  
net.ipv4.tcp\_tso\_win\_divisor = 3  
net.ipv4.tcp\_tw\_recycle = 0 \#是否快速回收TIME-WAIT套接字，不建议快速回收，但可以reuse,否则NAT环境会有问题  
net.ipv4.tcp\_tw\_reuse = 0 \#是否将处于TIME-WAIT状态的socket（TIME-WAIT的端口）重新用于TCP连接  
net.ipv4.tcp\_window\_scaling = 1 \#要支持超过64KB的TCP窗口，必须启用该值,TCP连接双方都启用时才生效  
net.ipv4.tcp\_wmem = 4096 16384 4194304 \#TCP套接字发送缓冲区的最小值、压力值、最大值;高于最大值,TCP拒绝分配socket  
net.ipv4.tcp\_workaround\_signed\_windows = 0  
net.ipv4.udp\_mem = 47073 62766 94146  
net.ipv4.udp\_rmem\_min = 4096  
net.ipv4.udp\_wmem\_min = 4096  
net.ipv4.xfrm4\_gc\_thresh = 32768  
net.ipv6.anycast\_src\_echo\_reply = 0  
net.ipv6.bindv6only = 0  
net.ipv6.conf.all.accept\_dad = 0  
net.ipv6.conf.all.accept\_ra = 1  
net.ipv6.conf.all.accept\_ra\_defrtr = 1  
net.ipv6.conf.all.accept\_ra\_pinfo = 1  
net.ipv6.conf.all.accept\_ra\_rt\_info\_max\_plen = 0  
net.ipv6.conf.all.accept\_ra\_rtr\_pref = 1  
net.ipv6.conf.all.accept\_redirects = 1  
net.ipv6.conf.all.accept\_source\_route = 0  
net.ipv6.conf.all.autoconf = 1  
net.ipv6.conf.all.dad\_transmits = 1  
net.ipv6.conf.all.disable\_ipv6 = 0 \#是否在所有的网络接口上禁用IPv6（XenServer虚机禁用无效）  
net.ipv6.conf.all.force\_mld\_version = 0  
net.ipv6.conf.all.force\_tllao = 0  
net.ipv6.conf.all.forwarding = 0  
net.ipv6.conf.all.hop\_limit = 64  
net.ipv6.conf.all.max\_addresses = 16  
net.ipv6.conf.all.max\_desync\_factor = 600  
net.ipv6.conf.all.mc\_forwarding = 0  
net.ipv6.conf.all.mldv1\_unsolicited\_report\_interval = 10000  
net.ipv6.conf.all.mldv2\_unsolicited\_report\_interval = 1000  
net.ipv6.conf.all.mtu = 1280  
net.ipv6.conf.all.ndisc\_notify = 0  
net.ipv6.conf.all.optimistic\_dad = 0  
net.ipv6.conf.all.proxy\_ndp = 0  
net.ipv6.conf.all.regen\_max\_retry = 3  
net.ipv6.conf.all.router\_probe\_interval = 60  
net.ipv6.conf.all.router\_solicitation\_delay = 1  
net.ipv6.conf.all.router\_solicitation\_interval = 4  
net.ipv6.conf.all.router\_solicitations = 3  
net.ipv6.conf.all.temp\_prefered\_lft = 86400  
net.ipv6.conf.all.temp\_valid\_lft = 604800  
net.ipv6.conf.all.use\_optimistic = 0  
net.ipv6.conf.all.use\_tempaddr = 0  
net.ipv6.conf.default.accept\_dad = 1  
net.ipv6.conf.default.accept\_ra = 1  
net.ipv6.conf.default.accept\_ra\_defrtr = 1  
net.ipv6.conf.default.accept\_ra\_pinfo = 1  
net.ipv6.conf.default.accept\_ra\_rt\_info\_max\_plen = 0  
net.ipv6.conf.default.accept\_ra\_rtr\_pref = 1  
net.ipv6.conf.default.accept\_redirects = 1  
net.ipv6.conf.default.accept\_source\_route = 0  
net.ipv6.conf.default.autoconf = 1  
net.ipv6.conf.default.dad\_transmits = 1  
net.ipv6.conf.default.disable\_ipv6 = 0 \#默认是否禁用IPv6（用不到IPv6时建议禁用-设定此值为1 （XenServer虚机禁用无效））  
net.ipv6.conf.default.force\_mld\_version = 0  
net.ipv6.conf.default.force\_tllao = 0  
net.ipv6.conf.default.forwarding = 0  
net.ipv6.conf.default.hop\_limit = 64  
net.ipv6.conf.default.max\_addresses = 16  
net.ipv6.conf.default.max\_desync\_factor = 600  
net.ipv6.conf.default.mc\_forwarding = 0  
net.ipv6.conf.default.mldv1\_unsolicited\_report\_interval = 10000  
net.ipv6.conf.default.mldv2\_unsolicited\_report\_interval = 1000  
net.ipv6.conf.default.mtu = 1280  
net.ipv6.conf.default.ndisc\_notify = 0  
net.ipv6.conf.default.optimistic\_dad = 0  
net.ipv6.conf.default.proxy\_ndp = 0  
net.ipv6.conf.default.regen\_max\_retry = 3  
net.ipv6.conf.default.router\_probe\_interval = 60  
net.ipv6.conf.default.router\_solicitation\_delay = 1  
net.ipv6.conf.default.router\_solicitation\_interval = 4  
net.ipv6.conf.default.router\_solicitations = 3  
net.ipv6.conf.default.temp\_prefered\_lft = 86400  
net.ipv6.conf.default.temp\_valid\_lft = 604800  
net.ipv6.conf.default.use\_optimistic = 0  
net.ipv6.conf.default.use\_tempaddr = 0  
net.ipv6.conf.eth0.accept\_dad = 1  
net.ipv6.conf.eth0.accept\_ra = 1  
net.ipv6.conf.eth0.accept\_ra\_defrtr = 1  
net.ipv6.conf.eth0.accept\_ra\_pinfo = 1  
net.ipv6.conf.eth0.accept\_ra\_rt\_info\_max\_plen = 0  
net.ipv6.conf.eth0.accept\_ra\_rtr\_pref = 1  
net.ipv6.conf.eth0.accept\_redirects = 1  
net.ipv6.conf.eth0.accept\_source\_route = 0  
net.ipv6.conf.eth0.autoconf = 1  
net.ipv6.conf.eth0.dad\_transmits = 1  
net.ipv6.conf.eth0.disable\_ipv6 = 0  
net.ipv6.conf.eth0.force\_mld\_version = 0  
net.ipv6.conf.eth0.force\_tllao = 0  
net.ipv6.conf.eth0.forwarding = 0  
net.ipv6.conf.eth0.hop\_limit = 64  
net.ipv6.conf.eth0.max\_addresses = 16  
net.ipv6.conf.eth0.max\_desync\_factor = 600  
net.ipv6.conf.eth0.mc\_forwarding = 0  
net.ipv6.conf.eth0.mldv1\_unsolicited\_report\_interval = 10000  
net.ipv6.conf.eth0.mldv2\_unsolicited\_report\_interval = 1000  
net.ipv6.conf.eth0.mtu = 1500  
net.ipv6.conf.eth0.ndisc\_notify = 0  
net.ipv6.conf.eth0.optimistic\_dad = 0  
net.ipv6.conf.eth0.proxy\_ndp = 0  
net.ipv6.conf.eth0.regen\_max\_retry = 3  
net.ipv6.conf.eth0.router\_probe\_interval = 60  
net.ipv6.conf.eth0.router\_solicitation\_delay = 1  
net.ipv6.conf.eth0.router\_solicitation\_interval = 4  
net.ipv6.conf.eth0.router\_solicitations = 3  
net.ipv6.conf.eth0.temp\_prefered\_lft = 86400  
net.ipv6.conf.eth0.temp\_valid\_lft = 604800  
net.ipv6.conf.eth0.use\_optimistic = 0  
net.ipv6.conf.eth0.use\_tempaddr = 0  
net.ipv6.conf.lo.accept\_dad = -1  
net.ipv6.conf.lo.accept\_ra = 1  
net.ipv6.conf.lo.accept\_ra\_defrtr = 1  
net.ipv6.conf.lo.accept\_ra\_pinfo = 1  
net.ipv6.conf.lo.accept\_ra\_rt\_info\_max\_plen = 0  
net.ipv6.conf.lo.accept\_ra\_rtr\_pref = 1  
net.ipv6.conf.lo.accept\_redirects = 1  
net.ipv6.conf.lo.accept\_source\_route = 0  
net.ipv6.conf.lo.autoconf = 1  
net.ipv6.conf.lo.dad\_transmits = 1  
net.ipv6.conf.lo.disable\_ipv6 = 0 \#是否在lo接口上禁用IPv6 （XenServer虚机禁用无效）  
net.ipv6.conf.lo.force\_mld\_version = 0  
net.ipv6.conf.lo.force\_tllao = 0  
net.ipv6.conf.lo.forwarding = 0  
net.ipv6.conf.lo.hop\_limit = 64  
net.ipv6.conf.lo.max\_addresses = 16  
net.ipv6.conf.lo.max\_desync\_factor = 600  
net.ipv6.conf.lo.mc\_forwarding = 0  
net.ipv6.conf.lo.mldv1\_unsolicited\_report\_interval = 10000  
net.ipv6.conf.lo.mldv2\_unsolicited\_report\_interval = 1000  
net.ipv6.conf.lo.mtu = 65536  
net.ipv6.conf.lo.ndisc\_notify = 0  
net.ipv6.conf.lo.optimistic\_dad = 0  
net.ipv6.conf.lo.proxy\_ndp = 0  
net.ipv6.conf.lo.regen\_max\_retry = 3  
net.ipv6.conf.lo.router\_probe\_interval = 60  
net.ipv6.conf.lo.router\_solicitation\_delay = 1  
net.ipv6.conf.lo.router\_solicitation\_interval = 4  
net.ipv6.conf.lo.router\_solicitations = 3  
net.ipv6.conf.lo.temp\_prefered\_lft = 86400  
net.ipv6.conf.lo.temp\_valid\_lft = 604800  
net.ipv6.conf.lo.use\_optimistic = 0  
net.ipv6.conf.lo.use\_tempaddr = -1  
net.ipv6.fwmark\_reflect = 0  
net.ipv6.icmp.ratelimit = 1000  
net.ipv6.idgen\_delay = 1  
net.ipv6.idgen\_retries = 3  
net.ipv6.ip6frag\_high\_thresh = 4194304  
net.ipv6.ip6frag\_low\_thresh = 3145728  
net.ipv6.ip6frag\_secret\_interval = 600  
net.ipv6.ip6frag\_time = 60  
net.ipv6.ip\_nonlocal\_bind = 0  
net.ipv6.mld\_max\_msf = 64  
net.ipv6.mld\_qrv = 2  
net.ipv6.neigh.default.anycast\_delay = 100  
net.ipv6.neigh.default.app\_solicit = 0  
net.ipv6.neigh.default.base\_reachable\_time\_ms = 30000  
net.ipv6.neigh.default.delay\_first\_probe\_time = 5  
net.ipv6.neigh.default.gc\_interval = 30  
net.ipv6.neigh.default.gc\_stale\_time = 60  
net.ipv6.neigh.default.gc\_thresh1 = 128  
net.ipv6.neigh.default.gc\_thresh2 = 512  
net.ipv6.neigh.default.gc\_thresh3 = 1024  
net.ipv6.neigh.default.locktime = 0  
net.ipv6.neigh.default.mcast\_solicit = 3  
net.ipv6.neigh.default.proxy\_delay = 80  
net.ipv6.neigh.default.proxy\_qlen = 64  
net.ipv6.neigh.default.retrans\_time\_ms = 1000  
net.ipv6.neigh.default.ucast\_solicit = 3  
net.ipv6.neigh.default.unres\_qlen = 31  
net.ipv6.neigh.default.unres\_qlen\_bytes = 65536  
net.ipv6.neigh.eth0.anycast\_delay = 100  
net.ipv6.neigh.eth0.app\_solicit = 0  
net.ipv6.neigh.eth0.base\_reachable\_time\_ms = 30000  
net.ipv6.neigh.eth0.delay\_first\_probe\_time = 5  
net.ipv6.neigh.eth0.gc\_stale\_time = 60  
net.ipv6.neigh.eth0.locktime = 0  
net.ipv6.neigh.eth0.mcast\_solicit = 3  
net.ipv6.neigh.eth0.proxy\_delay = 80  
net.ipv6.neigh.eth0.proxy\_qlen = 64  
net.ipv6.neigh.eth0.retrans\_time\_ms = 1000  
net.ipv6.neigh.eth0.ucast\_solicit = 3  
net.ipv6.neigh.eth0.unres\_qlen = 31  
net.ipv6.neigh.eth0.unres\_qlen\_bytes = 65536  
net.ipv6.neigh.lo.anycast\_delay = 100  
net.ipv6.neigh.lo.app\_solicit = 0  
net.ipv6.neigh.lo.base\_reachable\_time\_ms = 30000  
net.ipv6.neigh.lo.delay\_first\_probe\_time = 5  
net.ipv6.neigh.lo.gc\_stale\_time = 60  
net.ipv6.neigh.lo.locktime = 0  
net.ipv6.neigh.lo.mcast\_solicit = 3  
net.ipv6.neigh.lo.proxy\_delay = 80  
net.ipv6.neigh.lo.proxy\_qlen = 64  
net.ipv6.neigh.lo.retrans\_time\_ms = 1000  
net.ipv6.neigh.lo.ucast\_solicit = 3  
net.ipv6.neigh.lo.unres\_qlen = 31  
net.ipv6.neigh.lo.unres\_qlen\_bytes = 65536  
net.ipv6.route.gc\_elasticity = 9  
net.ipv6.route.gc\_interval = 30  
net.ipv6.route.gc\_min\_interval = 0  
net.ipv6.route.gc\_min\_interval\_ms = 500  
net.ipv6.route.gc\_thresh = 1024  
net.ipv6.route.gc\_timeout = 60  
net.ipv6.route.max\_size = 16384  
net.ipv6.route.min\_adv\_mss = 1220  
net.ipv6.route.mtu\_expires = 600  
net.ipv6.xfrm6\_gc\_thresh = 32768  
net.netfilter.nf\_conntrack\_acct = 0  
net.netfilter.nf\_conntrack\_buckets = 16384  
net.netfilter.nf\_conntrack\_checksum = 1  
net.netfilter.nf\_conntrack\_count = 1  
net.netfilter.nf\_conntrack\_dccp\_loose = 1  
net.netfilter.nf\_conntrack\_dccp\_timeout\_closereq = 64  
net.netfilter.nf\_conntrack\_dccp\_timeout\_closing = 64  
net.netfilter.nf\_conntrack\_dccp\_timeout\_open = 43200  
net.netfilter.nf\_conntrack\_dccp\_timeout\_partopen = 480  
net.netfilter.nf\_conntrack\_dccp\_timeout\_request = 240  
net.netfilter.nf\_conntrack\_dccp\_timeout\_respond = 480  
net.netfilter.nf\_conntrack\_dccp\_timeout\_timewait = 240  
net.netfilter.nf\_conntrack\_events = 1  
net.netfilter.nf\_conntrack\_events\_retry\_timeout = 15  
net.netfilter.nf\_conntrack\_expect\_max = 256  
net.netfilter.nf\_conntrack\_frag6\_high\_thresh = 4194304  
net.netfilter.nf\_conntrack\_frag6\_low\_thresh = 3145728  
net.netfilter.nf\_conntrack\_frag6\_timeout = 60  
net.netfilter.nf\_conntrack\_generic\_timeout = 600  
net.netfilter.nf\_conntrack\_helper = 1  
net.netfilter.nf\_conntrack\_icmp\_timeout = 30  
net.netfilter.nf\_conntrack\_icmpv6\_timeout = 30  
net.netfilter.nf\_conntrack\_log\_invalid = 0  
net.netfilter.nf\_conntrack\_max = 65536  
net.netfilter.nf\_conntrack\_sctp\_timeout\_closed = 10  
net.netfilter.nf\_conntrack\_sctp\_timeout\_cookie\_echoed = 3  
net.netfilter.nf\_conntrack\_sctp\_timeout\_cookie\_wait = 3  
net.netfilter.nf\_conntrack\_sctp\_timeout\_established = 432000  
net.netfilter.nf\_conntrack\_sctp\_timeout\_heartbeat\_acked = 210  
net.netfilter.nf\_conntrack\_sctp\_timeout\_heartbeat\_sent = 30  
net.netfilter.nf\_conntrack\_sctp\_timeout\_shutdown\_ack\_sent = 3  
net.netfilter.nf\_conntrack\_sctp\_timeout\_shutdown\_recd = 0  
net.netfilter.nf\_conntrack\_sctp\_timeout\_shutdown\_sent = 0  
net.netfilter.nf\_conntrack\_tcp\_be\_liberal = 0  
net.netfilter.nf\_conntrack\_tcp\_loose = 1  
net.netfilter.nf\_conntrack\_tcp\_max\_retrans = 3  
net.netfilter.nf\_conntrack\_tcp\_timeout\_close = 10  
net.netfilter.nf\_conntrack\_tcp\_timeout\_close\_wait = 60  
net.netfilter.nf\_conntrack\_tcp\_timeout\_established = 432000  
net.netfilter.nf\_conntrack\_tcp\_timeout\_fin\_wait = 120  
net.netfilter.nf\_conntrack\_tcp\_timeout\_last\_ack = 30  
net.netfilter.nf\_conntrack\_tcp\_timeout\_max\_retrans = 300  
net.netfilter.nf\_conntrack\_tcp\_timeout\_syn\_recv = 60  
net.netfilter.nf\_conntrack\_tcp\_timeout\_syn\_sent = 120  
net.netfilter.nf\_conntrack\_tcp\_timeout\_time\_wait = 120  
net.netfilter.nf\_conntrack\_tcp\_timeout\_unacknowledged = 300  
net.netfilter.nf\_conntrack\_timestamp = 0  
net.netfilter.nf\_conntrack\_udp\_timeout = 30  
net.netfilter.nf\_conntrack\_udp\_timeout\_stream = 180  
net.netfilter.nf\_log.0 = NONE  
net.netfilter.nf\_log.1 = NONE  
net.netfilter.nf\_log.10 = NONE  
net.netfilter.nf\_log.11 = NONE  
net.netfilter.nf\_log.12 = NONE  
net.netfilter.nf\_log.2 = NONE  
net.netfilter.nf\_log.3 = NONE  
net.netfilter.nf\_log.4 = NONE  
net.netfilter.nf\_log.5 = NONE  
net.netfilter.nf\_log.6 = NONE  
net.netfilter.nf\_log.7 = NONE  
net.netfilter.nf\_log.8 = NONE  
net.netfilter.nf\_log.9 = NONE  
net.netfilter.nf\_log\_all\_netns = 0  
net.nf\_conntrack\_max = 65536  
net.unix.max\_dgram\_qlen = 512  
user.max\_ipc\_namespaces = 7845  
user.max\_mnt\_namespaces = 7845  
user.max\_net\_namespaces = 7845  
user.max\_pid\_namespaces = 7845  
user.max\_user\_namespaces = 0  
user.max\_uts\_namespaces = 7845  
vm.admin\_reserve\_kbytes = 8192 \#始终会预留给管理员的内存  
vm.block\_dump = 0  
vm.dirty\_background\_bytes = 0  
vm.dirty\_background\_ratio = 10 \#当系统脏页的比例或者所占内存数量超过 dirty\_background\_ratio\(百分数\)阈值时，启动相关内核线程\(pdflush/flush/kdmflush\)开始将脏页写入磁盘  
vm.dirty\_bytes = 0  
vm.dirty\_expire\_centisecs = 3000 \#声明Linux内核写缓冲区里面的数据多"旧"了之后，pdflush/flush/kdmflush进程就开始考虑写到磁盘中去  
vm.dirty\_ratio = 30 \#当系统pagecache的脏页达到系统内存 dirty\_ratio\(百分数\)阈值时，系统就会阻塞新的写请求,直到脏页被回写到磁盘  
vm.dirty\_writeback\_centisecs = 500 \#内核线程\(pdflush/flush/kdmflush\)多久唤醒一次来检查是否需要将cache中的数据写入磁盘，单位1/100秒  
vm.drop\_caches = 0 \#释放cache，该参数每修改一次，触发一次释放操作（手动释放caches时就需要改变此值）  
vm.extfrag\_threshold = 500  
vm.hugepages\_treat\_as\_movable = 0  
vm.hugetlb\_shm\_group = 0  
vm.laptop\_mode = 0  
vm.legacy\_va\_layout = 0  
vm.lowmem\_reserve\_ratio = 256 256 32  
vm.max\_map\_count = 65530  
vm.memory\_failure\_early\_kill = 0  
vm.memory\_failure\_recovery = 1  
vm.min\_free\_kbytes = 45056 \#系统内核保留内存的最低值  
vm.min\_slab\_ratio = 5  
vm.min\_unmapped\_ratio = 1  
vm.mmap\_min\_addr = 4096  
vm.mmap\_rnd\_bits = 28  
vm.mmap\_rnd\_compat\_bits = 8  
vm.nr\_hugepages = 0 \#控制内存是否可以使用大页面  
vm.nr\_hugepages\_mempolicy = 0  
vm.nr\_overcommit\_hugepages = 0  
vm.nr\_pdflush\_threads = 0  
vm.numa\_zonelist\_order = default  
vm.oom\_dump\_tasks = 1 \#OOM信息打印（建议值1 能够在发生OOM后查看当时情景）  
vm.oom\_kill\_allocating\_task = 0 \#控制是否杀死触发OOM的进程（建议值0 OOM发生时内核自动kill内存占用最多的进程）  
vm.overcommit\_kbytes = 0  
vm.overcommit\_memory = 0 \#控制是否允许超额申请内存  
vm.overcommit\_ratio = 50 \#允许超额申请物理内容+此百分比的swap内存（只有当vm.overcommit\_memory=2时此值才会生效）  
vm.page-cluster = 3 \#控制内核一次从SWAP中连续读取2的多少次幂内存页  
vm.panic\_on\_oom = 0 \#控制内核在OOM时是否panic（恐慌）  
vm.percpu\_pagelist\_fraction = 0  
vm.stat\_interval = 1 \#VM统计信息更新的时间间隔，默认值1s  
vm.swappiness = 30 \#控制物理内存剩余%多少时使用SWAP（建议值0，但0并非禁用SWAP，只是充分利用物理内存）  
vm.user\_reserve\_kbytes = 60940 \#始终会预留给用户空间的内存  
vm.vfs\_cache\_pressure = 100  
vm.zone\_reclaim\_mode = 0  
 

**顺便附上以功能模块归类后的参数调优列表**

**RAID性能参数调优**

dev.raid.speed\_limit\_min = 1000 \#RAID最小读取速率  
dev.raid.speed\_limit\_max = 200000 \#RAID最大读取速率，如果RAID性能较高，可以修改此上限来提升IO性能  
dev.scsi.logging\_level = 0 \#是否开启scsi磁盘的日志功能，一般情况不建议开启  
 

**网络协议栈调整：单位是字节**

net.core.optmem\_max = 20480 \#每个套接字所允许的最大缓冲区的大小  
net.core.rmem\_default = 212992 \#网络协议栈默认接收内存  
net.core.rmem\_max = 212992 \#网络协议栈最大接收内存  
net.core.wmem\_default = 212992 \#网络协议栈默认发送内存  
net.core.wmem\_max = 212992 \#网络协议栈最大发送内存  
net.ipv4.tcp\_moderate\_rcvbuf = 1 \#是否开启TCP缓冲内存自动调整功能  
net.ipv4.tcp\_mem = 45918 61225 91836 \#TCP协议栈缓冲区的最小值、压力值、最大值;高于最大值,TCP拒绝分配socket  
net.ipv4.tcp\_rmem = 4096 87380 6291456 \#TCP套接字接收缓冲区的最小值、压力值、最大值;高于最大值,TCP拒绝分配socket  
net.ipv4.tcp\_wmem = 4096 16384 4194304 \#TCP套接字发送缓冲区的最小值、压力值、最大值;高于最大值,TCP拒绝分配socket  
 

**TCP并发性能优化**

net.core.somaxconn = 1280 \#定义了系统中每一个端口最大的监听队列长度，这是个全局的参数  
net.ipv4.tcp\_max\_syn\_backlog = 1280 \#SYN队列的长度,增大其值可以增大服务器接收并发的能力  
net.ipv4.tcp\_max\_tw\_buckets = 8192 \#针对TIME-WAIT数量配置其上限  
net.ipv4.tcp\_syn\_retries = 6 \#server主动连接client时发送syn的重试次数  
net.ipv4.tcp\_synack\_retries = 5 \#server应答client的synack的重试次数  
net.ipv4.tcp\_fin\_timeout = 30 \#server端主动发起断开连接后保持在FIN-WAIT-2状态的时间  
net.ipv4.tcp\_max\_orphans = 8192 \#允许保留的僵尸套接字的最大值  
net.core.netdev\_max\_backlog = 2000 \#网卡设备将请求放入队列的长度  
net.core.netdev\_tstamp\_prequeue = 1 \#网络设备预置队列序号

net.ipv4.tcp\_tw\_recycle = 0 \#是否需要快速回收TIME-WAIT套接字，不建议快速回收，但可以reuse,否则NAT环境会有问题  
net.ipv4.tcp\_tw\_reuse = 1 \#是否允许将处于TIME-WAIT状态的socket（TIME-WAIT的端口）用于新的TCP连接  
net.ipv4.tcp\_window\_scaling = 1 \#要支持超过64KB的TCP窗口，必须启用该值,TCP连接双方都启用时才生效  
net.ipv4.tcp\_syncookies = 1 \#是否打开SYN Cookie功能，该功能可以防止部分SYN×××  
net.ipv4.tcp\_timestamps = 1 \#是否启用TCP时间戳（会在TCP包头增加12个字节），增加了报文大小，但实现了更好的TCP性能  
 

**对于用不上IPV6的建议直接禁用**

net.ipv6.conf.default.disable\_ipv6 = 1 \#默认是否在lo接口上禁用IPv6 （XenServer虚机禁用无效）  
net.ipv6.conf.all.disable\_ipv6 = 1 \#是否在所有接口上禁用IPv6 （XenServer虚机禁用无效）  
net.ipv6.conf.lo.disable\_ipv6 = 1 \#是否在lo接口上禁用IPv6 （XenServer虚机禁用无效）  
 

**系统端口设定**

net.ipv4.ip\_local\_port\_range = 10000 65535 \#服务器端可用端口范围（建议值 1024 65535）  
net.ipv4.ip\_local\_reserved\_ports = \#系统预留端口列表：可以防止并发时占用服务端口  
 

**TCP丢包重传机制控制，TCP拥塞控制算法对TCP传输速率的影响比较大**

net.ipv4.tcp\_available\_congestion\_control = cubic reno \#内核中可用的TCP拥塞控制算法  
net.ipv4.tcp\_congestion\_control = cubic \#当前正在使用的TCP拥塞控制算法  
net.ipv4.tcp\_allowed\_congestion\_control = cubic reno \#IPV4 TCP允许的拥塞控制算法  
 

**TCP keepalive时长控制**

net.ipv4.tcp\_keepalive\_intvl = 30 \#探测消息未获得响应时，重发该消息的间隔时间（秒）  
net.ipv4.tcp\_keepalive\_probes = 3 \#在认定TCP连接失效之前，最多发送多少个keepalive探测消息  
net.ipv4.tcp\_keepalive\_time = 1800 \#TCP发送keepalive探测消息的间隔时间（秒），用于确认TCP连接是否有效  
 

**memory**

vm.overcommit\_memory = 0 \#控制是否允许超额申请内存  
vm.overcommit\_ratio = 50 \#只有当vm.overcommit\_memory=2时此值才会生效  
vm.page-cluster = 3 \#控制内核一次从SWAP中连续读取2的多少次幂内存页  
vm.panic\_on\_oom = 0 \#控制内核在OOM时是否panic（恐慌）  
vm.stat\_interval = 1 \#VM统计信息更新的时间间隔，默认值1s  
vm.swappiness = 0 \#控制物理内存剩余%多少时使用SWAP（建议值0，但0并非禁用SWAP，只是充分利用物理内存）  
vm.min\_free\_kbytes = 45056 \#系统内核保留内存的最低值  
vm.user\_reserve\_kbytes = 60942 \#始终会预留给用户空间的内存，此处预留60M  
vm.admin\_reserve\_kbytes = 8192 \#始终会预留给管理员的内存，此处预留8M  
 

**OOM控制**

vm.oom\_dump\_tasks = 1 \#OOM信息打印  
vm.oom\_kill\_allocating\_task = 0 \#控制是否杀死触发OOM的进程（建议值0 OOM发生时内核自动kill内存占用最多的进程）  
 

**安全防护模块**

net.ipv4.conf.default.log\_martians = 0 \#默认是否开启并记录欺骗，源路由和重定向数据包（如果是路由器建议值为1）  
net.ipv4.conf.all.log\_martians = 0 \#是否开启并记录欺骗，源路由和重定向数据包:记录带有不允许的地址的数据报到内核日志中（如果是路由器建议值为1）  
net.ipv4.conf.default.accept\_redirects = 1 \#默认是否接收重写过的数据包  
net.ipv4.conf.all.accept\_redirects = 1 \#是否接收重写过的数据包:用作路由器时默认值为0  
net.ipv4.conf.default.accept\_source\_route = 0 \#默认是否接收无源路由的数据包  
net.ipv4.conf.all.accept\_source\_route = 0 \#是否接收无源路由的数据包  
net.ipv4.conf.default.secure\_redirects = 1 \#默认是否支持安全重定向数据包  
net.ipv4.conf.all.secure\_redirects = 1 \#是否支持安全重定向数据包  
net.ipv4.conf.default.rp\_filter = 1 \#默认是否开启反向路径过滤  
net.ipv4.conf.all.rp\_filter = 1 \#是否开启反向路径过滤  
net.ipv4.tcp\_invalid\_ratelimit = 500 \#无效数据包发送速率时间限制（单位：毫秒）  
net.ipv4.tcp\_limit\_output\_bytes = 262144 \#单个套接字限制最大输出字节数  
 

**保障TCP通信质量**

net.ipv4.tcp\_sack = 1 \#是否启用有选择的应答（Selective Acknowledgment），使TCP只重新发送交互过程中丢失的包，不用发送后续所有的包，而且提供相应机制使接收方能告诉发送方哪些数据丢失，哪些数据重发了，哪些数据已经提前收到了。如此大大提高了客户端与服务器端数据交互的效率  
net.ipv4.tcp\_fack = 1 \#启用转发应答（Forward Acknowledgment 建议值1），可以进行有选择应答（SACK）从而减少拥塞情况的发生  
net.ipv4.tcp\_slow\_start\_after\_idle = 1 \#拥塞窗口在经过一段时间空闲后是否需要重新初始化  
net.ipv4.tcp\_stdurg = 0  
net.ipv4.tcp\_retries1 = 3 \#放弃回应一个TCP连接请求前进行重试的次数  
net.ipv4.tcp\_retries2 = 15 \#放弃一个已经建立的TCP连接前进行重试的次数  
net.ipv4.tcp\_rfc1337 = 0  
net.ipv4.tcp\_mtu\_probing = 0 \#是否开启tcp层路径mtu发现  
net.ipv4.tcp\_no\_metrics\_save = 0 \#是否将LAST\_ACK状态保存各种连接信息到路由缓存中：方便下次连接时快速恢复现场  
 

**IO密集性服务器优化参数**

vm.dirty\_expire\_centisecs = 3000 \#声明Linux内核写缓冲区里面的数据多"旧"了之后，pdflush/flush/kdmflush进程就开始考虑写到磁盘中去  
vm.dirty\_background\_ratio = 10 \#当系统脏页的比例或者所占内存数量超过 dirty\_background\_ratio\(百分数\)阈值时，启动相关内核线程\(pdflush/flush/kdmflush\)开始将脏页写入磁盘  
vm.dirty\_ratio = 30 \#当系统pagecache的脏页达到系统内存 dirty\_ratio\(百分数\)阈值时，系统就会阻塞新的写请求,直到脏页被回写到磁盘  
vm.drop\_caches = 0 \#释放cache，该参数每修改一次，触发一次释放操作  
vm.dirty\_writeback\_centisecs = 500 \#内核线程\(pdflush/flush/kdmflush\)多久唤醒一次来检查是否需要将cache中的数据写入磁盘，单位1/100秒  
 

**LVS负载均衡需要修改选项arp\_ignore=1，arp\_announce=2,两项的默认开关不用修改，需要修改all和lo**

net.ipv4.conf.default.arp\_ignore = 0  
net.ipv4.conf.all.arp\_ignore = 0 \#定义对目标地址为本地IP的ARP询问不同的应答模式  
\#0：回应任何网络接口上对任何本地IP地址的arp查询请求  
\#1：只回答目标IP地址是来访网络接口本地地址的ARP查询请求  
\#2：只回答目标IP地址是来访网络接口本地地址的ARP查询请求,且来访IP必须在该网络接口的子网段内   
\#3：不回应该网络界面的arp请求，而只对设置的唯一和连接地址做出回应  
\#8：不回应所有（本地地址）的arp查询  
net.ipv4.conf.lo.arp\_ignore = 0  
net.ipv4.conf.default.arp\_announce = 0  
net.ipv4.conf.all.arp\_announce = 0 \#对网络接口上，本地IP地址的发出的，ARP回应，作出相应级别的限制: 确定不同程度的限制,宣布对来自本地源IP地址发出Arp请求的接口  
\#0： 在任意网络接口（eth0,eth1，lo）上的任何本地地址  
\#1：尽量避免不在该网络接口子网段的本地地址做出arp回应. 当发起ARP请求的源IP地址是被设置应该经由路由达到此网络接口的时候很有用.此时会检查来访IP是否为所有接口上的子网段内ip之一.如果改来访IP不属于各个网络接口上的子网段内,那么将采用级别2的方式来进行处理.   
\#2：对查询目标使用最适当的本地地址.在此模式下将忽略这个IP数据包的源地址并尝试选择与能与该地址通信的本地地址.首要是选择所有的网络接口的子网中外出访问子网中包含该目标IP地址的本地地址. 如果没有合适的地址被发现,将选择当前的发送网络接口或其他的有可能接受到该ARP回应的网络接口来进行发送.  
net.ipv4.conf.lo.arp\_announce = 0  
net.ipv4.ip\_no\_pmtu\_disc = 0 \#是否关闭路径MTU探测功能  
net.ipv4.ip\_forward\_use\_pmtu = 0 \#是否支持巨型帧转发（使用LVS做负载均衡器时建议此值为1）  
net.ipv4.conf.default.arp\_accept = 0  
net.ipv4.conf.all.arp\_accept = 0 \#默认对不在ARP表中的IP地址发出的APR包的处理方式:0不在ARP表中创建对应IP地址的表项;1在ARP表中创建对应IP地址的表项  
net.ipv4.conf.default.arp\_filter = 0  
net.ipv4.conf.all.arp\_filter = 0 \# 0：内核设置每个网络接口各自应答其地址上的arp询问。这项看似会错误的设置却经常能非常有效，因为它增加了成功通讯的机会。在Linux主机上，每个IP地址是网络接口独立的，而非一个复合的接口。只有在一些特殊的设置的时候，比如负载均衡的时候会带来麻烦  
\#1：允许多个网络介质位于同一子网段内，每个网络界面依据是否内核指派路由该数据包经过此接口来确认是否回答ARP查询\(这个实现是由来源地址确定路由的时候决定的\),换句话说，允许控制使用某一块网卡（通常是第一块）回应arp询问  
net.ipv4.conf.default.arp\_notify = 0  
net.ipv4.conf.all.arp\_notify = 0 \#是否开启arp通知链操作：0不做任何操作，1当设备或硬件地址改变时自动产生一个arp请求  
net.ipv4.conf.default.bootp\_relay = 0  
net.ipv4.conf.all.bootp\_relay = 0 \#是否接收源地址为0.a.b.c，目的地址不是本机的数据包，是为了支持bootp服务  
net.ipv4.conf.default.disable\_policy = 0  
net.ipv4.conf.all.disable\_policy = 0 \#是否禁止internet协议安全性验证  
net.ipv4.conf.default.disable\_xfrm = 0  
net.ipv4.conf.all.disable\_xfrm = 0 \#是否禁止internet协议安全性加密  
net.ipv4.conf.default.force\_igmp\_version = 0  
net.ipv4.conf.all.force\_igmp\_version = 0  
 

**路由器选项控制**

net.ipv4.conf.default.forwarding = 0  
net.ipv4.ip\_forward = 0 \#是否启用IP转发  
net.ipv4.conf.all.forwarding = 0 \#是否启用转发功能  
net.ipv4.conf.default.mc\_forwarding = 0  
net.ipv4.conf.all.mc\_forwarding = 0 \#是否进行多播路由（只有内核编译有CONFIG\_MROUTE并且有路由服务程序在运行该参数才有效）  
net.ipv4.conf.default.medium\_id = 0  
net.ipv4.conf.all.medium\_id = 0 \#用来区分不同媒介.两个网络设备可以使用不同的值,使他们只有其中之一接收到广播包.通常,这个参数被用来配合proxy\_arp实现roxy\_arp的特性即是允许arp报文在两个不同的网络介质中转发.  
\#0：表示各个网络介质接受他们自己介质上的媒介  
\#-1：表示该媒介未知  
net.ipv4.conf.default.promote\_secondaries = 1  
net.ipv4.conf.all.promote\_secondaries = 1 \#主备IP地址切换控制机制：0当接口的主IP地址被移除时，删除所有次IP地址；1当接口的主IP地址被移除时，将次IP地址提升为主IP地址  
net.ipv4.conf.default.proxy\_arp = 0  
net.ipv4.conf.all.proxy\_arp = 0 \#是否启用arp代理功能  
net.ipv4.conf.default.proxy\_arp\_pvlan = 0  
net.ipv4.conf.all.proxy\_arp\_pvlan = 0 \#回应代理ARP的数据包从接收到此代理ARP请求的网络接口出去  
net.ipv4.conf.default.route\_localnet = 0  
net.ipv4.conf.all.route\_localnet = 0 \#是否允许外部访问localhost  
net.ipv4.conf.default.shared\_media = 1  
net.ipv4.conf.all.shared\_media = 1 \#发送或接收RFC1620 共享媒体重定向 会覆盖ip\_secure\_redirects的值  
 

**路由机制控制**

net.ipv4.ip\_no\_pmtu\_disc = 0 \#是否关闭路径MTU探测功能  
net.ipv4.ip\_forward\_use\_pmtu = 0 \#是否支持巨型帧转发（使用LVS做负载均衡器时建议此值为1）  
net.ipv4.conf.default.send\_redirects = 1 \#默认是否发送重定向数据包  
net.ipv4.conf.all.send\_redirects = 1 \#是否发送重定向数据包  
net.ipv4.ip\_default\_ttl = 64 \#定义数据报的生存周期:最多经过多少路由器后数据将被丢弃  
net.ipv4.conf.default.src\_valid\_mark = 0 \#默认是否为源地址有效的数据包打标记  
net.ipv4.conf.all.src\_valid\_mark = 0 \#是否为所有接口上源地址有效的数据包打标记  
net.ipv4.conf.default.tag = 0  
net.ipv4.conf.all.tag = 0  
net.ipv4.conf.default.accept\_local = 0 \#默认是否允许接收从本机IP地址上发送给本机的数据包  
net.ipv4.conf.all.accept\_local = 0 \#是否允许所有接口接收从本机IP地址上发送给本机的数据包  
 

**内存大页面使用策略**

vm.nr\_hugepages = 0 \#控制内存是否可以使用大页面  
 

