# ps

```text
-e    #everything, all process
-f    #full format listing
-u username   #display username's processes
-p pid  #display information for PID

```

```text
pstree #Display processes in a tree format.
top #Interactive process viewer.
htop #Interactive process viewer. 
```

ps命令用于显示正在运行中的进程的信息，ps命令有很多选项，这里只列出了几个

查看当前正在运行的所有进程

```text
$ ps -ef | more
```

以树状结构显示当前正在运行的进程，H选项表示显示进程的层次结构

```text
$ ps -efH | more
```



