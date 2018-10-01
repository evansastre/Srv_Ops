# Notes\_huangsl

ssh -p 36000 shilei@203.117.148.40

 \# root need ssh localhost without password when install blueking

```text
# ssh-keygen -t rsa -f ~/.ssh/my-ssh-key -C root
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
chmod og-wx ~/.ssh/authorized_keys 

chmod 0755 ~               # or chmod g-w ~   
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
vi /etc/ssh/sshd_config
#PubkeyAuthentication yes
#PermitRootLogin yes
sudo service sshd restart
```



1.Change centos firewalld to iptables if needed.

2.Change cloud backend firewall rules to enable http, or enable all.

3.Change "global.env"  export AUTO\_GET\_WANIP=1

