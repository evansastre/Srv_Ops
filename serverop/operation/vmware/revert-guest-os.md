# Revert Guest OS

We need to revert all Control Management machines every week, according to our security policy.

1.Log in vSphere Web Client, choose virtual-machine, power off ,Edit Settings, Hard disk → Disk Mode → "Independent- Nonpersistent" → OK

2.\[TopTab\] Monitor，Task&Events, Scheduled Task, Schedule a New Task → Reset → Scheduling options→ Configured Scheduler→ change → set weekly sunday 10:00 PM

3.Disabled windows update.

   Disable service "wuauserv": `sc stop wuauserv & sc wuauserv config start= disabled`

   Set registry: 

`reg add HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\WindowsUpdate\AU /v NoAutoUpdate /t DWORD /d 1 /f` 



