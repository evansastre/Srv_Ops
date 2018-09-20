# Get counter

```bash
#!/bin/bash
 
####define
#AdminWeb=V-AdminWeb
AdminWeb=T-AdminWeb
#EPO="V-xxxxO"
EPO="T-xxxO"
 
CurDate=$(date  +%Y%m%d)
####check minion return
check_minion_return() {
 
if [[ $Res == *"No response"* ]]; then
        echo $MyServer " No response"
        exit
else
    echo $Res
fi
 
}
 
 
Res=$(salt $AdminWeb cmd.run 'pushd E:\log\ManagementDaemon\ && del counter.7z && 7z a counter.7z counter ')
check_minion_return
Res=$(salt $AdminWeb cp.push 'E:\log\ManagementDaemon\counter.7z')
check_minion_return
Res=$(salt $AdminWeb cmd.run 'pushd E:\log\ManagementDaemon\ && del counter.7z ')
check_minion_return
 
mv -f '/var/cache/salt/master/minions/'$AdminWeb'/files/log/ManagementDaemon/counter.7z' /srv/salt
Res=$(salt $EPO cmd.run 'mkdir C:\Log_to_XX\'$CurDate'\')
check_minion_return
Res=$(salt $EPO cp.get_file salt://counter.7z 'C:\Log_to_XX\'$CurDate'\counter.7z')
check_minion_return
rm -f /srv/salt/counter.7z
 
echo ====================================================================================
```

