# server Initial

```text
##may need disable firewalld
systemctl stop firewalld
systemctl disable firewalld
systemctl status firewalld

##config iptables 
yum -y install iptables-services
vim /etc/sysconfig/iptables
#add:  
#
systemctl restart iptables
systemctl enable iptables
```

