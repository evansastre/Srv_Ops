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

6.How to check the NIC traffic in real time? How to view historical NIC traffic?

```text
yum install -y sysstat# install sysstat package, get sar command
sar -n DEV# view NIC traffic, default 10 minutes update
sar -n DEV 1 10# is displayed once in a second, showing a total of 10 times
sar -n DEV -f /var/log/sa/sa22#View the traffic log for the specified date
```

7.Show running process

```text
$ps -aux
Warning: bad syntax, perhaps a bogus '-'? See /usr/share/doc/procps-3.2.8/FAQ
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.0   2900  1428 ?        Ss   10:43   0:01 /sbin/init
root         2  0.0  0.0      0     0 ?        S    10:43   0:00 [kthreadd]
root         3  0.0  0.0      0     0 ?        S    10:43   0:00 [migration/0]
root         4  0.0  0.0      0     0 ?        S    10:43   0:00 [ksoftirqd/0]

#STAT: S = sleeping , s = main process, Z =zombie process

$ps -elf
F S UID        PID  PPID  C PRI  NI ADDR SZ WCHAN  STIME TTY          TIME CMD
4 S root         1     0  0  80   0 -   725 -      10:43 ?        00:00:01 /sbin/init
1 S root         2     0  0  80   0 -     0 -      10:43 ?        00:00:00 [kthreadd]
1 S root         3     2  0 -40   - -     0 -      10:43 ?        00:00:00 [migration/0]
1 S root         4     2  0  80   0 -     0 -      10:43 ?        00:00:00 [ksoftirqd/0]
1 S root         5     2  0 -40   - -     0 -      10:43 ?        00:00:00 [migration/0]

```

8.



