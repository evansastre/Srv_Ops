# CPU&Memory



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
$top
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

6.show memory

```text
$free
              total        used        free      shared  buff/cache   available
Mem:         500780       90672      119240        8844      290868      367188
Swap:       1048572           0     1048572
```

7. One day you suddenly found that the company website access speed is very slow and slow, what should you do?

Analyze the system load, use the w command or the uptime command to check the system load. If the load is high, use the top command to check the CPU, MEM, etc., either the CPU is busy or the memory is not enough. Both of them are normal, then use the sar command to analyze the NIC traffic and analyze whether it has been attacked. Once the cause of the problem is analyzed, take corresponding measures to resolve it, such as deciding whether to kill some processes, or prohibiting some access.

8.



