# cp & mv

## cp

拷贝文件1到文件2，并保持文件的权限、属主和时间戳

```text
$ cp -p file1 file2
```

拷贝file1到file2，如果file2存在会提示是否覆盖

```text
$ cp -i file1 file2
```

```text
#copy file1 file2 to dir1
cp file1 file2 dir1
#copy dir1 dir2 to dir3
cp -r dir1 dir2 dir3
```

## mv

将文件名file1重命名为file2，如果file2存在则提示是否覆盖

```text
$ mv -i file1 file2
```

注意如果使用-f选项则不会进行提示

-v会输出重命名的过程，当文件名中包含通配符时，这个选项会非常方便

```text
$ mv -v file1 file2
```

