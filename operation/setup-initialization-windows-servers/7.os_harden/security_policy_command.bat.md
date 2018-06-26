# security\_policy\_command.bat

{% code-tabs %}
{% code-tabs-item title="security\_policy\_command.bat" %}
```bash
:::::::2.1 Remove unnecessary user accounts in administrator group
::net localgroup administrators ::show all users in administrators group 
::net localgroup administrators user1 /delete

::::::::2.2 Disable Guest Account
net user guest /active:no

::::::::2.3 Delete unnecessary account management
::net user ::show all users , then decide which account should be delete
::net user [users] /delete'

::::::::2.9 Change Admin account name
wmic useraccount where name="Administrator" call rename name="Disney"

::::::::2.4 Password Policy Settings
wmic UserAccount where Name="Disney" set PasswordExpires=True
wmic UserAccount where Name="Hollywood" set PasswordExpires=True


net accounts /maxpwage:90
net accounts /minpwage:1
net accounts /minpwlen:8

::::::::2.5 Account lock up policy settings
net accounts /lockoutduration:30
net accounts /lockoutthreshold:5
net accounts /lockoutwindow:30

::::::::2.6 Enforce recent password history settings
net accounts /uniquepw:12

::::::::2.7 Password complexity setting

::::::::2.8 Deactivate encryption settings

::::::::2.10 User Account Control Settings
REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v ConsentPromptBehaviorAdmin /t REG_DWORD /d 5 /f

::::::::2.11 Use vulnerable password
::This one we are using Password Generator, which helps us generate more than 12 length password.

::::::::3.1 user directory access authority setting
icacls C:\Users /remove everyone /T

::::::::3.2 SAM file access authority setting
icacls "C:\windows/system32/config/SAM"
icacls "C:\windows/system32/config/SAM" /remove Users
::icacls "C:\windows/system32/config/SAM" /remove [users or groups]

::::::::3.3 Use system basic public folder
net share C$ /delete
net share IPC$ /delete
net share admin$ /delete
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters /v AutoShareWks /t REG_DWORD /d 0 /f
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters /v AutoShareServer /t REG_DWORD /d 0 /f
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa /v restrictanonymous /t REG_DWORD /d 1 /f

::::::::3.4 User sharing folder setting
::net share --> get list of sharing folders ,remove unnecessary sharing folders. About D E F, maybe can consider only give access to administrators group 
::net share sharename=drive::path /GRANT::user,[READ | CHANGE | FULL] /GRANT::user,[READ | CHANGE | FULL]


::::::::4.1 NetBIOS binding
wmic nicconfig where TcpipNetbiosOptions=0 call SetTcpipNetbios 2
wmic nicconfig where TcpipNetbiosOptions=1 call SetTcpipNetbios 2

::::::::4.2 SMTP replay restriction 
sc stop smtpsvc
sc config "smtpsvc" start= disabled

::::::::4.3 Telnet security setting
sc stop telnet
sc config "telnet" start= disabled

::::::::4.4 SNMP security setting
sc stop SNMPTRAP
sc config "SNMPTRAP" start= disabled

::::::::4.5 Terminal service security setting
REG ADD "HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Terminal Server\WinStations\RDP-Tcp" /v MinEncryptionLevel /t REG_DWORD /d 2 /f

::::::::4.6 Remote terminal access timeout setting
REG ADD "HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Terminal Server\WinStations\RDP-Tcp" /v MaxIdleTime /t REG_DWORD /d 86400000 /f

::::::::4.7 DNS security setting
sc stop dns
sc config "dns" start= disabled

::::::::4.8 DNS Zone Transfer setting
sc stop dns
sc config "dns" start= disabled

::::::::4.9 unnecessary service 
sc stop Alerter
sc config "Alerter" start= disabled
sc stop ClipSrv
sc config "ClipSrv" start= disabled
sc stop Messenger
sc config "Messenger" start= disabled
sc stop simptcp
sc config "simptcp" start= disabled

::::::::5.1 Auto Logon restriction 
REG DELETE "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon" /v DefaultPassword /f
REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon" /v AutoAdminLogon /t REG_DWORD /d 0 /f

::::::5.2 Null Session restriction 
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa /v restrictanonymous /t REG_DWORD /d 1 /f
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa /v restrictanonymoussam /t REG_DWORD /d 1 /f
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters /v restrictnullsessaccess /t REG_DWORD /d 1 /f

::::::::5.3 remote registry access restriction 
sc stop RemoteRegistry
sc config "RemoteRegistry" start= disabled

::::::::5.4 DoS attack defense setting
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v SynAttackProtect /t REG_DWORD /d 2 /f
::Disables dead gateway detection
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v EnableDeadGWDetect /t REG_DWORD /d 0 /f
::Determines how often TCP sends keep-alive transmissions. TCP sends keep-alive transmissions to verify that an idle connection is still active.
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v KeepAliveTime /t REG_DWORD /d 300000 /f
::The NetBIOS name for the system will no longer appear under ‘My Network Places’.
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v NoNameReleaseOnDemand /t REG_DWORD /d 1 /f

::::::::6.1 audit policy setting
AuditPol /Set /Category:"Account Management" /success:enable /failure:enable
AuditPol /Set /Category:"Account Logon" /success:enable /failure:enable
AuditPol /Set /Category:"Privilege Use" /failure:enable
AuditPol /Set /Category:"DS Access" /success:enable /failure:enable
AuditPol /Set /Category:"Logon/Logoff" /success:enable /failure:enable
AuditPol /Set /Category:"Policy change" /success:enable /failure:enable
AuditPol /Set /Category:"System" /success:enable
AuditPol /Set /Category:"Detailed Tracking" /failure:enable
AuditPol /Set /Category:"Object Access" /failure:enable



::::::::6.2 Remote log file access authority setting
icacls C:\Windows\System32\config /remove everyone /T

::::::::6.3 event log setting
::::wevtutil sl Security /ms::83886080
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Eventlog\Security /v MaxSize /t REG_DWORD /d 83886080 /f

::::::::7.1 the last user name display restriction
::default setting is enable
REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v dontdisplaylastusername /t REG_DWORD /d 1 /f

::::::::7.2 Set messagers for users try to logon
REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v legalnoticecaption /t REG_SZ /d warn /f
REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v legalnoticetext /t REG_SZ /d "big brother is watching you" /f


::::::::7.3 Restriction for Forcing to terminate system in remote system 
::import secedit by command

::::::::7.4 restriction for Terminating system without logon
::Default on servers:: Disabled.
REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System\ /v shutdownwithoutlogon /t REG_DWORD /d 0 /f

::::::::7.5 system termination restriction 
::import secedit by command

::::::::7.6 Set popup message to users before password expired.
REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon" /v PasswordExpiryWarning /t REG_DWORD /d 14 /f

::::::::7.7 Do not immediately terminate the system if security audit can’t log 
::Default:: Disabled.
REG ADD "HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Lsa" /v CrashOnAuditFail /t REG_DWORD /d 0 /f

::::::::7.8 LAN MANAGER certification level
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa /v LmCompatibilityLevel /t REG_DWORD /d 3 /f

::::::::7.9 Digital encrypted and signature of security channel
::Default:: Enable
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Netlogon\Parameters /v RequireSignOrSeal /t REG_DWORD /d 1 /f
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Netlogon\Parameters /v SealSecureChannel /t REG_DWORD /d 1 /f
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Netlogon\Parameters /v SignSecureChannel /t REG_DWORD /d 1 /f

::::::::7.10 Required time before session disconnected
::Default::This policy is not defined, which means that the system treats it as 15 minutes for servers and undefined for workstations.
REG ADD "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters Print Services" /v autodisconnect /t REG_DWORD /d 15 /f

::::::::7.11 Removable media format and bringing out restriction 
REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon" /v AllocateDASD /t REG_SZ /d 0 /f

::::::::7.12 Restrict using blank password in local account at local logon
::Default:: Enabled. 
REG ADD "HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Lsa" /v LimitBlankPasswordUse /t REG_DWORD /d 1 /f

::::::::7.13 Allow changing NULL SID/name restriction 
::Default on workstations and member servers:: Disabled.
::import secedit by command

::::::::7.14 Restricting Everyone authority to NULL user
::Default:: Disabled.
REG ADD "HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Lsa" /v EveryoneIncludesAnonymous /t REG_DWORD /d 0 /f

::::::::7.15 computer account password restriction 
REG ADD "HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Netlogon\Parameters" /v DisablePasswordChange /t REG_DWORD /d 0 /f
REG ADD "HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Netlogon\Parameters" /v MaximumPasswordAge /t REG_DWORD /d 90 /f

::::::::7.16 Restriction for user installing printer driver
REG ADD "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Print\Providers\LanMan Print Services" /v AddPrinterDrivers /t REG_DWORD /d 0 /f

:::::::: e2.disable USB on servers
REG ADD "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\USBSTOR" /v Start /t REG_DWORD /d 4 /f

:::::
sc stop WinRM
sc config "WinRM" start= disabled

:::::added2
sc stop SNMP
sc config "SNMP" start= disabled

::import 
secedit /configure /db secedit.sdb /cfg security_policy_infchange.inf



:::::::: e1.MaxIdleTime & MaxConnectionTime

::disconnect after 30min no operate ****** only on CM******

REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services" /v MaxIdleTime /t REG_DWORD /d 1800000 

::1day logoff disconnected user 

::MaxDisconnectionTime
::gpedit.msc -> Compiter Configuration -> Administrative Templates -> Windows Components -> Remote Desktop Services -> Remote Desktop Session Host -> 
::Session Time Limits -> Set time limit for disconnected session -> "Enabled" -> "1 day"

REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services" /v MaxDisConnectionTime /t REG_DWORD /d 86400000 

::MinEncryptionLevel   

::gpedit.msc -> Computer Configuration -> Administrative Templates -> Windows Components -> Remote Desktop Services -> Remote Desktop Session Host -> 
::Security -> Set client connection encryption level -> "Enabled" -> "Client Compatible"

REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services" /v MinEncryptionLevel /t REG_DWORD /d 2
```
{% endcode-tabs-item %}
{% endcode-tabs %}

