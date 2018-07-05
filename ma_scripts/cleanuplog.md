# CleanupLog

```bash
#set crontab
00  6 * * * root bash /srv/salt/LIVE_Scripts/CleanupLog.sh
```

{% code-tabs %}
{% code-tabs-item title="/srv/salt/LIVE\_Scripts/CleanupLog.sh" %}
```bash
salt -N 'World' cmd.run 'forfiles -p "E:\log" -s -m * -d -30 -c "cmd /c del /s /q @path"'
salt -N 'Cache' cmd.run 'forfiles -p "E:\log" -s -m * -d -30 -c "cmd /c del /s /q @path"'
salt -N 'Log' cmd.run 'forfiles -p "E:\log" -s -m * -d -30 -c "cmd /c del /s /q @path"'
salt -N 'Chat' cmd.run 'forfiles -p "E:\log" -s -m * -d -30 -c "cmd /c del /s /q @path"'
salt -N 'Func' cmd.run 'forfiles -p "E:\log" -s -m * -d -60 -c "cmd /c del /s /q @path"'
salt -N 'Log' cmd.run 'forfiles -p "D:\Service\LogServer\log" -s -m * -d -30 -c "cmd /c del /s /q @path"'
salt -N 'LogAgent' cmd.run 'forfiles -p "D:\Service\LogAgent\log" -s -m * -d -30 -c "cmd /c del /s /q @path"'
salt -N 'Management' cmd.run 'forfiles -p "D:\Service\ManagementAgent\log" -s -m * -d -30 -c "cmd /c del /s /q @path"'
```
{% endcode-tabs-item %}
{% endcode-tabs %}

