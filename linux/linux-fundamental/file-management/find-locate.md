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

