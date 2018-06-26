# security\_policy\_command\_check

```bash
::::::::2.1 Remove unnecessary user accounts in administrator group
::net localgroup administrators' ::show all users in administrators group 
::net localgroup administrators BILLMENG /delete'"

::::::::2.2 Disable Guest Account
#no
salt -N 'OS-Windows' cmd.run 'net user guest | find "active"' 
::::::::2.3 Delete unnecessary account management
::net user' ::show all users , then decide which account should be delete
::net user [users] /delete'

::::::::2.9 Change Admin account name
#yes
salt -N 'OS-Windows' cmd.run 'net user Starbucks | find "active"'

::::::::2.4 Password Policy Settings
salt -N 'OS-Windows' cmd.run 'net user'

#90
salt -N 'OS-Windows' cmd.run 'net accounts | find "Maximum"'
#1
salt -N 'OS-Windows' cmd.run 'net accounts | find "Minimum password age"'
#8
salt -N 'OS-Windows' cmd.run 'net accounts | find "Minimum password length"'

::::::::2.5 Account lock up policy settings
#30
salt -N 'OS-Windows' cmd.run 'net accounts | find "Lockout duration"'
#5
salt -N 'OS-Windows' cmd.run 'net accounts | find "Lockout threshold"'
#30
salt -N 'OS-Windows' cmd.run 'net accounts | find "Lockout observation window"'


::::::::2.6 Enforce recent password history settings
#12
salt -N 'OS-Windows' cmd.run 'net accounts | find "Length of password"'
::::::::2.7 Password complexity setting

::::::::2.8 Deactivate encryption settings



::::::::2.10 User Account Control Settings
#5 or 0x5
salt -N 'OS-Windows' cmd.run 'REG QUERY HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v ConsentPromptBehaviorAdmin '

::::::::2.11 Use vulnerable password
::This one we are using Password Generator, which helps us generate more than 12 length password.

::::::::3.1 user directory access authority setting
#no "everyone"
salt -N 'OS-Windows' cmd.run 'icacls C:\Users ' | find "Everyone"'

::::::::3.2 SAM file access authority setting

#no group "Users"
salt -N 'OS-Windows' cmd.run 'icacls "C:\windows/system32/config/SAM"'  |  find "Users"'
::icacls "C:\windows/system32/config/SAM" /remove [users or groups]

::::::::3.3 Use system basic public folder
#no admin$ \ Drive share
salt -N 'OS-Windows' cmd.run 'net share'

net share IPC$ /delete
net share admin$ /delete
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters /v AutoShareWks /t REG_DWORD /d 0 /f
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters /v AutoShareServer /t REG_DWORD /d 0 /f
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa /v restrictanonymous /t REG_DWORD /d 1 /f

::::::::3.4 User sharing folder setting
::net share --> get list of sharing folders ,remove unnecessary sharing folders. About D E F, maybe can consider only give access to administrators group 
::net share sharename=drive::path /GRANT::user,[READ | CHANGE | FULL] /GRANT::user,[READ | CHANGE | FULL]"


::::::::4.1 NetBIOS binding
#shows long message
salt -N 'OS-Windows' cmd.run 'wmic nicconfig where TcpipNetbiosOptions=2'

#or try to see 0 or 1, "No Instance(s) Avaliable"
salt '*' cmd.run 'wmic nicconfig where TcpipNetbiosOptions=0'
salt '*' cmd.run 'wmic nicconfig where TcpipNetbiosOptions=1'


::::::::4.2 SMTP replay restriction 
#show does not exist
salt -N 'OS-Windows' cmd.run 'sc query "smtpsvc" '

#or
#show stopped
salt -N 'OS-Windows' cmd.run 'sc query "smtpsvc" | find "STATE"' 
#show disabled
salt -N 'OS-Windows' cmd.run 'sc qc "smtpsvc" | find "START_TYPE"'


::::::::4.3 Telnet security setting
#show does not exist
salt -N 'OS-Windows' cmd.run 'sc query "telnet" '

#or
#show stopped
salt -N 'OS-Windows' cmd.run 'sc query "telnet" | find "STATE"' 
#show disabled
salt -N 'OS-Windows' cmd.run 'sc qc "telnet" | find "START_TYPE"'

::::::::4.4 SNMP security setting
show does not exist
salt -N 'OS-Windows' cmd.run 'sc query "SNMPTRAP" '

#or
#show stopped
salt -N 'OS-Windows' cmd.run 'sc query "SNMPTRAP" | find "STATE"' 
#show disabled
salt -N 'OS-Windows' cmd.run 'sc qc "SNMPTRAP" | find "START_TYPE"'

::::::::4.5 Terminal service security setting
#0x2 2
salt -N 'OS-Windows' cmd.run 'REG QUERY "HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Terminal Server\WinStations\RDP-Tcp" /v MinEncryptionLevel'

::::::::4.6 Remote terminal access timeout setting
#0x5265c00 86400000
salt -N 'OS-Windows' cmd.run 'REG QUERY "HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Terminal Server\WinStations\RDP-Tcp" /v MaxIdleTime'


::::::::4.7 DNS security setting
show does not exist
salt -N 'OS-Windows' cmd.run 'sc query "dns" '

#or
#show stopped
salt -N 'OS-Windows' cmd.run 'sc query "dns" | find "STATE"' 
#show disabled
salt -N 'OS-Windows' cmd.run 'sc qc "dns" | find "START_TYPE"'


::::::::4.8 DNS Zone Transfer setting
show does not exist
salt -N 'OS-Windows' cmd.run 'sc query "dns" '

#or
#show stopped
salt -N 'OS-Windows' cmd.run 'sc query "dns" | find "STATE"' 
#show disabled
salt -N 'OS-Windows' cmd.run 'sc qc "dns" | find "START_TYPE"'

::::::::4.9 unnecessary service 
show does not exist
salt -N 'OS-Windows' cmd.run 'sc query "Alerter" '
#or
#show stopped
salt -N 'OS-Windows' cmd.run 'sc query "Alerter" | find "STATE"' 
#show disabled
salt -N 'OS-Windows' cmd.run 'sc qc "Alerter" | find "START_TYPE"'

show does not exist
salt -N 'OS-Windows' cmd.run 'sc query "ClipSrv" '
#or
#show stopped
salt -N 'OS-Windows' cmd.run 'sc query "ClipSrv" | find "STATE"' 
#show disabled
salt -N 'OS-Windows' cmd.run 'sc qc "ClipSrv" | find "START_TYPE"'

show does not exist
salt -N 'OS-Windows' cmd.run 'sc query "Messenger" '
#or
#show stopped
salt -N 'OS-Windows' cmd.run 'sc query "Messenger" | find "STATE"' 
#show disabled
salt -N 'OS-Windows' cmd.run 'sc qc "Messenger" | find "START_TYPE"'

show does not exist
salt -N 'OS-Windows' cmd.run 'sc query "simptcp" '
#or
#show stopped
salt -N 'OS-Windows' cmd.run 'sc query "simptcp" | find "STATE"' 
#show disabled
salt -N 'OS-Windows' cmd.run 'sc qc "simptcp" | find "START_TYPE"'


::::::::5.1 Auto Logon restriction 
#show "unabl to find" 
salt -N 'OS-Windows' cmd.run 'REG QUERY "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon" /v DefaultPassword'
# 0x0
salt -N 'OS-Windows' cmd.run 'REG QUERY "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon" /v AutoAdminLogon'


::::::5.2 Null Session restriction
# 0x1
salt -N 'OS-Windows' cmd.run 'REG QUERY HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa /v restrictanonymous'
# 0x1
salt -N 'OS-Windows' cmd.run 'REG QUERY HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa /v restrictanonymoussam'
# 0x1
salt -N 'OS-Windows' cmd.run 'REG QUERY HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters /v restrictnullsessaccess'

::::::::5.3 remote registry access restriction 
show does not exist
salt -N 'OS-Windows' cmd.run 'sc query "RemoteRegistry" '
#or
#show stopped
salt -N 'OS-Windows' cmd.run 'sc query "RemoteRegistry" | find "STATE"' 
#show disabled
salt -N 'OS-Windows' cmd.run 'sc qc "RemoteRegistry" | find "START_TYPE"'

::::::::5.4 DoS attack defense setting
# 0x2
salt -N 'OS-Windows' cmd.run 'REG QUERY HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v SynAttackProtect'
::Disables dead gateway detection
# 0x0
salt -N 'OS-Windows' cmd.run 'REG QUERY HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v EnableDeadGWDetect'
::Determines how often TCP sends keep-alive transmissions. TCP sends keep-alive transmissions to verify that an idle connection is still active.
# 0x493e0
salt -N 'OS-Windows' cmd.run 'REG QUERY HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v KeepAliveTime'

::The NetBIOS name for the system will no longer appear under ‘My Network Places’.
#0x1
salt -N 'OS-Windows' cmd.run 'REG QUERY HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v NoNameReleaseOnDemand'

:::::::6.1 audit policy setting
# success and failure
salt -N 'OS-Windows' cmd.run 'AuditPol /Get /Category:"Account Management" '
# success and failure
salt -N 'OS-Windows' cmd.run 'AuditPol /Get /Category:"Account Logon" '
#failure
salt -N 'OS-Windows' cmd.run 'AuditPol /Get /Category:"Privilege Use" '
# success and failure
salt -N 'OS-Windows' cmd.run 'AuditPol /Get /Category:"DS Access" '
# success and failure
salt -N 'OS-Windows' cmd.run 'AuditPol /Get /Category:"Logon/Logoff" '
# success and failure
salt -N 'OS-Windows' cmd.run 'AuditPol /Get /Category:"Policy change" '
# success
salt -N 'OS-Windows' cmd.run 'AuditPol /Get /Category:"System" '
# failure
salt -N 'OS-Windows' cmd.run 'AuditPol /Get /Category:"Detailed Tracking" '
# failure
salt -N 'OS-Windows' cmd.run 'AuditPol /Get /Category:"Object Access" '



::::::::6.2 Remote log file access authority setting
#no group 'everyone'
salt -N 'OS-Windows' cmd.run 'icacls C:\Windows\System32\config' | find "Everyone"' 

::::::::6.3 event log setting
::::wevtutil sl Security /ms::83886080
# 0x5000000 83886080
salt -N 'OS-Windows' cmd.run 'REG QUERY HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Eventlog\Security /v MaxSize '


::::::::7.1 the last user name display restriction
::default setting is enable
#0x1
salt -N 'OS-Windows' cmd.run 'REG QUERY HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v dontdisplaylastusername'


::::::::7.2 Set messagers for users try to logon
#warn
salt -N 'OS-Windows' cmd.run 'REG QUERY HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v legalnoticecaption'

#big brother is watching you
salt -N 'OS-Windows' cmd.run 'REG QUERY HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v legalnoticetext'

::::::::7.3 Restriction for Forcing to terminate system in remote system 
::import secedit by command

::::::::7.4 restriction for Terminating system without logon
::Default on servers:: Disabled.
#0x0
salt -N 'OS-Windows' cmd.run 'REG QUERY HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System\ /v shutdownwithoutlogon'


::::::::7.5 system termination restriction 
::import secedit by command

::::::::7.6 Set popup message to users before password expired.
#0xe
salt -N 'OS-Windows' cmd.run 'REG QUERY "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon" /v PasswordExpiryWarning'


::::::::7.7 Do not immediately terminate the system if security audit can’t log 
::Default:: Disabled.
#0x0
salt -N 'OS-Windows' cmd.run 'REG QUERY "HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Lsa" /v CrashOnAuditFail'

::::::::7.8 LAN MANAGER certification level
salt -N 'OS-Windows' cmd.run 'REG QUERY HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa /v LmCompatibilityLevel'

::::::::7.9 Digital encrypted and signature of security channel
::Default:: Enable
#0x1
salt -N 'OS-Windows' cmd.run 'REG QUERY HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Netlogon\Parameters /v RequireSignOrSeal'
#0x1
salt -N 'OS-Windows' cmd.run 'REG QUERY HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Netlogon\Parameters /v SealSecureChannel'
#0x1
salt -N 'OS-Windows' cmd.run 'REG QUERY HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Netlogon\Parameters /v SignSecureChannel'

::::::::7.10 Required time before session disconnected
::Default::This policy is not defined, which means that the system treats it as 15 minutes for servers and undefined for workstations.
#0xf
salt -N 'OS-Windows' cmd.run 'REG QUERY "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters Print Services" /v autodisconnect'


::::::::7.11 Removable media format and bringing out restriction 
#0
salt -N 'OS-Windows' cmd.run 'REG QUERY "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon" /v AllocateDASD'


::::::::7.12 Restrict using blank password in local account at local logon
::Default:: Enabled. 
#0x1
salt -N 'OS-Windows' cmd.run 'REG QUERY "HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Lsa" /v LimitBlankPasswordUse'

::::::::7.13 Allow changing NULL SID/name restriction 
::Default on workstations and member servers:: Disabled.
::import secedit by command

::::::::7.14 Restricting Everyone authority to NULL user
::Default:: Disabled.
#0x0
salt -N 'OS-Windows' cmd.run 'REG QUERY "HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Lsa" /v EveryoneIncludesAnonymous'


::::::::7.15 computer account password restriction 
#0x0
salt -N 'OS-Windows' cmd.run 'REG QUERY "HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Netlogon\Parameters" /v DisablePasswordChange'

#0x5a
salt -N 'OS-Windows' cmd.run 'REG QUERY "HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Netlogon\Parameters" /v MaximumPasswordAge'


::::::::7.16 Restriction for user installing printer driver
#0x0
salt -N 'OS-Windows' cmd.run 'REG QUERY "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Print\Providers\LanMan Print Services" /v AddPrinterDrivers'


::::::::e2 e2.disable USB on servers
#0x4
salt -N 'OS-Windows' cmd.run 'REG QUERY "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\USBSTOR" /v Start'


:::::added1
show does not exist
salt -N 'OS-Windows' cmd.run 'sc query "WinRM" '

#or
#show stopped
salt -N 'OS-Windows' cmd.run 'sc query "WinRM" | find "STATE"' 
#show disabled
salt -N 'OS-Windows' cmd.run 'sc qc "WinRM" | find "START_TYPE"'

:::::added2
show does not exist
salt -N 'OS-Windows' cmd.run 'sc query "SNMP" '

#or
#show stopped
salt -N 'OS-Windows' cmd.run 'sc query "SNMP" | find "STATE"' 
#show disabled
salt -N 'OS-Windows' cmd.run 'sc qc "SNMP" | find "START_TYPE"'

#export 
salt -N 'OS-Windows' cmd.run 'pushd C:\ && secedit /export /cfg newexport.inf'

#0
salt -N 'OS-Windows' cmd.run 'pushd C:\ && find "ClearTextPassword" newexport.inf'
#1
salt -N 'OS-Windows' cmd.run 'pushd C:\ && find "PasswordComplexity" newexport.inf'
#0
salt -N 'OS-Windows' cmd.run 'pushd C:\ && find "LSAAnonymousNameLookup" newexport.inf'
#*S-1-5-32-544
salt -N 'OS-Windows' cmd.run 'pushd C:\ && find "SeRemoteShutdownPrivilege" newexport.inf'
#*S-1-5-32-544
salt -N 'OS-Windows' cmd.run 'pushd C:\ && find "SeShutdownPrivilege" newexport.inf'

#delete exported inf file
salt -N 'OS-Windows' cmd.run 'pushd C:\ && del newexport.inf'



#MaxDisconnectionTime REG_DWORD 0x5265c00 
salt -N OS-Windows cmd.run 'REG QUERY "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services" /v MaxDisconnectionTime '

#MinEncryptionLevel REG_DWORD 0x2 
salt -N OS-Windows cmd.run 'REG QUERY "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services" /v MinEncryptionLevel'
```

