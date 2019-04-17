# sed

## sed

当你将Dos系统中的文件复制到Unix/Linux后，这个文件每行都会以\r\n结尾，sed可以轻易将其转换为Unix格式的文件，使用\n结尾的文件

```text
$ sed 's/.$//' filename
```

反转文件内容并输出

```text
$ sed -n '1!G; h; p' filename
```

为非空行添加行号

```text
$ sed '/./=' thegeekstuff.txt | sed 'N; s/\n/ /'
```

s

```text
sed -r 's/(^[^#])/#&/' /path/to
```

更多示例：[Advanced Sed Substitution Examples](http://www.thegeekstuff.com/2009/10/unix-sed-tutorial-advanced-sed-substitution-examples/)

