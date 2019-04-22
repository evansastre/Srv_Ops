# mount

如果要挂载一个文件系统，需要先创建一个目录，然后将这个文件系统挂载到这个目录上

```text
# mkdir /u01

# mount /dev/sdb1 /u01
```

也可以把它添加到fstab中进行自动挂载，这样任何时候系统重启的时候，文件系统都会被加载

```text
/dev/sdb1 /u01 ext2 defaults 0 2
```

