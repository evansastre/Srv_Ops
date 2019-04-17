# Basic Shell Command

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

## sort

以升序对文件内容排序

```text
$ sort names.txt
```

以降序对文件内容排序

```text
$ sort -r names.txt
```

以第三个字段对/etc/passwd的内容排序

```text
$ sort -t: -k 3n /etc/passwd | more
#-u unique
```

## export

输出跟字符串oracle匹配的环境变量

```text
$ export | grep ORCALE
declare -x ORACLE_BASE="/u01/app/oracle"
declare -x ORACLE_HOME="/u01/app/oracle/product/10.2.0"
declare -x ORACLE_SID="med"
declare -x ORACLE_TERM="xterm"
```

设置全局环境变量

```text
$ export ORACLE_HOME=/u01/app/oracle/product/10.2.0
```

## du 

```text
du [-b|-k|-m] #show size in b k m 
du -h -a #show all& human can read
```



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

## crontab

查看某个用户的crontab入口

```text
$ crontab -u john -l
```

设置一个每十分钟执行一次的计划任务

```text
*/10 * * * * /home/ramesh/check-disk-space
```

更多示例：[Linux Crontab: 15 Awesome Cron Job Examples](http://www.thegeekstuff.com/2009/06/15-practical-crontab-examples/)

## ps

ps命令用于显示正在运行中的进程的信息，ps命令有很多选项，这里只列出了几个

查看当前正在运行的所有进程

```text
$ ps -ef | more
```

以树状结构显示当前正在运行的进程，H选项表示显示进程的层次结构

```text
$ ps -efH | more
```

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

## top

top命令会显示当前系统中占用资源最多的一些进程（默认以CPU占用率排序）如果你想改变排序方式，可以在结果列表中点击O（大写字母O）会显示所有可用于排序的列，这个时候你就可以选择你想排序的列

```text
Current Sort Field:  P  for window 1:Def
Select sort field via field letter, type any other key to return

  a: PID        = Process Id              v: nDRT       = Dirty Pages count
  d: UID        = User Id                 y: WCHAN      = Sleeping in Function
  e: USER       = User Name               z: Flags      = Task Flags
  ........
```

如果只想显示某个特定用户的进程，可以使用-u选项

```text
$ top -u oracle
```

更多示例：[Can You Top This? 15 Practical Linux Top Command Examples](http://www.thegeekstuff.com/2010/01/15-practical-unix-linux-top-command-examples/)

## df

显示文件系统的磁盘使用情况，默认情况下`df -k` 将以字节为单位输出磁盘的使用量

```text
$ df -k
Filesystem           1K-blocks      Used Available Use% Mounted on
/dev/sda1             29530400   3233104  24797232  12% /
/dev/sda2            120367992  50171596  64082060  44% /home
```

使用-h选项可以以更符合阅读习惯的方式显示磁盘使用量

```text
$ df -h
Filesystem                  Size   Used  Avail Capacity  iused      ifree %iused  Mounted on
/dev/disk0s2               232Gi   84Gi  148Gi    37% 21998562   38864868   36%   /
devfs                      187Ki  187Ki    0Bi   100%      648          0  100%   /dev
map -hosts                   0Bi    0Bi    0Bi   100%        0          0  100%   /net
map auto_home                0Bi    0Bi    0Bi   100%        0          0  100%   /home
/dev/disk0s4               466Gi   45Gi  421Gi    10%   112774  440997174    0%   /Volumes/BOOTCAMP
//app@izenesoft.cn/public  2.7Ti  1.3Ti  1.4Ti    48%        0 18446744073709551615    0%   /Volumes/public
```

使用-T选项显示文件系统类型

```text
$ df -T
Filesystem    Type   1K-blocks      Used Available Use% Mounted on
/dev/sda1     ext4    29530400   3233120  24797216  12% /
/dev/sda2     ext4   120367992  50171596  64082060  44% /home
```

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



## cat

你可以一次查看多个文件的内容，下面的命令会先打印file1的内容，然后打印file2的内容

```text
$ cat file1 file2
```

-n命令可以在每行的前面加上行号

```text
$ cat -n /etc/logrotate.conf
    1	/var/log/btmp {
    2	    missingok
    3	    monthly
    4	    create 0660 root utmp
    5	    rotate 1
    6	}
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

## chmod

chmod用于改变文件和目录的权限

给指定文件的属主和属组所有权限\(包括读、写、执行\)

```text
$ chmod ug+rwx file.txt
```

删除指定文件的属组的所有权限

```text
$ chmod g-rwx file.txt
```

修改目录的权限，以及递归修改目录下面所有文件和子目录的权限

```text
$ chmod -R ug+rwx file.txt
```

更多示例：[7 Chmod Command Examples for Beginners](http://www.thegeekstuff.com/2010/06/chmod-command-examples/)

## chown

chown用于改变文件属主和属组

同时将某个文件的属主改为oracle，属组改为db

```text
$ chown oracle:dba dbora.sh
```

使用-R选项对目录和目录下的文件进行递归修改

```text
$ chown -R oracle:dba /home/oracle
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

## tail

tail命令默认显示文件最后的10行文本

```text
$ tail filename.txt
```

你可以使用-n选项指定要显示的行数

```text
$ tail -n N filename.txt
```

你也可以使用-f选项进行实时查看，这个命令执行后会等待，如果有新行添加到文件尾部，它会继续输出新的行，在查看日志时这个选项会非常有用。你可以通过CTRL-C终止命令的执行

```text
$ tail -f log-file
```

更多示例：[3 Methods To View tail -f output of Multiple Log Files in One Terminal](http://www.thegeekstuff.com/2009/09/multitail-to-view-tail-f-output-of-multiple-log-files-in-one-terminal/)

## less

这个命名可以在不加载整个文件的前提下显示文件内容，在查看大型日志文件的时候这个命令会非常有用

```text
$ less huge-log-file.log
```

当你用less命令打开某个文件时，下面两个按键会给你带来很多帮助，他们用于向前和向后滚屏

```text
CTRL+F – forward one window
CTRL+B – backward one window
```

更多示例：[Unix Less Command: 10 Tips for Effective Navigation](http://www.thegeekstuff.com/2010/02/unix-less-command-10-tips-for-effective-navigation/)

## su

su命令用于切换用户账号，超级用户使用这个命令可以切换到任何其他用户而不用输入密码

```text
$ su - USERNAME
```

用另外一个用户名执行一个命令下面的示例中用户john使用raj用户名执行ls命令，执行完后返回john的账号

```text
[john@dev-server]$ su - raj -c 'ls'

[john@dev-server]$
```

用指定用户登录，并且使用指定的shell程序，而不用默认的

```text
$ su -s 'SHELLNAME' USERNAME
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

##  yum

使用yum安装apache

```text
$ yum install httpd
```

更新apache

```text
$ yum update httpd
```

卸载/删除apache

```text
$ yum remove httpd
```

## rpm

使用rpm安装apache

```text
# rpm -ivh httpd-2.2.3-22.0.1.el5.i386.rpm
```

更新apache

```text
# rpm -uvh httpd-2.2.3-22.0.1.el5.i386.rpm
```

卸载/删除apache

```text
# rpm -ev httpd
```

更多示例：[RPM Command: 15 Examples to Install, Uninstall, Upgrade, Query RPM Packages](http://www.thegeekstuff.com/2010/07/rpm-command-examples/)

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





























