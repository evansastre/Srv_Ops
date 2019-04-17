# File management



## ls

```bash
# ~
#reverse cat
tac

#show command which document include "calendar" 
man -k calendar

#cd previous path
cd -             

#show previous path  
echo $OLDPWD       

#show types of files
ls -F
# / Directory
# @ Link
# * Executable

#list files by time 
ls -t 
#Reverse order
ls -r
#long listing including all files reverse sorted by time
ls -latr

#list files recursively
ls -R
#list directories only
tree -d 
#colorize output
tree -C

#list directory 
ls -d [dirname]

#show as human can ready
$ ls -lh
-rw-r----- 1 ramesh team-dev 8.9M Jun 12 15:27 arch-linux.txt.gz
```

more examples：[Unix LS Command: 15 Practical Examples](http://www.thegeekstuff.com/2009/07/linux-ls-command-examples/)

## file

```text
#Display the file type
```

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

## cat head/tail more/less

```text
#cat    :   show whole content
#head/tail  :   show head or tail of a file
#more/less  : browser  the content, less has more function than more.[Space]down page, [any type]down one line, [Q]quit

#tail -f filename  :   Display the data is writing to the file.
```

## vim

```text
####vim
##movement
#k j :  up or down one line,   <5>+<k> move 5line 
#h l :  left or right one charactor
#w b :  right or left one word
#^   :  go to beginning of one line
#$   :  go to end of one line
#gg Go to the first line
#G Go to the last line

#i I : insert current position or begining of line
#80i<Text><Esc>= Insert<Text>80times
#80_<Esc>=Insert"_"80times
#a A : add after current position or ending of line
#o Open a new line below the current line
#O Open a new line above the current line

# :wq or :x   :   save and quit
# :n   :  go to number n line
# :$   :  go to last line

# :set nu    :set nonu    : show line number or not 

#x :  delete a charactor
#dw:  delete one word
#dd:  delete one line
#D:   delete from current position

#r :  replace current charactor
#cw:  change current word
#cc:  change current line
#c$:  change from current position
#C :  same as c$

#~ :  Reverse case of a Charactor, like a->A, A-a

#yy : copy current line
#y3w: copy 3 words
#y$:  copy rest of current line
#p  : paste copied or deleted content 

#u :undo
#Ctrl-R : Redo

#/   : start a forward search
#?   : srart a reverse search
#n   : next 
#N   : previous

##Find and Replace
#:s/{old}/{new}/{options} Substitute {new} for {old} on the current line
#:%s/{old}/{new}/{options} Substitute {new} for {old} in the entire document
#The g option substitutes all occurrences on a line, otherwise just the first occurrence is changed per line.
#example    :$s/i/I/g   change all i to I
```





