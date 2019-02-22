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

3.















