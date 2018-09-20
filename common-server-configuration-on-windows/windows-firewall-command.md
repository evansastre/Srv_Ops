# Windows Firewall Command



Turn on windows firewall:

| `NetSh Advfirewall set allprofiles state on` |
| :--- |


Turn off windows firewall:

| `NetSh Advfirewall set allprofiles state off` |
| :--- |


Check the status of Windows firewall:

| `Netsh Advfirewall show allprofiles` |
| :--- |


Disable rule:

| `netsh advfirewall firewall set rule name="xxxx"` `new` `enable=no` |
| :--- |


Enable rule:

| `netsh advfirewall firewall set rule name="xxxx"` `new` `enable=yes` |
| :--- |


Block inbound/outbound

```bash
netsh advfirewall set domainprofile firewallpolicy blockinbound,blockoutbound
netsh advfirewall set privateprofile firewallpolicy blockinbound,blockoutbound
netsh advfirewall set publicprofile firewallpolicy blockinbound,blockoutbound
```

  
Initial settings:

```bash
echo * disable unused rules...
netsh advfirewall firewall set rule group="Core Networking" new enable=no
netsh advfirewall firewall set rule group="File and Printer Sharing" new enable=no
netsh advfirewall firewall set rule group="Windows Remote Management" new enable=no
netsh advfirewall firewall set rule group="Windows Management Instrumentation (WMI)" new enable=no
netsh advfirewall firewall set rule group="Windows Firewall Remote Management" new enable=no
netsh advfirewall firewall set rule group="SNMP Trap" new enable=no
netsh advfirewall firewall set rule group="Secure Socket Tunneling Protocol" new enable=no
netsh advfirewall firewall set rule group="Windows Security Configuration Wizard" new enable=no
netsh advfirewall firewall set rule group="Routing and Remote Access" new enable=no
netsh advfirewall firewall set rule group="Remote Volume Management" new enable=no
netsh advfirewall firewall set rule group="Remote Service Management" new enable=no
netsh advfirewall firewall set rule group="Remote Scheduled Tasks Management" new enable=no
netsh advfirewall firewall set rule group="Remote Event Log Management" new enable=no
netsh advfirewall firewall set rule group="Remote Administration" new enable=no
netsh advfirewall firewall set rule group="Performance Logs and Alerts" new enable=no
netsh advfirewall firewall set rule group="Network Discovery" new enable=no
netsh advfirewall firewall set rule group="Netlogon Service" new enable=no
netsh advfirewall firewall set rule group="Key Management Service" new enable=no
netsh advfirewall firewall set rule group="iSCSI Service" new enable=no
netsh advfirewall firewall set rule group="Distributed Transaction Coordinator" new enable=no
netsh advfirewall firewall set rule group="DFS Management" new enable=no
netsh advfirewall firewall set rule group="Core Networking" new enable=no
netsh advfirewall firewall set rule group="COM+ Remote Administration" new enable=no
netsh advfirewall firewall set rule group="COM+ Network Access" new enable=no
netsh advfirewall firewall set rule group="BranchCache - Peer Discovery (Uses WSD)" new enable=no
netsh advfirewall firewall set rule group="Secure World Wide Web Services (HTTPS)" new enable=no
netsh advfirewall firewall set rule group="World Wide Web Services (HTTP)" new enable=no
netsh advfirewall firewall set rule group="Remote Desktop" new enable=no
netsh advfirewall firewall set rule group="Remote Desktop - RemoteFX" new enable=no
  
echo * add IP restriction to Remote Desktop
netsh advfirewall firewall add rule name="RDP" dir=in action=allow protocol=TCP localport=19896 remoteip="203.117.172.136,101.127.248.186"
 
netsh advfirewall firewall add rule name="DROP PORTS" dir=in action=block protocol=TCP localport=135-139
netsh advfirewall firewall add rule name="DROP 445" dir=in action=block protocol=TCP localport=445
 
netsh advfirewall set allprofiles state on
 
echo * done initialization
```

### **Salt module for Windows firewall** {#WindowsFirewallCommand-SaltmoduleforWindowsfirewall}

Add/delete rule

```bash
salt 'minion' firewall.add_rule 'rule_name' 'port' 'tcp' 'allow' 'in' 'xx.xx.xx.xx'
salt 'minion' firewall.delete_rule 'rule_name' 'port' 'tcp' 'in' 'xx.xx.xx.xx'
```

### Enable/Disable windows firewall inbound/outbound {#WindowsFirewallCommand-Enable/Disablewindowsfirewallinbound/outbound}

```bash
netsh advfirewall set domainprofile firewallpolicy blockinbound,blockoutbound
netsh advfirewall set privateprofile firewallpolicy blockinbound,blockoutbound
netsh advfirewall set publicprofile firewallpolicy blockinbound,blockoutbound
 
netsh advfirewall set domainprofile firewallpolicy blockinbound,allowoutbound
netsh advfirewall set privateprofile firewallpolicy blockinbound,allowoutbound
netsh advfirewall set publicprofile firewallpolicy blockinbound,allowoutbound
```

