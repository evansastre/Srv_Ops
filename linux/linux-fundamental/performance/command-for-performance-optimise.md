# Command for performance optimise



## **1,hdparm查看硬度读取速度：**

```text
命令：hdparm -t /dev/sda5
打印：Timing buffered disk reads: 254 MB in 3.01 seconds = 84.34 MB/sec
说明：能够指定具体的哪块硬盘进行查询的哦！
```

## **2,iostat检测磁盘IO情况：**

```text
格式：iostat [ -c | -d ] [ -k ] [ -t ] [ -V ] [ -x [ device ] ] [ interval ]
描述：iostat是I/O statistics（输入/输出统计）的缩写，iostat工具将对系统的磁盘操作活动进行监视。它的特点是汇报磁盘活动统计情况，同时也会汇报出CPU使用情况，同vmstat一样，iostat也有一个弱点，就是它不能对某个进程进行深入分析，仅对系统的整体情况进行分析，每1秒检测统计一次（共5次）。
```

![&#x76D8;&#x70B9;linux&#x7CFB;&#x7EDF;&#x4E2D;&#x7684;12&#x6761;&#x6027;&#x80FD;&#x8C03;&#x4F18;&#x547D;&#x4EE4;&#x3002;&#x76D8;&#x70B9;linux&#x7CFB;&#x7EDF;&#x4E2D;&#x7684;12&#x6761;&#x6027;&#x80FD;&#x8C03;&#x4F18;&#x547D;&#x4EE4;&#x3002;](https://www.linuxprobe.com/wp-content/uploads/2016/04/iostat.png)

> blk\_read/s 每秒读取的数据块数
>
> blk\_wrtn/s 每秒写入的数据块数
>
> blk\_read   表示读取的所有数据块数
>
> blk\_wrtn   表示写入的所有数据块数



相关工具：iotop  iftop vmstat 

## **3,vmstat报告内存以及CPU状况：**

```text
名称：报告虚拟内存的统计信息
格式：vmstat [-n] [延时[次数]]
```

![&#x76D8;&#x70B9;linux&#x7CFB;&#x7EDF;&#x4E2D;&#x7684;12&#x6761;&#x6027;&#x80FD;&#x8C03;&#x4F18;&#x547D;&#x4EE4;&#x3002;&#x76D8;&#x70B9;linux&#x7CFB;&#x7EDF;&#x4E2D;&#x7684;12&#x6761;&#x6027;&#x80FD;&#x8C03;&#x4F18;&#x547D;&#x4EE4;&#x3002;](https://www.linuxprobe.com/wp-content/uploads/2016/04/vmstat.png)

| R: | 运行和等待CPU时间片的进程数。长期大于CPU的个数，代表CPU不足 |
| :--- | :--- |
| B： | 等待资源的进程数，如果等待数量多，问题有可能处在I/O或者内存 |
| Swpd: | 切换到内存交换区的内存大小\[以KB为单位\] |
| free: | 当前空闲的物理内存数量\[以KB为单位\] |
| si: | 由磁盘调入内存 |
| so: | 由内存调入磁盘 |
| bi: | 从块设备读入数据的总量 |
| bo: | 写到块设备的数据总量 |
| bi+bo | 1000 如果超过1000，代表硬盘的读写速度有问题 |
| in: | 在某一时间间隔内观测到的每秒设备中断数\[中断数太多对性能不好\] |
| cs: | 列表示每秒产生的上下文切换次数 |
| us+sy &gt; 80% | 代表CPU资源不足 |
| us: | 用户进程消耗的CPU时间百分比 |
| sy: | 内核进程消耗的CPU时间百分比 |
| id: | CPU处在空闲状态的时间百分比 |
| wa: | IO等待所占用的时间百分比 |
| runq-sz: | 内存中可以运行的进程数 |
| plist-sz: | 系统中活跃的任务个数 |

##  **4,sar检测CPU资源：**

```text
任务计划 /etc/cron.d/sysstat
日志目录 /var/log/sa
查看方法 Sar –q –f /var/log/sa/sa10
```

![&#x76D8;&#x70B9;linux&#x7CFB;&#x7EDF;&#x4E2D;&#x7684;12&#x6761;&#x6027;&#x80FD;&#x8C03;&#x4F18;&#x547D;&#x4EE4;&#x3002;&#x76D8;&#x70B9;linux&#x7CFB;&#x7EDF;&#x4E2D;&#x7684;12&#x6761;&#x6027;&#x80FD;&#x8C03;&#x4F18;&#x547D;&#x4EE4;&#x3002;](https://www.linuxprobe.com/wp-content/uploads/2016/04/sar.png)\*\*\*\*

## **5,lscpu显示CPU信息：**

```text
dmesg 显示出开机启动的信息
 lscpu 显示CPU信息
 lscpu -p 显示CPU对应的节点数
getconf LONG_BIT 获知主机的位数
 getconf -a 查看全部的参数
 /sys/class/dmi/id 可以查看Bios的信息 bios_*
```

## **6,strace显1示程序的调用：**

```text
strace –fc elinks –dump http://localhost
```

## **7,调优硬盘优先写入/读取数据用：**

> ![&#x76D8;&#x70B9;linux&#x7CFB;&#x7EDF;&#x4E2D;&#x7684;12&#x6761;&#x6027;&#x80FD;&#x8C03;&#x4F18;&#x547D;&#x4EE4;&#x3002;&#x76D8;&#x70B9;linux&#x7CFB;&#x7EDF;&#x4E2D;&#x7684;12&#x6761;&#x6027;&#x80FD;&#x8C03;&#x4F18;&#x547D;&#x4EE4;&#x3002;](https://www.linuxprobe.com/wp-content/uploads/2016/04/%E7%A1%AC%E7%9B%98IO%E9%80%9F%E5%BA%A6.png)  
> 预先读取需要写入的量，然后再处理写请求，↑读到的值将会是设置值的一半↑。  
> 设置读取到缓存中的数值越大.写入时就会因为数据量大而速度变慢。
>
> /sys/block/sda/queue/nr\_requests 队列长度越大,硬盘IO速度会提升,但占用内存  
> /sys/block/sda/queue/scheduler 调度算法Noop、anticipatory、deadline、\[cfq\]

##  **8,将Ext3文件系统的日志功能独立：**

> ```text
> 1、创建200M的/dev/sdb1 格式化为ext3
> 2、dumpe2fs /dev/sdb1查看文件系统功能中包含的has_journal
> 3、Tune2fs –O ^has_journal /dev/sdb1 去掉默认原有的日志功能
> 4、再分一个200M的分区./dev/sdb2. 日志卷的block必须等于 /dev/sdb1
> Mke2fs –O journal_dev –b 1024 /dev/sdb2
> 5、将/dev/sdb2作为/dev/sdb1的日志卷.
> Tune2fs –j –J device=/dev/sdb2 /dev/sdb1
> ```

## **9,关闭记录文件系统atime：**

```text
对于网站文件，频繁的修改atime是没有意义的，会影响性能
mount –o remount,noatime DEVICE 即可
```

## **10、修改文件日志的提交时间：**

```text
默认是5秒提交一次日志，修改更长时间可以提高性能，但容易丢失数据。
mount –o remount,commit=15 DEVICE
```

## **11,RAID轮循写入调优,适用于0/5/6：**

> chunk size.轮循一次写入的字节.默认是64K,只要没有写满，就不会移动到下一个设备
>
> 设置在每个硬盘都只写一个文件就切换到下一块硬盘,那么如果都是1K的小文件，就会将系统资源浪费在切换硬盘上
>
> 如果将chunk size的值设置很大，比如100M,那么也就没有了意义，还不如用一块硬盘。
>
> Stripe size.条带大小，并不是有数据就写入,而是设置每次写入的数据量，一般是16K写一次。
>
> 所以.Chunk size\(64K\)/stripe size\(16K\)，也就是说每块硬盘写四次。
>
> ------------------------------------算当前应该把chunk size调成多少------------------------------------
>
> 使用iostat –x查看自开机以来每秒的平均请求数avgrq-sz  
> chunk size = 每秒请求数\*512/1024/磁盘数，取一个最紧接2倍数的整数  
> stride = chunk size /block\(默认是4k\)
>
> 创建raid并设置chunk sinze  
> mdadm –C /dev/md0 –l 0 –n3 –chunk=8 /dev/sdb\[123\]  
> 修改raid  
> mke2fs –j –b 4096 –E stride=2 /dev/md0

## **12,硬盘的block保留数：**

```text
 dumpe2fs /dev/sda1
 tune2fs –m 10 /dev/sda1 保留block百分比
 tune2fs –r 保留block数
 保留的block过少,影响性能,保留的过多又浪费硬盘,默认是5%
 
```

## **13, 调度磁盘io优先级 ionice**

```text
ionice
```

