# Service backup -remote

```bash
dateToday=$(date +%Y%m%d)
salt 'TH-DBBS' cmd.run 'netsh advfirewall firewall set rule name="LAN-LIVE-connect-LIVEDB445" new enable=yes'
#salt -N 'TH-Service' cmd.run 'pushd D:\Service && taskkill /F /IM Robocopy.exe'
 
#Test
#dateToday=20180613
#salt -N 'TH-Service' cmd.run 'pushd D:\Service && net use \\10.**.**.**\ServiceBack passwd /user:10.**.**.**\serviceback && robocopy E:\ServiceBack\Service'$dateToday' \\10.**.**.**\ServiceBack\%computername% /mir /np /nfl /ndl'
 
salt -N 'TH-Service' cmd.run 'pushd D:\Service && net use \\10.**.**.**\ServiceBack passwd /user:10.**.**.**\serviceback && robocopy D:\Service \\10.**.**.**\ServiceBack\%computername% /mir /np /nfl /ndl'
 
wait
salt 'TH-DBBS' cmd.run 'echo '$dateToday' >> E:\ServiceBack\update.log'
salt 'TH-DBBS' cmd.run 'netsh advfirewall firewall set rule name="LAN-LIVE-connect-LIVEDB445" new enable=no'
```

