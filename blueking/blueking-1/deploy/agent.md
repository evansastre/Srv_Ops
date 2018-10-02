# Agent

1. Cert updates to newest. And restart service.
2. Need add "admin" to business-operation member.
3. If no rsync on proxy, install rsync, and reinstall rsync 
4. 5. All P-agents's hostname-IP required in proxy's /etc/hosts 
6. Test remote execute on proxy:

```text
cd /opt/py27/bin
./wmiexec.py -debug Administrator:password@P-Agent-Hostname 'dir C:\'
```



