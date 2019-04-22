# tr



```text
# tr [-cdst][--help][--version][First character set][Second character set]  

#Parameter Description:

# -c, --complement: Inverse selection of characters. That is, the part that conforms to SET1 is not processed, and the remaining part that does not match is converted.
# -d, --delete: delete instruction characters
# -s, --squeeze-repeats: Reduces consecutively repeated characters into a specified single character
# -t, --truncate-set1: Cut the specified range of SET1 to be equal to the set length of SET2
# --help: Display program usage information
# --version: display version information of the program itself
# Character Set 1: Specify the original character set to be converted or deleted. When performing a conversion operation, the target character set of the conversion must be specified using the parameter "Character Set 2". However, the parameter "Character Set 2" is not required when performing the delete operation;
# Character Set 2: Specify the target character set to be converted to.

The range of character sets:

\NNN Character of octal value NNN (1 to 3 is an octal value character)
\ Backslash
\a Ctrl-G ringtone
\b Ctrl-H backspace
\f Ctrl-L
\n Ctrl-J new line
\r Ctrl-M Enter
\t Ctrl-I tab
\v Ctrl-X horizontal tab
CHAR1-CHAR2: The range of characters ranges from CHAR1 to CHAR2. The specification of the range is based on the order of the ASCII code. It can only be small to large and cannot be large or small.
[CHAR*] : This is a SET2-specific setting that repeats the specified characters to the same length as SET1.
[CHAR*REPEAT] : This is also a SET2-specific setting. The function is to repeat the specified character to the set number of REPEATs (the REPEAT number is calculated in 8-bit format, starting with 0)
[:alnum:] : all alphabetic characters and numbers
[:alpha:] : all alphabetic characters
[:blank:] : All horizontal spaces
[:cntrl:] : all control characters
[:digit:] : all numbers
[:graph:] : All printable characters (does not contain spaces)
[:lower:] : all lowercase letters
[:print:] : All printable characters (including spaces)
[:punct:] : all punctuation characters
[:space:] : All horizontal and vertical spaces
[:upper:] : all uppercase letters
[:xdigit:] : All 16-digit numbers
[=CHAR=] : All match the specified characters (CHAR in the equal sign, which means you can customize the characters)
```

## Examples

```text
$cat testfile |tr a-z A-Z 
$cat testfile |tr [:lower:] [:upper:] 

$echo "hello 123 world 456" | tr -d '0-9' 
hello world 

$cat text | tr '\t' ' '

$echo aa.,a 1 b#$bb 2 c*/cc 3 ddd 4 | tr -d -c '0-9 \n' 
1  2  3  4

$echo "thissss is a text linnnnnnne." | tr -s ' sn' 
this is a text line.

$echo 1 2 3 4 5 6 7 8 9 | xargs -n1 | echo $[ $(tr '\n' '+') 0 ]

$cat file | tr -s "\r" "\n" > new_file 
#OR
$cat file | tr -d "\r" > new_file
```

