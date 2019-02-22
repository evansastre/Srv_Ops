# DNS

1. Change DNS config

```text
vim /etc/resolv.conf 
vim  /etc/sysconfig/network-scripts/ifcfg-eth0
```

2.Check dns server

```text
nslookup ipAddr

dig 
```

3. Record

```text
A  hostname to IP, IPv4
AAA  hostname to IP, IPv6
CNAME  domainname1 to domainname2, redirect
MX   mail exchange
```

4.

