# Disable Disconnected Interface

1.Get all disconnected interface, save to t.txt

```bash
salt '*' cmd.run ' netsh interface show interface | find "Disconnected" '
```

2.Edit t.txt to command line, Or can use auto.au3.

{% code-tabs %}
{% code-tabs-item title="auto.au3" %}
```bash
#include<file.au3>
$arr=FileReadToArray("t.txt")
 
_FileCreate("t1.txt")
$t1=FileOpen("t1.txt",1)
For $line In $arr
    If (Not StringInStr($line,":")) And (Not StringInStr($line,"Dedicated")) Then
        FileWrite($t1,$line & @LF)
    ElseIf StringInStr($line,":") Then
        $ar_tmp=StringSplit($line,":",1)
        $temp_name=StringStripWS($ar_tmp[1],1+2)
         
    ElseIf StringInStr($line,"Dedicated") Then
        $ar_tmp=StringSplit($line,"Dedicated",1)
        $interface=StringStripWS($ar_tmp[2],1+2)
        FileWrite($t1,"salt '"& $temp_name & "' " & " cmd.run " & "'netsh interface set interface """ )
        FileWrite($t1,$interface & """ admin=disable'" & @LF)
    EndIf
     
Next
 
ShellExecute("notepad++","E:\t1.txt")

```
{% endcode-tabs-item %}
{% endcode-tabs %}

3.excute commands in t1.txt

4.check result 

```bash
salt '*' cmd.run ' netsh interface show interface | find "Disconnected" '
```

We can see every disconnected interface is in "Disabled" status.

