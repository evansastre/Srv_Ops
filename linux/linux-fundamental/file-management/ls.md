# ls

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

