# find & locate

## find 

```text
#Find the file with the specified file name (not case sensitive)
find -iname "MyProgram.c" 

#Execute a command on the found file
find -iname "MyProgram.c" -exec md5sum {} \; 

#Find all empty files in the home directory
find ~ -empty

#-mtime days   #Finds files that are days old
find . -mtime +10 -mtime -13

#-size num  .    
find .   -size +1M

#-type d    |  -type f
#-newer
find . -type d  -newer file.txt
```

```text
-amin<minutes> Finds files or directories that have been accessed at a specified time, in minutes.
-anewer<reference file or directory> Finds files or directories whose access time is closer to the current file than the specified file or directory.
-atime<24 hours> Finds files or directories that have been accessed at a specified time. The unit is calculated in 24 hours.
-cmin<minutes> Finds files or directories that were changed at the specified time.
-cnewer<reference file or directory> Finds a file or directory whose change time is closer to the current file than the specified file or directory.
-ctime<24 hours> Finds the file or directory that was changed at the specified time, in 24 hours.
-daystart Calculates the time from today.
-depth Looks up from the deepest subdirectory in the specified directory.
-expty Look for a file with a file size of 0 Byte, or an empty directory with no subdirectories or files under the directory.
-exec<execute instruction> Assuming that the return value of the find instruction is True, the instruction is executed.
-false Sets the return value of the find command to False.
-fls<list file> The effect of this parameter is similar to specifying the "-ls" parameter, but will save the result as the specified list file.
-follow Excludes symbolic links.
-fprint<list file> The effect of this parameter is similar to specifying the "-print" parameter, but will save the result to the specified list file.
-fprint0<list file> The effect of this parameter is similar to specifying the "-print0" parameter, but will save the result to the specified list file.
-fprintf<list file><output format> The effect of this parameter is similar to specifying the "-printf" parameter, but will save the result to the specified list file.
-fstype<filesystem type> Find only files or directories under this filesystem type.
-gid<group ID> Finds a file or directory that matches the specified group ID.
-group<group name> Finds a file or directory that matches the specified group name.
-help or --help online help.
-ilname<template style> The effect of this parameter is similar to specifying the "-lname" parameter, but ignoring the difference in character case.
-iname<template style> The effect of this parameter is similar to specifying the "-name" parameter, but ignoring the difference in character case.
-inum<inode number> Finds a file or directory that matches the specified inode number.
-ipath<template style> The effect of this parameter is similar to specifying the "-ipath" parameter, but ignoring the difference in character case.
-iregex<template style> The effect of this parameter is similar to specifying the "-regexe" parameter, but ignoring the difference in character case.
-links<number of connections> Finds files or directories that match the specified number of hard links.
-iname<template style> Specifies a string as a template style for finding symbolic links.
-ls Assuming the return value of the find command is True, the file or directory name is listed to standard output.
-maxdepth<directory level> Sets the maximum directory level.
-mindepth<directory level> Sets the minimum directory level.
-mmin<minutes> Finds files or directories that have been changed at a given time, in minutes.
-mount This parameter has the same effect as specifying "-xdev".
-mtime<24 hours> Finds files or directories that have been changed at the specified time, in 24 hours.
-name<template style> Specify a string as a template style for finding files or directories.
-newer<reference file or directory> Finds a file or directory whose change time is closer to the current file than the specified file or directory.
-nogroup Finds files or directories that do not belong to the local host group ID.
-noleaf Do not consider the directory to have at least two hard links.
-nouser Finds files or directories that are not part of the local host user ID.
-ok<execute command> The effect of this parameter is similar to specifying the "-exec" parameter, but the user will be asked before executing the command. If "y" or "Y" is answered, the execution instruction will be discarded.
-path<template style> Specifies the string as the template style for finding the directory.
-perm<permission value> Finds a file or directory that matches the specified permission value.
-print Assuming the return value of the find command is True, the file or directory name is listed to standard output. The format is a name for each column, and each name has a "./" string before it.
-print0 Assuming the return value of the find command is True, the file or directory name is listed to standard output. The format is all on the same line.
-printf<output format> Assuming the return value of the find command is True, the file or directory name is listed to standard output. The format can be specified by itself.
-prune does not look for strings as a template style for finding files or directories.
-regex<template style> Specify a string as a template style for finding files or directories.
-size<file size> Finds files that match the specified file size.
-true Sets the return value of the find command to True.
-typ<file type> Finds only files that match the specified file type.
-uid<user ID> Finds a file or directory that matches the specified user ID.
-used <number of days> Finds the file or directory that was accessed at a specified time after the file or directory was changed. The unit is calculated in days.
-user<owner name> Finds a file or directory that matches the specified owner name.
-version or --version displays version information.
-xdev limits the scope to the preemptive file system.
-xtype<file type> The effect of this parameter is similar to specifying the "-type" parameter, except that it checks for symbolic links.
```

## locate

* Lists files that match pattern. 
* Faster than the find command. 
* Queries an index. 
* Results are not in real time. 
* May not be enabled on all systems.

locate命名可以显示某个指定文件（或一组文件）的路径，它会使用由updatedb创建的数据库

下面的命令会显示系统中所有包含crontab字符串的文件

```text
$ locate crontab
/etc/anacrontab
/etc/crontab
/usr/bin/crontab
/usr/share/doc/cron/examples/crontab2english.pl.gz
/usr/share/man/man1/crontab.1.gz
/usr/share/man/man5/anacrontab.5.gz
/usr/share/man/man5/crontab.5.gz
/usr/share/vim/vim72/syntax/crontab.vim
```

