# ftp

## ftp

ftp命令和sftp命令的用法基本相似连接ftp服务器并下载多个文件

```text
$ ftp IP/hostname
ftp> mget *.html
```

显示远程主机上文件列表

```text
ftp> mls *.html -
/ftptest/features.html
/ftptest/index.html
/ftptest/othertools.html
/ftptest/samplereport.html
/ftptest/usage.html
```

更多示例：[FTP and SFTP Beginners Guide with 10 Examples](http://www.thegeekstuff.com/2010/06/ftp-sftp-tutorial/)

