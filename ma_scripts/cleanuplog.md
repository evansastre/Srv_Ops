# CleanupLog

```bash
#set crontab
00  6 * * * root bash /srv/salt/LIVE_Scripts/CleanupLog.sh
```

{% code-tabs %}
{% code-tabs-item title="/srv/salt/LIVE\_Scripts/CleanupLog.sh" %}
```bash
# Do not use [*] replace [*.*], [*] include folder, that logic will make error.
  
salt -N 'World' cmd.run 'forfiles -p "E:\log" -s -m *.* -d -30 -c "cmd /c del /s /q @file"'
salt -N 'Cache' cmd.run 'forfiles -p "E:\log" -s -m *.* -d -30 -c "cmd /c del /s /q @file"'
salt -N 'Log' cmd.run 'forfiles -p "E:\log" -s -m *.* -d -30 -c "cmd /c del /s /q @file"'
salt -N 'Chat' cmd.run 'forfiles -p "E:\log" -s -m *.* -d -30 -c "cmd /c del /s /q @file"'
salt -N 'Func' cmd.run 'forfiles -p "E:\log" -s -m *.* -d -60 -c "cmd /c del /s /q @file"'
salt 'Dungeon01' cmd.run 'forfiles -p "E:\log" -s -m *.* -d -15 -c "cmd /c del /s /q @file"'
salt -N 'Log' cmd.run 'forfiles -p "D:\Service\LogServer\log" -s -m *.* -d -30 -c "cmd /c del /s /q @file"'
salt -N 'LogAgent' cmd.run 'forfiles -p "D:\Service\LogAgent\log" -s -m *.* -d -30 -c "cmd /c del /s /q @file"'
salt -N 'Management' cmd.run 'forfiles -p "D:\Service\ManagementAgent\log" -s -m *.* -d -30 -c "cmd /c del /s /q @file"'
```
{% endcode-tabs-item %}
{% endcode-tabs %}

