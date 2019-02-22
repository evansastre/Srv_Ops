# Common

1.How to check the NIC traffic in real time? How to view historical NIC traffic?

```text
yum install -y sysstat# install sysstat package, get sar command
sar -n DEV# view NIC traffic, default 10 minutes update
sar -n DEV 1 10# is displayed once in a second, showing a total of 10 times
sar -n DEV -f /var/log/sa/sa22#View the traffic log for the specified date
```

2.Show running process

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



3.Show openning ports

```text
netstat -anlp
nmap 127.0.0.1


#check port 3306
netstat -anlp | grep 3306
lsof -i:3306
telnet 127.0.0.1 3306
nc -vv 127.0.0.1 3306 #netcat: nc

```

4.How to check the network connection status

```text
$netstat -anp 
```

5.Change IP.

```text
vim /etc/sysconfig/network-scripts/ifcft-eth0

#restart NIC
ifdown eth0
ifup eth0

#or restart network service
service network restart
```

6. Set multiple IP in one NIC

```text
#ip1
cat /etc/sysconfig/network-scripts/ifcfg-eth0 

#ip2
cp /etc/sysconfig/network-scripts/ifcfg-eth0 /etc/sysconfig/network-scripts/ifcfg-eth0:1
vim /etc/sysconfig/network-scripts/ifcfg-eth0:1

#restart 
service network restart

```

7.How do I check if a NIC is connected to a switch?

```text
mii-tool eth0 
#or
ethtool eth0
```







