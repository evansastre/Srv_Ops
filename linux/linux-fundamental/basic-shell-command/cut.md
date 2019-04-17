# cut

```text
-d delimiter   #use delimiter as the filed separatoe
-f N        #Fisplay the Nth field

cat /etc/passwd | cut -d':' -f1,5 | sort | tr ":" " " | column -t 

#tr means change ":" to space " " 
#column -t means show as table
```

