# Basic Shell Command

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


```

## tar

```text
#create
tar cvf archive_name.tar dirname/
#estimates the tar file size ( in KB ) before you create the tar file.
$ tar -cf - /directory/to/archive/ | wc -c
20480

#extract
tar xvf archive_name.tar  [destPath1] [destPath2]
#extract archives using regular expression
tar xvf archive_file.tar --wildcards '*.pl'
#Adding a file or directory to an existing archive, 
#Note: You cannot add file or directory to a compressed archive, for instance '.tgz'
tar rvf archive_name.tar newfileOrnewdir

#show
tar tvf archive_name.tar 
less archive_name.tar 



#c – create a new archive
#v – verbosely list files which are processed.
#f – following is the archive file name
#z – filter the archive through gzip
#j – filter the archive through bzip2
#–wildcards *.pl – files with pl extension
#r - Adding a file or directory to an existing archive 
-W Verify files available in tar 
```

## grep

```text
$ grep -i "the" demo_file
$ grep -A 3 -i "example" demo_text
$ grep -r "ramesh" *

```































