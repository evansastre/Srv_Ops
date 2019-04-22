# Basic Shell Command

## Resource 

[https://www.linuxtrainingacademy.com/](https://www.linuxtrainingacademy.com/)

## ssh

登录到远程主机

```text
$ ssh -l jsmith remotehost.example.com
```

调试ssh客户端

```text
$ ssh -v -l jsmith remotehost.example.com
```

显示ssh客户端版本

```text
$ ssh -V
```

更多示例：[Basic Linux SSH Client Commands](http://www.thegeekstuff.com/2008/05/5-basic-linux-ssh-client-commands/)

##  pwd

输出当前工作目录

## cd

`cd -`可以在最近工作的两个目录间切换

使用`shopt -s cdspell`可以设置自动对cd命令进行拼写检查

更多示例：[6 Awesome Linux cd command Hacks](http://www.thegeekstuff.com/2008/10/6-awesome-linux-cd-command-hacks-productivity-tip3-for-geeks/)

## shutdown

关闭系统并立即关机

```text
$ shutdown -h now
```

10分钟后关机

```text
$ shutdown -h +10
```

重启

```text
$ shutdown -r now
```

重启期间强制进行系统检查

```text
$ shutdown -Fr now
```

##  rm

删除文件前先确认

```text
$ rm -i filename.txt
```

在文件名中使用shell的元字符会非常有用。删除文件前先打印文件名并进行确认

```text
$ rm -i file*
```

递归删除文件夹下所有文件，并删除该文件夹

```text
$ rm -r example
```

## passwd

passwd用于在命令行修改密码，使用这个命令会要求你先输入旧密码，然后输入新密码

```text
$ passwd
```

超级用户可以用这个命令修改其他用户的密码，这个时候不需要输入用户的密码

```text
# passwd USERNAME
```

passwd还可以删除某个用户的密码，这个命令只有root用户才能操作，删除密码后，这个用户不需要输入密码就可以登录到系统

```text
# passwd -d USERNAME
```

## mkdir

在home目录下创建一个名为temp的目录

```text
$ mkdir ~/temp
```

使用-p选项可以创建一个路径上所有不存在的目录

```text
$ mkdir -p dir1/dir2/dir3/dir4/
```



## uname

uname可以显示一些重要的系统信息，例如内核名称、主机名、内核版本号、处理器类型之类的信息

```text
$ uname -a
Linux john-laptop 2.6.32-24-generic #41-Ubuntu SMP Thu Aug 19 01:12:52 UTC 2010 i686 GNU/Linux
```

## whereis

当你不知道某个命令的位置时可以使用whereis命令，下面使用whereis查找ls的位置

```text
$ whereis ls
ls: /bin/ls /usr/share/man/man1/ls.1.gz /usr/share/man/man1p/ls.1p.gz
```

当你想查找某个可执行程序的位置，但这个程序又不在whereis的默认目录下，你可以使用-B选项，并指定目录作为这个选项的参数。下面的命令在/tmp目录下查找lsmk命令

```text
$ whereis -u -B /tmp -f lsmk
lsmk: /tmp/lsmk
```

## whatis

wathis显示某个命令的描述信息

```text
$ whatis ls
ls		(1)  - list directory contents

$ whatis ifconfig
ifconfig (8)         - configure a network interface
```

## man

显示某个命令的man页面

```text
$ man crontab
```

有些命令可能会有多个man页面，每个man页面对应一种命令类型

```text
$ man SECTION-NUMBER commandname
```

man页面一般可以分为8种命令类型

1. 用户命令
2. 系统调用
3. c库函数
4. 设备与网络接口
5. 文件格式
6. 游戏与屏保
7. 环境、表、宏
8. 系统管理员命令和后台运行命令

例如，我们执行`whatis crontab`，你可以看到crontab有两个命令类型1和5，所以我们可以通过下面的命令查看命令类型5的man页面

```text
$ whatis crontab
crontab (1)          - maintain crontab files for individual users (V3)
crontab (5)          - tables for driving cron

$ man 5 crontab
```

## mysql

mysql可能是Linux上使用最广泛的数据库，即使你没有在你的服务器上安装mysql，你也可以使用mysql客户端连接到远程的mysql服务器

连接一个远程数据库，需要输入密码

```text
$ mysql -u root -p -h 192.168.1.2
```

连接本地数据库

```text
$ mysql -u root -p
```

你也可以在命令行中输入数据库密码，只需要在-p后面加上密码作为参数，可以直接写在p后面而不用加空格

## date

设置系统日期

```text
# date -s "01/31/2010 23:59:53"
```

当你修改了系统时间，你需要同步硬件时间和系统时间

```text
# hwclock –systohc

# hwclock --systohc –utc
```

## 

