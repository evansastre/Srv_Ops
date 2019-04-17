# wildcards

```text
* - matches zero or more characters
a*.txt
? - matches exactly one character
?.txt
a?
a?.txt

[] - a character class
ca[nt]*
- can
- cat
- candy
- catch

[!] - not include 
ca[t]*
- can
- candy

[a-g]*
matches all files that start with a,b,c,d,e,f,g
[3-6]*
matches all files that start with 3,4,5,6

predefined named character classes
[[:alpha:]]
[[:alnum:]]
[[:digit:]]
[[:lower:]]
[[:space:]]
[[:upper:]]

\ - escape character
*\?
  - done?
  
  
```

```text
* 
```

