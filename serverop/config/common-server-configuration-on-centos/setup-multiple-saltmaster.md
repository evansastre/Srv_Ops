# Setup multiple saltmaster

1.Install saltmaster on SaltBak.

```text
sudo yum install https://repo.saltstack.com/yum/redhat/salt-repo-2016.11-2.el7.noarch.rpm
yum clean expire-cache
sudo yum install salt-master
sudo yum install salt-minion
```

2.Copy key from Salt to SaltBak

```text
#login Salt
cd /etc/salt/pki/master
scp master.* user@SaltBak:/home/user
 
 
#login SaltBak
cd /home/user 
cp master.* /etc/salt/pki/master
service salt-master start
```

3.Add new master into minion conf and restart minion

```text
#Linux Server run below script
#!/bin/bash
salt -N 'OS-Linux' cmd.run "sed -i '/^master: 10.*$/a\ \ -\ 10.XX.XX.203' /etc/salt/minion"
salt -N 'OS-Linux' cmd.run "sed -i '/^master: 10.*$/a\ \ -\ 10.XX.XX.196' /etc/salt/minion"
salt -N 'OS-Linux' cmd.run "sed -i 's/^master: 10.*$/master:/g' /etc/salt/minion"
salt -N 'OS-Linux' cmd.run "pkill minion && service salt-minion start"
#salt -N 'OS-Linux' cmd.run "salt-call service.restart salt-minion"

#Windows Server run below script
salt -N 'OS-Windows' cmd.run 'sed -i "/^master: 10.*$/a\ \ -\ 10.XX.XX.203" C:\salt\conf\minion'
salt -N 'OS-Windows' cmd.run 'sed -i "/^master: 10.*$/a\ \ -\ 10.XX.XX.196" C:\salt\conf\minion'
salt -N 'OS-Windows' cmd.run 'sed -i "s/^master: 10.*$/master:/g" C:\salt\conf\minion'
salt -N 'OS-Windows' cmd.run 'C:\salt\salt-call.bat --local service.restart salt-minion'
```







