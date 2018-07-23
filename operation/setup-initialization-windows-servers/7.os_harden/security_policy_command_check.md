# security\_policy\_command\_check

```bash
####2.1 Remove unnecessary user accounts in administrator group, manual confirm

#show all users in administrators group 

salt -N 'OS-Windows' cmd.run 'net localgroup administrators'

#delete
salt -N 'OS-Windows' cmd.run 'net localgroup administrators user1 /delete'"'



#2.2 Disable Guest Account
#no
salt -N 'OS-Windows' cmd.run 'net user guest | find "active"'


####2.3 Delete unnecessary account management
salt -N 'OS-Windows' cmd.run 'net user'

#show all users , then decide which account should be delete
salt -N 'OS-Windows' cmd.run 'net user [users] /delete'



####2.9 Change Admin account name
#yes
salt -N 'OS-Windows' cmd.run 'net user Starbucks | find "active"'



####2.4 Password Policy Settings
salt -N 'OS-Windows' cmd.run 'net user'

#90
salt -N 'OS-Windows' cmd.run 'net accounts | find "Maximum"'
#1
salt -N 'OS-Windows' cmd.run 'net accounts | find "Minimum password age"'
#8
salt -N 'OS-Windows' cmd.run 'net accounts | find "Minimum password length"'



####2.5 Account lock up policy settings
#30
salt -N 'OS-Windows' cmd.run 'net accounts | find "Lockout duration"'
#5
salt -N 'OS-Windows' cmd.run 'net accounts | find "Lockout threshold"'
#30
salt -N 'OS-Windows' cmd.run 'net accounts | find "Lockout observation window"'


####2.6 Enforce recent password history settings
#12
salt -N 'OS-Windows' cmd.run 'net accounts | find "Length of password"'


####2.7 Password complexity setting

#see last title 'security group policy check'



####2.8 Deactivate encryption settings

#see last title 'security group policy check'



####2.10 User Account Control Settings
#5 or 0x5
salt -N 'OS-Windows' cmd.run 'REG QUERY HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v ConsentPromptBehaviorAdmin ' | grep -E ":|REG"



####2.11 Use vulnerable password
#This one we are using Password Generator, which helps us generate more than 12 length password.



####3.1 user directory access authority setting
#no "everyone"
salt -N 'OS-Windows' cmd.run 'icacls C:\Users ' | find "Everyone"'



####3.2 SAM file access authority setting

#no group "Users"
salt -N 'OS-Windows' cmd.run 'icacls "C:\windows/system32/config/SAM"'  |  find "Users"'
#icacls "C:\windows/system32/config/SAM" /remove [users or groups]



####3.3 Use system basic public folder
#no admin$ \ Drive share
salt -N 'OS-Windows' cmd.run 'net share'



####3.4 User sharing folder setting
#net share --> get list of sharing folders ,remove unnecessary sharing folders. About D E F, maybe can consider only give access to administrators group 
#net share sharename=drive:path /GRANT:user,[READ | CHANGE | FULL] /GRANT:user,[READ | CHANGE | FULL]"


####4.1 NetBIOS binding
#shows long message
salt -N 'OS-Windows' cmd.run 'wmic nicconfig where TcpipNetbiosOptions=2'

#or try to see 0 or 1, "No Instance(s) Avaliable"
salt -N 'OS-Windows' cmd.run 'wmic nicconfig where TcpipNetbiosOptions=0'
salt -N 'OS-Windows' cmd.run 'wmic nicconfig where TcpipNetbiosOptions=1'


####4.2 SMTP replay restriction 
#show does not exist
salt -N 'OS-Windows' cmd.run 'sc query "smtpsvc" '

#or
#show stopped
salt -N 'OS-Windows' cmd.run 'sc query "smtpsvc" | find "STATE"' 
#show disabled
salt -N 'OS-Windows' cmd.run 'sc qc "smtpsvc" | find "START_TYPE"'


####4.3 Telnet security setting
#show does not exist
salt -N 'OS-Windows' cmd.run 'sc query "telnet" '

#or
#show stopped
salt -N 'OS-Windows' cmd.run 'sc query "telnet" | find "STATE"' 
#show disabled
salt -N 'OS-Windows' cmd.run 'sc qc "telnet" | find "START_TYPE"'



####4.4 SNMP security setting
show does not exist
salt -N 'OS-Windows' cmd.run 'sc query "SNMPTRAP" '

#or
#show stopped
salt -N 'OS-Windows' cmd.run 'sc query "SNMPTRAP" | find "STATE"' 
#show disabled
salt -N 'OS-Windows' cmd.run 'sc qc "SNMPTRAP" | find "START_TYPE"'



####4.5 Terminal service security setting
#0x2 2
salt -N 'OS-Windows' cmd.run 'REG QUERY "HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Terminal Server\WinStations\RDP-Tcp" /v MinEncryptionLevel' | grep -E ":|REG"



####4.6 Remote terminal access timeout setting
#0x5265c00 86400000
salt -N 'OS-Windows' cmd.run 'REG QUERY "HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Terminal Server\WinStations\RDP-Tcp" /v MaxIdleTime' | grep -E ":|REG"


####4.7 DNS security setting
show does not exist
salt -N 'OS-Windows' cmd.run 'sc query "dns" '

#or
#show stopped
salt -N 'OS-Windows' cmd.run 'sc query "dns" | find "STATE"' 
#show disabled
salt -N 'OS-Windows' cmd.run 'sc qc "dns" | find "START_TYPE"'


####4.8 DNS Zone Transfer setting
show does not exist
salt -N 'OS-Windows' cmd.run 'sc query "dns" '

#or
#show stopped
salt -N 'OS-Windows' cmd.run 'sc query "dns" | find "STATE"' 
#show disabled
salt -N 'OS-Windows' cmd.run 'sc qc "dns" | find "START_TYPE"'



####4.9 unnecessary service 
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


####5.1 Auto Logon restriction 
#show "unabl to find" 
salt -N 'OS-Windows' cmd.run 'REG QUERY "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon" /v DefaultPassword' | grep -E ":|REG"
# 0x0
salt -N 'OS-Windows' cmd.run 'REG QUERY "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon" /v AutoAdminLogon' | grep -E ":|REG"


###5.2 Null Session restriction
# 0x1
salt -N 'OS-Windows' cmd.run 'REG QUERY HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa /v restrictanonymous' | grep -E ":|REG"
# 0x1
salt -N 'OS-Windows' cmd.run 'REG QUERY HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa /v restrictanonymoussam' | grep -E ":|REG"
# 0x1
salt -N 'OS-Windows' cmd.run 'REG QUERY HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters /v restrictnullsessaccess' | grep -E ":|REG"



####5.3 remote registry access restriction 
show does not exist
salt -N 'OS-Windows' cmd.run 'sc query "RemoteRegistry" '
#or
#show stopped
salt -N 'OS-Windows' cmd.run 'sc query "RemoteRegistry" | find "STATE"' 
#show disabled
salt -N 'OS-Windows' cmd.run 'sc qc "RemoteRegistry" | find "START_TYPE"'



####5.4 DoS attack defense setting
# 0x2
salt -N 'OS-Windows' cmd.run 'REG QUERY HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v SynAttackProtect' | grep -E ":|REG"
#Disables dead gateway detection
# 0x0
salt -N 'OS-Windows' cmd.run 'REG QUERY HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v EnableDeadGWDetect' | grep -E ":|REG"
#Determines how often TCP sends keep-alive transmissions. TCP sends keep-alive transmissions to verify that an idle connection is still active.
# 0x493e0
salt -N 'OS-Windows' cmd.run 'REG QUERY HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v KeepAliveTime' | grep -E ":|REG"

#The NetBIOS name for the system will no longer appear under ‘My Network Places’.
#0x1
salt -N 'OS-Windows' cmd.run 'REG QUERY HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v NoNameReleaseOnDemand' | grep -E ":|REG"



###:6.1 audit policy setting
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



####6.2 Remote log file access authority setting
#no group 'everyone'
salt -N 'OS-Windows' cmd.run 'icacls C:\Windows\System32\config' | find "Everyone"' 

####6.3 event log setting
# 0x5000000 83886080
salt -N 'OS-Windows' cmd.run 'REG QUERY HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Eventlog\Security /v MaxSize ' | grep -E ":|REG"


####7.1 the last user name display restriction
#default setting is enable
#0x1
salt -N 'OS-Windows' cmd.run 'REG QUERY HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v dontdisplaylastusername' | grep -E ":|REG"


####7.2 Set messagers for users try to logon
#warn
salt -N 'OS-Windows' cmd.run 'REG QUERY HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v legalnoticecaption' | grep -E ":|REG"

#big brother is watching you
salt -N 'OS-Windows' cmd.run 'REG QUERY HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v legalnoticetext' | grep -E ":|REG"



####7.3 Restriction for Forcing to terminate system in remote system 
#see last title 'security group policy check'



####7.4 restriction for Terminating system without logon
#Default on servers:Disabled
#0x0
salt -N 'OS-Windows' cmd.run 'REG QUERY HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System\ /v shutdownwithoutlogon' | grep -E ":|REG"


####7.5 system termination restriction 
#see last title 'security group policy check'



####7.6 Set popup message to users before password expired.
#0xe
salt -N 'OS-Windows' cmd.run 'REG QUERY "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon" /v PasswordExpiryWarning' | grep -E ":|REG"


####7.7 Do not immediately terminate the system if security audit can’t log 
#Default: Disabled.
#0x0
salt -N 'OS-Windows' cmd.run 'REG QUERY "HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Lsa" /v CrashOnAuditFail' | grep -E ":|REG"



####7.8 LAN MANAGER certification level
salt -N 'OS-Windows' cmd.run 'REG QUERY HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa /v LmCompatibilityLevel' | grep -E ":|REG"



####7.9 Digital encrypted and signature of security channel
#Default:Enable
#0x1
salt -N 'OS-Windows' cmd.run 'REG QUERY HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Netlogon\Parameters /v RequireSignOrSeal' | grep -E ":|REG"
#0x1
salt -N 'OS-Windows' cmd.run 'REG QUERY HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Netlogon\Parameters /v SealSecureChannel' | grep -E ":|REG"
#0x1
salt -N 'OS-Windows' cmd.run 'REG QUERY HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Netlogon\Parameters /v SignSecureChannel' | grep -E ":|REG"



####7.10 Required time before session disconnected
#Default:This policy is not defined, which means that the system treats it as 15 minutes for servers and undefined for workstations.
#0xf
salt -N 'OS-Windows' cmd.run 'REG QUERY "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters Print Services" /v autodisconnect' | grep -E ":|REG"


####7.11 Removable media format and bringing out restriction 
#0
salt -N 'OS-Windows' cmd.run 'REG QUERY "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon" /v AllocateDASD' | grep -E ":|REG"


####7.12 Restrict using blank password in local account at local logon
#Default: Enabled
#0x1
salt -N 'OS-Windows' cmd.run 'REG QUERY "HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Lsa" /v LimitBlankPasswordUse' | grep -E ":|REG"



####7.13 Allow changing NULL SID/name restriction 
#Default on workstations and member servers: Disabled.
#see last title 'security group policy check'



####7.14 Restricting Everyone authority to NULL user
#Default: Disabled.
#0x0
salt -N 'OS-Windows' cmd.run 'REG QUERY "HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Lsa" /v EveryoneIncludesAnonymous' | grep -E ":|REG"


####7.15 computer account password restriction 
#0x0
salt -N 'OS-Windows' cmd.run 'REG QUERY "HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Netlogon\Parameters" /v DisablePasswordChange' | grep -E ":|REG"

#0x5a
salt -N 'OS-Windows' cmd.run 'REG QUERY "HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Netlogon\Parameters" /v MaximumPasswordAge' | grep -E ":|REG"


####7.16 Restriction for user installing printer driver
#0x0
salt -N 'OS-Windows' cmd.run 'REG QUERY "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Print\Providers\LanMan Print Services" /v AddPrinterDrivers' | grep -E ":|REG"



####e1.MaxIdleTime & MaxConnectionTime

#0x1b7740   disconnect after 30min no operate [only on CM]

salt -N OS-Windows cmd.run 'REG QUERY "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services" /v MaxIdleTime' | grep -E ":|REG"



#0x5265c00 1day logoff disconnected user [ logD0* exclude ]
salt -N OS-Windows cmd.run 'REG QUERY "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services" /v MaxDisconnectionTime ' | grep -E ":|REG"



####e2.disable USB on servers
#0x4
salt -N 'OS-Windows' cmd.run 'REG QUERY "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\USBSTOR" /v Start' | grep -E ":|REG"



#### e3.disable all disconnected network interface

salt '*' cmd.run ' netsh interface show interface | find "Disconnected" ' #check all "Disconnected" is "Disabled"





#### e4.disable all DB server external interface

salt -N DB cmd.run ' ipconfig /all | findstr "IPv4" '   #check no external IP exsit



#### e5.MinEncryptionLevel   

#gpedit.msc -> Computer Configuration -> Administrative Templates -> Windows Components -> Remote Desktop Services -> Remote Desktop Session Host -> Security -> Set client connection encryption level -> "Enabled" -> "Client Compatible"

#0x2   MinEncryptionLevel REG_DWORD   [ logD0* exclude ]
salt -N OS-Windows cmd.run 'REG QUERY "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services" /v MinEncryptionLevel' | grep -E ":|REG"


####:added1
show does not exist
salt -N 'OS-Windows' cmd.run 'sc query "WinRM" '

#or
#show stopped
salt -N 'OS-Windows' cmd.run 'sc query "WinRM" | find "STATE"' 
#show disabled
salt -N 'OS-Windows' cmd.run 'sc qc "WinRM" | find "START_TYPE"'



####:added2
show does not exist
salt -N 'OS-Windows' cmd.run 'sc query "SNMP" '

#or
#show stopped
salt -N 'OS-Windows' cmd.run 'sc query "SNMP" | find "STATE"' 
#show disabled
salt -N 'OS-Windows' cmd.run 'sc qc "SNMP" | find "START_TYPE"'



####security group policy check

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




```

