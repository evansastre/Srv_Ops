# Proxy

1.Proxy require centos7. 

2.Proxy temp open outbound. 

3.Proxy check "/etc/yum.conf"  , enable kernel update, repo useful.

4.Require : rsync

5.Network access: 

```text
GSE to proxy : port TCP:10020,58930,22 UDP:10020,10030 
proxy to GSE : port TCP:48533,58625,58725,58930,10020 UDP:10020,10030 
!proxy to Nginx: port TCP:80 
proxy to proxy : port TCP:58930,10020 UDP:10020,10030

agent to proxy: port TCP:48533,58625,59173,10020 UDP:10020,10030 
proxy to agent: port TCP:60020-60030 UDP：60020-60030 
proxy to agent windows: port TCP:22,139,445,49154(wmiexec)
#open TCP/IP Netbios and its service, 
#check netstat -ano | findstr "139"   (445) 
#admin$ may need
agent to agent: port TCP:60020-60030 UDP：60020-60030 
```

5.Must use root/administrator to install and allow root login

```text
vim /etc/ssh/sshd_config
"PermitRootLogin yes"
service sshd restart
```



