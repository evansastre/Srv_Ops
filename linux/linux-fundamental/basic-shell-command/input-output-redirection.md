# Input, Output, Redirection

| I/O Name | Abbreviation | File Descriptor  |
| :--- | :--- | :--- |
| Standard Input | stdin  | 0 |
| Standard Output | stdout | 1 |
| Standard Error | stderr | 2 |

```text
> Redirects standard output to a file.
Overwrites (truncating) existing contents.
>> Redirects standard output to a file.
Appends to any existing contents.
< Redirects input from a file to a command. 

& Used with redirection to signal that a
file descriptor is being used.
2>&1 Combine stderr and standard output.
2>file Redirect standard error to a file.

>/dev/null Redirect output to nowhere.
$ ls here not-here 2> /dev/null
here
$ ls here not-here > /dev/null 2>&1

$ ls files.txt not-here 1>out 2>out.err

```

>

