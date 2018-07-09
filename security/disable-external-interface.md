# Disable External Interface

1. Get all disconnected interface, save to "t.txt".   for example  find ip 103.\*.\*.\*

```bash
salt '*' cmd.run 'IPCONFIG | FINDSTR /R \"Ethernet* Address.*103*\.[0-9]*\.[0-9][0-9]*\.[0-9][0-9]*\"' >t.txt
```

1. get list from server-list , for example all DB servers, save the hostname to "DB.txt". 
2. Put "t.txt" and "DB.tx" in same folder, and run 

{% code-tabs %}
{% code-tabs-item title="auto.au3" %}
```bash
#include<file.au3>
$arr=FileReadToArray("t.txt")
$DB=FileReadToArray("DB.txt")
 
_FileCreate("DB1.txt")
$DB1=FileOpen("DB1.txt",1)
For $item In $DB
    FileWrite($DB1,"salt '"& $item & "' " & " cmd.run 'ipconfig'" & @LF)
Next
 
_FileCreate("t1.txt")
$t1=FileOpen("t1.txt",1)
For $line In $arr
    If (Not StringInStr($line,"VN")) And (Not StringInStr($line,"Address")) And (Not StringInStr($line,"Ethernet")) Then
        FileWrite($t1,$line & @LF)
    ElseIf StringInStr($line,"VN") Then
        $ar_tmp=StringSplit($line,":",1)
        $temp_host=StringStripWS($ar_tmp[1],1+2)
 
    ElseIf StringInStr($line,"Ethernet") Then
        $ar_tmp=StringSplit($line,"adapter",1)
        $temp_adapter_t=StringStripWS($ar_tmp[2],1+2)
        $ar_tmp=StringSplit($temp_adapter_t,":",1)
        $temp_adapter=StringStripWS($ar_tmp[1],1+2)
 
    ElseIf StringInStr($line,"Address") Then
        For $item In $DB
            If $item==$temp_host Then
                FileWrite($t1,"salt '"& $temp_host & "' " & " cmd.run " & "'netsh interface set interface """ )
                FileWrite($t1,$temp_adapter & """ admin=disable'" & @LF)
            EndIf
        Next
 
    EndIf
 
Next
 
ShellExecute("notepad++","E:\DB1.txt")
ShellExecute("notepad++","E:\t1.txt")
```
{% endcode-tabs-item %}
{% endcode-tabs %}

1. excute commands in t1.txt 
2. check result , excute commands in DB1.txt 

