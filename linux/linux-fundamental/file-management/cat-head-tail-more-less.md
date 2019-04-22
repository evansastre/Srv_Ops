# cat & head/tail & more/less

## Cat

```text
# cat    :   show whole content 
# -n or --number starts with 1 and numbers the number of rows for all outputs
# -b or --number-nonblank is similar to -n except that blank lines are not numbered
# -s or --squeeze-blank When a blank line with more than two consecutive lines is encountered, it is replaced with a blank line of one line.
# -v or --show-nonprinting

#example:
cat -n textfile1 > textfile2 #Add the file content of textfile1 to textfile2 adding the line number.
cat -b textfile1 textfile2 >> textfile3 #Append the contents of textfile1 and textfile2 to the filefile after adding the line number (the blank line is not added)
```

## head/tail

```text
#head/tail  :show head or tail of a file
#tail -f filename  :   Display the data is writing to the file.
```

## more/less

```text
#more/less  : browser  the content, less has more function than more.[Space]down page, [any type]down one line, [Q]quit
```



