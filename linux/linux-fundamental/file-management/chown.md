# chown

```text
#chown [-cfhRv][--dereference][--help][--version][owner.<owned group>][file or directory..]
#or chown [-chfRv][--dereference][--help][--version][. belongs to group][file or directory... ...]
#or chown [-cfhRv][--dereference][--help][--reference=<reference file or directory>][--version][file or directory...]

# -c or --changes works like the "-v" parameter, but only returns the changed part.
# -f or --quite or --silent does not display an error message.
# -h or --no-dereference modify the symbolic link file without changing any other related files.
# -R or --recursive Recursive processing, processing all files and subdirectories under the specified directory.
# -v or --version Displays the instruction execution process.
# The --dereference effect is the same as the "-h" parameter.
# --help Online help.
# --reference=<reference file or directory> Sets the owner of the specified file or directory to the group to which it belongs and the owner of the reference file or directory is the same as the group to which it belongs.
# --version Displays version information.
```



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

