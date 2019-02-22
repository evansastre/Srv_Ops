# route

The network address of the local area network is 192.168.1.0/24, and the gateway address of the local area network to connect to other networks is 192.168.1.1. When the host 192.168.1.20 accesses the 172.16.1.0/24 network.

```text
route add –net 172.16.1.0 gw 192.168.1.1 netmask 255.255.255.0 metric 1
```



