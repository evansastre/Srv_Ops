# Service backup

```bash
#!/bin/bash
 
echo "Service backup start right now"
 
salt -N 'OS-Windows' cmd.run 'robocopy D:\Service E:\ServiceBack\Service%date:~-4%%date:~-10,-8%%date:~-7,-5% /e /np /nfl /ndl'
```

