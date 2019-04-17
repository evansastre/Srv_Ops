# xargs

## xargs

将所有图片文件拷贝到外部驱动器

```text
$ ls *.jpg | xargs -n1 -i cp {} /external-hard-drive/directory
```

将系统中所有jpd文件压缩打包

```text
$ find / -name *.jpg -type f -print | xargs tar -cvzf images.tar.gz
```

下载文件中列出的所有url对应的页面

```text
$ cat url-list.txt | xargs wget –c
```

