# Agent

1. Cert updates to newest on blueking server. And restart service.
2. Need add account "admin" to business-operation membership.
3. Inbound , set both on PA and windows firewall
4. ```text
   proxy to agent: port TCP:60020-60030 UDP：60020-60030 
   proxy to agent windows: port TCP:22,139,445,49154(wmiexec)
   ```
5. How to open 139,445 on windows

   ```bash
   #open TCP/IP Netbios and its service
   wmic nicconfig where TcpipNetbiosOptions=0 call SetTcpipNetbios 1
   wmic nicconfig where TcpipNetbiosOptions=2 call SetTcpipNetbios 1
   sc stop lmhosts
   sc start lmhosts
   #check: 
   netstat -ano | findstr "139" 
   netstat -ano | findstr "445"   
   ```

6. admin$ need on P-Agent, set below and reboot to take effect.

   ```bash
   REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters /v AutoShareWks /t REG_DWORD /d 1 /f
   REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters /v AutoShareServer /t REG_DWORD /d 1 /f
   #after reboot, check show admin$
   net share
   ```

7. All P-agents's hostname-IP required in proxy's /etc/hosts 
8. Test remote execute on proxy:

   ```text
   cd /opt/py27/bin
   ./wmiexec.py -debug Administrator:password@P-Agent-Hostname 'dir C:\'
   ```

