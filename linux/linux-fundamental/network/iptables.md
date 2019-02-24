# iptables

1.Reject IP from 192.168.1.101 access to local port 80

```text
iptables -I INPUT -s 192.168.1.101 -p tcp --dport 80 -j REJECT
```

2.Save iptable to a file 

```text
iptables-save > 1.ipt
```

Restore from a file

```text
iptables-restore < 1.ipt
```

3.NAT  port 80 to 8080

```text
iptables -t nat -A PREROUTING -d 192.168.16.1 -p tcp --dport 80 -j DNAT --to 192.168.16.1:8080
```



SNAT 

DNAT，

MASQUERADE \(special instance of SNAT, when your IP is dynamic, need use NIC IP instead source IP\)











