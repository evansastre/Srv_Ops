# tar & gzip

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



## gzip

```text
# creat *.gz compressed file
$ gzip test.txt
#extra *.gz file
$ gzip -d test.txt.gz
#show compressed ratio
$ gzip -l *.gz
     compressed        uncompressed  ratio uncompressed_name
          23709               97975  75.8% asp-patch-rpms.txt
```

## gunzip

```text
gunzip file.gz
```

## bzip2

创建\*.bz2压缩文件

```text
$ bzip2 test.txt
```

解压\*.bz2文件

```text
bzip2 -d test.txt.bz2
```

更多示例：[BZ is Eazy! bzip2, bzgrep, bzcmp, bzdiff, bzcat, bzless, bzmore examples](http://www.thegeekstuff.com/2010/10/bzcommand-examples/)

## uzip

解压\*.zip文件

```text
$ unzip test.zip
```

查看\*.zip文件的内容

```text
$ unzip -l jasper.zip
Archive:  jasper.zip
Length     Date   Time    Name
--------    ----   ----    ----
40995  11-30-98 23:50   META-INF/MANIFEST.MF
32169  08-25-98 21:07   classes_
15964  08-25-98 21:07   classes_names
10542  08-25-98 21:07   classes_ncomp
```

