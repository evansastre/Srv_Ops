# Get Log

```bash
#!/bin/bash
echo "This is a small script to extract log from server group"
####Current Date
CurDate=$(date +%Y%m%d)
echo "Current Date: "$CurDate
#EPO="V-xxxO"
EPO="T-xxxO"
 
 
MyServers=$1
 
MyDateTimes=$2
###Test value
#MyServers="ArenaD01 Dungeon01 WorldD01"
#MyDateTimes="2018/05/25-17:00:30 2018/05/25-17:00:00"
#MyDateTimes="2018/06/05-17:00:30"
#CurDate=$CurDate'-Test'
 
echo 'MyServers: '$MyServers
echo 'MyDateTimes: '$MyDateTimes
echo ====================================================================================
 
 
 
####check minion return
check_minion_return() {
 
if [[ $Res == *"No response"* ]]; then
        echo $MyServer " No response"
        #exit
else
    echo $Res
fi
 
}
 
####push log
MyServers_arr=($MyServers)
for MyServer in ${MyServers_arr[@]}; do
    {
    UploadName=$MyServer
    MyDateTimes_arr=($MyDateTimes)
    for MyDateTime in ${MyDateTimes_arr[@]}; do
    {
        MyDate=$(date -d $(echo $MyDateTime | cut -d "-" -f 1) +%Y%m%d)
        MyTime=$(echo $MyDateTime | cut -d "-" -f 2)
        MyHour=$(date -d $(echo $MyDateTime | cut -d "-" -f 2) +%H)
        MyMin=$(date -d $(echo $MyDateTime | cut -d "-" -f 2) +%M)
        MySec=$(date -d $(echo $MyDateTime | cut -d "-" -f 2) +%S)
        echo $MyHour $MyMin $MySec
        echo $MyDateTime
        echo $MyDate
        
        if   [ "$MyHour" == "00" ] && [ "$MyMin" == "00" ] && [ "$MySec" == "00" ] ; then
            MyDate=$(date -d ""$MyDate" -1 day"  +%Y%m%d )
            MyHour=$(date -d ""$MyHour" -1 hour"  +%H )
            echo "Query Date: "$MyDate
            echo "Query Hour: "$MyHour
        elif [ "$MyHour" != "00" ] && [ "$MyMin" == "00" ] && [ "$MySec" == "00" ]  ; then
            MyHour=$(date -d ""$MyHour" -1 hour"  +%H )
            echo "Query Hour: "$MyHour
        fi
        #special servers, like AdminWeb
        if [ $MyServer == "AdminWeb" ]; then
            MyDateTime_NoMin=$(date -d $(echo $MyDateTime | cut -d "-" -f 1) +%Y-%m-%d)"T"$MyHour":"${MyMin%?}
            echo $MyDateTime_NoMin
            Query_Log_Name=$MyDate
        else
            MyDateTime_NoSec=${MyDateTime%:*}
            MyDateTime_NoMin=${MyDateTime_NoSec%?}
            Query_Log_Name=$MyDate'-'$MyHour
        fi
        
        logName=$(salt $MyServer cmd.run 'pushd E:\log\ && findstr /s /i /m /c:"'$MyDateTime_NoSec'" *'$Query_Log_Name'*.log | find /v "client" | find /v "guard"')
        Res=$logName
        check_minion_return
 
        logPath=$(echo "E:\\log\\"$(echo $logName |  cut -d ":" -f 2 |cut -d " " -f 2))
 
        Res=$(salt $MyServer cmd.run 'xcopy '$logPath' E:\'$UploadName'\ /y ')
        check_minion_return
 
        echo 'pushd E:\log\ && findstr /s /i /m /c:"'$MyDateTime_NoSec'" *'$Query_Log_Name'*.log | find /v "client" | find /v "guard"'
        echo "E:\\log\\"$(echo $logName |  cut -d ":" -f 2 |cut -d " " -f 2)
        echo 'xcopy '$logPath' E:\'$UploadName'\ /y '
 
        echo ====================================================================================
    }&
    done
    wait
 
    Res=$(salt $MyServer cmd.run 'pushd E:\ &&  7z a '$UploadName'.7z '$UploadName)
    check_minion_return
    Res=$(salt $MyServer cp.push 'E:\'$UploadName'.7z')
    check_minion_return
    Res=$(salt $MyServer cmd.run 'pushd E:\ &&  rd /s /q  '$UploadName' && del '$UploadName'.7z')
    check_minion_return
 
 
 
    mv -f '/var/cache/salt/master/minions/'$UploadName'/files/'$UploadName'.7z' /srv/salt
    Res=$(salt $EPO cmd.run 'mkdir C:\Log_to_xx\'$CurDate'\')
    check_minion_return
    echo $EPO cp.get_file salt://$UploadName\.7z 'C:\Log_to_xx\'$CurDate'\'$UploadName'.7z'
    Res=$(salt $EPO cp.get_file salt://$UploadName\.7z 'C:\Log_to_xx\'$CurDate'\'$UploadName'.7z')
    check_minion_return
    rm -f /srv/salt/$UploadName\.7z
    echo ====================================================================================
    }&
done
wait
```

