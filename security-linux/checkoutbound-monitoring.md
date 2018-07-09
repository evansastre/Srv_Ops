# CheckOutBound-Monitoring

Run every two minute in crontab job on salt master. Check if minion's outbound open or minion disconnected.  


{% code-tabs %}
{% code-tabs-item title="CheckOutBound.sh" %}
```bash
#!/bin/bash

####define
Sender="xxx<saltmaster@xxx.com>"
Reciver="xxx@xxx.com"
group_windows="OS-Windows"
group_linux="OS-Linux"
 
date=`date "+%Y-%m-%d_%H:%M:%S"`
 
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
        echo "$Host salt-minion not connected ! Please Check . " | tee -a '/var/log/outboundcheck/outboundcheck'$date'.log'
        echo "$Host salt-minion not connected ! Please Check . " | mutt -e "my_hdr from:"$Sender -s "[Info] Salt-Minion Not Connected !" $Reciver
    elif [[ $result == *"No response"* ]] ; then
        echo "$Host is no response!"
    elif [[ $result == *"General failure"* ]] ; then
        echo "$Host outbound is closed."
    elif [[ $result == *"Packets: Sent = 1, Received = 1, Lost = 0 (0% loss)"* ]]; then
        echo "$Host's outbound is open ! Please Check immediately! " | tee -a '/var/log/outboundcheck/outboundcheck'$date'.log'
        echo "$Host's outbound is open ! Please Check immediately! " | mutt -e "my_hdr from:"$Sender -s "[Warning] Outbound is Open !" $Reciver
    elif [[ $result == *"1 packets transmitted, 1 received, 0% packet loss"* ]];then
    echo "$Host's outbound is open ! Please Check immediately! " | tee -a '/var/log/outboundcheck/outboundcheck'$date'.log'
        echo "$Host's outbound is open ! Please Check immediately! " | mutt -e "my_hdr from:"$Sender -s "[Warning] Outbound is Open !" $Reciver
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

