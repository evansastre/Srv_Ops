# grep & egrep % fgrep

## grep

```text
$ grep -i "the" demo_file   
$ grep -A 3 -i "example" demo_text
$ grep -r "ramesh" *

#-i ignore case
#-c  count
#-n   precede output with line numbers
#-v   invert match. Print lines that don't match.
#-A [n]  after n lines 
#-B [n]  before nlines

```

```text
-a or --text Do not ignore binary data.
-A<display column number> or --after-context=<display column number> In addition to displaying the column that matches the template style, the content after the column is displayed.
-b or --byte-offset Indicates the bit number of the first character of the column before displaying the column that matches the template style.
-B<display column number> or --before-context=<display column number> In addition to displaying the column that matches the template style, the content before the column is displayed.
-c or --count Counts the number of columns that match the template style.
-C<display column number> or --context=<display column number> or -<display column number> In addition to displaying the column that matches the template style, the content before and after the column is displayed.
-d<make action> or --directories=<perform action> This parameter must be used when specifying that the directory is to be searched instead of a file, otherwise the grep command will report the information and stop the action.
-e<template style> or --regexp=<template style> Specify a string as a template style for finding the contents of a file.
-E or --extended-regexp Use the template style as an extended normal representation.
-f<template file> or --file=<template file> Specifies the template file whose content contains one or more template styles, allowing grep to find the contents of the file that conform to the template condition, in the format of a template style for each column.
-F or --fixed-regexp treats a template style as a list of fixed strings.
-G or --basic-regexp treats the template style as a normal representation.
-h or --no-filename Does not indicate the name of the file to which the column belongs before displaying the column that matches the template style.
-H or --with-filename Indicates the name of the file to which the column belongs before displaying the column that matches the template style.
-i or --ignore-case ignores the difference in character case.
-l or --file-with-matches Lists the file names whose file contents conform to the specified template style.
-L or --files-without-match Lists file names whose file contents do not match the specified template style.
-n or --line-number Marks the column number of the column before displaying the column that matches the template style.
-q or --quiet or --silent does not display any information.
-r or --recursive This parameter has the same effect as specifying the "-d recurse" parameter.
-s or --no-messages does not display an error message.
-v or --revert-match Reverse lookup.
-V or --version displays version information.
-w or --word-regexp displays only full-character columns.
-x or --line-regexp displays only the columns that match the entire column.
-y This parameter has the same effect as specifying the "-i" parameter.
--help Online help
```

## egrep

```text
egrep =  grep -E
```



## fgrep

```text
egrep =  grep -F
```

