# tcpdump

1.In the Linux system, how to capture packets according to the following requirements: only filter out the access http service, the target ip is 192.168.0.111, a total of 1000 packets, and saved to the 1.cap file?

```text
tcpdump -nn -s0 host 192.168.0.111 and port 80 -c 1000 -w 1.cap
```

