# QA

1. Show physical cpu and processor

```text
cat /proc/cpuinfo|grep -c 'physical id'
cat /proc/cpuinfo|grep -c 'processor'
```

2. Show system load

```text
$ w
 04:11:02 up 2 min,  1 user,  load average: 0.05, 0.09, 0.05
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
vagrant  pts/0    gateway          04:09    6.00s  0.01s  0.00s w
$updtime
 04:11:23 up 3 min,  1 user,  load average: 0.04, 0.08, 0.05
 
# load average: 0.04, 0.08, 0.05 means average task number is 1 min 5min 15min
```

3. vmstat

```text
$vmstat
procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st
 2  0      0 310668    948 122128    0    0   280    23  122  546  1  2 96  0  0
 
#r, running, running tasks
#b, blocked, blocked tasks

#si, data read from swap to memory
#so, data read from memory to swap
#bi, data read from block to memory
#bo, data read from memory to block
#i, input
#o, output
#s, swap
#b, block
#Unit:KB
```

4.Different between buffer and cache in linux system.

A: Both buffer and cache are an area in memory. When the CPU needs to write data to disk, because the disk speed is slow, the CPU first stores the data into the buffer, then the CPU performs other tasks, and the data in the buffer is periodically written to Disk; When the CPU needs to read data from the disk, because the disk speed is relatively slow, the data to be used can be stored in the cache in advance, and the CPU takes the data directly from the Cache much faster.

Buffer: Cpu write to disk

Cache:CPU read from disk

5. top

```text
PID USER      PR  NI  VIRT  RES  SHR S %CPU %MEM    TIME+  COMMAND
301 root      20   0     0    0    0 S  0.3  0.0   0:00.08 jbd2/sda3-8
1 root      20   0  2900 1428 1216 S  0.0  0.1   0:01.28 init
2 root      20   0     0    0    0 S  0.0  0.0   0:00.00 kthreadd
3 root      RT   0     0    0    0 S  0.0  0.0   0:00.00 migration/0

#VIRT virtual memory usage
#RES physical memory usage
#SHR shared memory usage
#%MEM memory usage percentage
```

6.Find provider of a tool

```text
$yum whatprovides netstat
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: centos.netonboard.com
 * epel: epel.scopesky.iq
 * extras: centos.gbnetwork.my
 * updates: centos.exabytes.com.my
base/7/x86_64/filelists_db                               | 7.1 MB     00:01
epel/x86_64/filelists_db                                 |  11 MB     00:01
extras/7/x86_64/filelists_db                             | 230 kB     00:00
saltstack-repo/7/x86_64/filelists_db                     |  88 kB     00:00
updates/7/x86_64/filelists_db                            | 1.9 MB     00:00
net-tools-2.0-0.24.20131004git.el7.x86_64 : Basic networking tools
Repo        : base
Matched from:
Filename    : /bin/netstat

#So we can know it's in "net-tools"
$yum install net-tools
```

```

```

















