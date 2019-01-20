# CheckOutBound-Monitoring

Run every two minute in crontab job on salt master. Check if minion's outbound open or minion disconnected.  


{% code-tabs %}
{% code-tabs-item title="CheckOutBound.sh" %}
```bash

#!/bin/bash

####define 
Sender=$(hostname)"<saltmaster@xxx.com>"
Reciver="abc@xxx.com"
group_windows="OS-Windows"
group_linux="OS-Linux"

date=$(date "+%Y-%m-%d_%H:%M:%S")
lastlog=$(ls -l /var/log/outboundcheck | tail -n 1 | awk '{print $9}')
RecentAlert=False
content_lastlog=""
if [[ -n "$lastlog" ]]; then 
    date_lastlog=$(echo $lastlog |  cut -c 14-32 )
    echo $date_lastlog
    time=$((($(date +%s -d "$(echo $date | sed 's/_/ /g')")-$(date +%s -d "$(echo $date_lastlog | sed 's/_/ /g')" ))/60 ))
    echo time: $time
    content_lastlog=""
    if [[ $time -le 3 ]]; then
        RecentAlert=True
        content_lastlog=$(cat '/var/log/outboundcheck/'$lastlog)
    fi
fi

echo RecentAlert: $RecentAlert

outboundcheck() { 
    echo "OS:"$OS" Host:"$Host  
    if [[ $OS == *"Windows"* ]] ; then
        arg="-n"
    elif [[ $OS == *"Linux"* ]] ; then
        arg="-c"
    fi
   
    result=$(salt $Host cmd.run 'ping '$arg' 1 8.8.8.8')
    echo $result
    if [[ $result == *"Not connected"* ]] ; then
        msg="$Host salt-minion not connected ! Please Check . "
        echo $msg | tee -a '/var/log/outboundcheck/outboundcheck'$date'.log'
	if [[ "$RecentAlert" == "True" ]] && grep -q "$Host" '/var/log/outboundcheck/'$lastlog ; then
            echo Sending!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
            echo $msg    |  mutt -e "my_hdr from:"$Sender -s "[Warning] Outbound is Open !" $Reciver
        else
            echo Not send this time.
        fi
    elif [[ $result == *"No response"* ]] ; then
        echo "$Host is no response!"
    elif [[ $result == *"General failure"* ]] ; then
        echo "$Host outbound is closed."
    elif [[ $result == *"Packets: Sent = 1, Received = 1, Lost = 0 (0% loss)"* ]]; then
        msg="$Host's outbound is open ! Please Check immediately! "
	echo $msg | tee -a '/var/log/outboundcheck/outboundcheck'$date'.log'
	if [[ "$RecentAlert" == "True" ]] && grep -q "$Host" '/var/log/outboundcheck/'$lastlog ; then
            echo Sending!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
            echo $msg    |  mutt -e "my_hdr from:"$Sender -s "[Warning] Outbound is Open !" $Reciver
        else
            echo Not send this time.
        fi
    elif [[ $result == *"1 packets transmitted, 1 received, 0% packet loss"* ]];then
        msg="$Host's outbound is open ! Please Check immediately! "
	echo $msg | tee -a '/var/log/outboundcheck/outboundcheck'$date'.log'
	#echo RecentAlert: $RecentAlert
	#echo msg: $msg
	#echo content_lastlog: $content_lastlog
	#echo grep -q "$Host" '/var/log/outboundcheck/'$lastlog
        if [[ "$RecentAlert" == "True" ]] && grep -q "$Host" '/var/log/outboundcheck/'$lastlog ; then
	    echo Sending!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
            echo $msg    |  mutt -e "my_hdr from:"$Sender -s "[Warning] Outbound is Open !" $Reciver
	else
            echo Not send this time.
        fi
    else
        echo "$Host outbound is closed."
    fi
}

main() {
    OS_Windows=$(salt -N $group_windows test.ping | grep ":" |cut -d ":" -f 1)
    OS_Linux=$(salt -N $group_linux test.ping | grep ":" |cut -d ":" -f 1)
    mkdir -p /var/log/outboundcheck/

    for Host in $OS_Windows; do
    {
    	OS="Windows"
    	outboundcheck
    }&
    done
    wait

    for Host in $OS_Linux; do
    {
    	OS="Linux"
	outboundcheck
    }&
    done
    wait

    echo "=============Result==============="
    if [ ! -f '/var/log/outboundcheck/outboundcheck'$date'.log' ]; then
	echo "No Alert"
    else
	cat '/var/log/outboundcheck/outboundcheck'$date'.log'
    fi
}
main

```
{% endcode-tabs-item %}
{% endcode-tabs %}

