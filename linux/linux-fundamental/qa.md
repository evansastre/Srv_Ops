# QA

1.Find provider of a tool

```text
$yum whatprovides netstat
#So we can know it's in "net-tools"
$yum install net-tools
```

2.Change hostname

```
###CentOS6.X
##temp
hostname NewHostName
##perm
vim /etc/sysconfig/network

###CentOS7.X
hostnamectl NewHostName
```

3.How do I back up a user's mission plan?

```text
cp /var/spool/cron/user1 /tmp/bak/cron_bak/
```

4.Close unnecessary service.

```text
yum install ntsysv
#check all services
ntsysv

#close
chkconfig service name off
```

5.After logging in to an account, what log files will the system record in the log file?

A: The user authentication process is recorded in /var/log/secure, and the login success information is recorded in /var/log/wtmp.

6.Use xargs and exec to achieve such a requirement, and change the permissions of all files with the .txt file in the current directory to 777.

```text
（1）find ./ -type f -name "*.txt" |xargs chmod 777
（2）find ./ -type f -name "*.txt" -exec chmod 777 {} \;

```

7. Hard Link and Symbolic Link.

> **Symbolic link** \(Symlinks/Soft links\) are links between files. It is nothing but a shortcut of a file\(in windows terms\).
>
> **Hard link** is the exact replica of the actual file it is pointing to .Both the hard link and the linked file shares the same inode .
>
> Hard links cannot span across filesystem.
>
> Hard links can link only files,not directories.

```text
#To create Symlink 
ln -s <source> <linkname>

#create hard link
ln <source> <linkname>
```

8.Count the number of local user accounts

```text
wc -l /etc/passwd|cut -d" " -f1
```



















