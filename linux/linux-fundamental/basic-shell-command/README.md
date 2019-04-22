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

## 

## free

这个命令用于显示系统当前内存的使用情况，包括已用内存、可用内存和交换内存的情况

默认情况下free会以字节为单位输出内存的使用量

```text
$ free
             total       used       free     shared    buffers     cached
Mem:       3566408    1580220    1986188          0     203988     902960
-/+ buffers/cache:     473272    3093136
Swap:      4000176          0    4000176
```

如果你想以其他单位输出内存的使用量，需要加一个选项，-g为GB，-m为MB，-k为KB，-b为字节

```text
$ free -g
             total       used       free     shared    buffers     cached
Mem:             3          1          1          0          0          0
-/+ buffers/cache:          0          2
Swap:            3          0          3
```

如果你想查看所有内存的汇总，请使用-t选项，使用这个选项会在输出中加一个汇总行

```text
ramesh@ramesh-laptop:~$ free -t
             total       used       free     shared    buffers     cached
Mem:       3566408    1592148    1974260          0     204260     912556
-/+ buffers/cache:     475332    3091076
Swap:      4000176          0    4000176
Total:     7566584    1592148    5974436
```



## 

## kill

kill用于终止一个进程。一般我们会先用`ps -ef`查找某个进程得到它的进程号，然后再使用`kill -9 进程号`终止该进程。你还可以使用killall、pkill、xkill来终止进程

```text
$ ps -ef | grep vim
ramesh    7243  7222  9 22:43 pts/2    00:00:00 vim

$ kill -9 7243
```

更多示例：[4 Ways to Kill a Process – kill, killall, pkill, xkill](http://www.thegeekstuff.com/2009/12/4-ways-to-kill-a-process-kill-killall-pkill-xkill/)

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



## mount

如果要挂载一个文件系统，需要先创建一个目录，然后将这个文件系统挂载到这个目录上

```text
# mkdir /u01

# mount /dev/sdb1 /u01
```

也可以把它添加到fstab中进行自动挂载，这样任何时候系统重启的时候，文件系统都会被加载

```text
/dev/sdb1 /u01 ext2 defaults 0 2
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

## ifconfig

ifconfig用于查看和配置Linux系统的网络接口

查看所有网络接口及其状态

```text
$ ifconfig -a
```

使用up和down命令启动或停止某个接口

```text
$ ifconfig eth0 up

$ ifconfig eth0 down
```

更多示例：[Ifconfig: 7 Examples To Configure Network Interface](http://www.thegeekstuff.com/2009/03/ifconfig-7-examples-to-configure-network-interface/)

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



## ping

ping一个远程主机，只发5个数据包

```text
$ ping -c 5 gmail.com
```

更多示例：[Ping Tutorial: 15 Effective Ping Command Examples](http://www.thegeekstuff.com/2009/11/ping-tutorial-13-effective-ping-command-examples/)

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

## wget

使用wget从网上下载软件、音乐、视频

```text
$ wget http://prdownloads.sourceforge.net/sourceforge/nagios/nagios-3.2.1.tar.gz
```

下载文件并以指定的文件名保存文件

```text
$ wget -O taglist.zip http://www.vim.org/scripts/download_script.php?src_id=7701
```

更多示例：[The Ultimate Wget Download Guide With 15 Awesome Examples](http://www.thegeekstuff.com/2009/09/the-ultimate-wget-download-guide-with-15-awesome-examples/)

