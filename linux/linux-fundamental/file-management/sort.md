# sort

以升序对文件内容排序

```text
$ sort names.txt
```

以降序对文件内容排序

```text
$ sort -r names.txt
```

以第三个字段对/etc/passwd的内容排序

```text
$ sort -t: -k 3n /etc/passwd | more
#-u unique
```

```text
-b Ignores the space character that begins before each line.
-c Checks if the files are sorted in order.
-d When sorting, processing English letters, numbers, and space characters, ignoring other characters.
-f When sorting, treat lowercase letters as uppercase letters.
-i When sorting, except for ASCII characters between 040 and 176, other characters are ignored.
-m Combines several sorted files.
-M Sorts the first 3 letters according to the abbreviation of the month.
-n Sort by size.
-o<output file> Saves the sorted result to the specified file.
-r Sorts in reverse order.
-t<delimiter> Specifies the field separator character used for sorting.
+<Start Field>-<End Field> Sorts by the specified field, from the start field to the previous field of the end field.
--help Displays help.
--version Displays version information.
```

