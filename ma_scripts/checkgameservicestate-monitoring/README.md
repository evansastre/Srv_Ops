---
description: >-
  Check game service state, if state turn to "INVALID", send alert to related
  department.
---

# CheckGameServiceState-Monitoring

1. [Create service for selenium](https://evansastre.gitbook.io/srvops/ma_scripts/checkgameservicestate-monitoring/create-service-for-selenium)
2. [Config mail sender on centos](https://evansastre.gitbook.io/srvops/ma_scripts/checkgameservicestate-monitoring/config-mail-sender-on-centos)
3. Script to get state.

{% code-tabs %}
{% code-tabs-item title="CheckServiceState.py" %}
```python
#!/bin/python
# -*- coding: utf-8 -*-
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
import time
from datetime import datetime
import sys
import os
import subprocess
import base64
 
monitorServer='10.**.**.**'
seleniumServer='10.**.**.**'
seleniumServer_Hostname="TH-**"
 
#kill process
def kill_process(myprocess):
    subprocess.call(["salt", seleniumServer_Hostname,"cmd.exec_code","python", \
                     "import psutil ; PROCNAME = '"+ myprocess +"' ; "+ \
                     "[proc.kill() for proc in psutil.process_iter() if proc.name() == PROCNAME]"])
#star selenium server
def restart_selenium_server():
    subprocess.call(["salt", seleniumServer_Hostname,"cmd.run","sc stop selenium & ping 127.0.0.1 -n 4 & sc start selenium"])
 
 
##############kill_process("chromedriver.exe")
 
 
#get input username and password
username="tw**"
password="***"
 
InGateD01='InGateD01'
InGateD02='InGateD02'
LobbyD='LobbyD'
LoGateD01='LoGateD01'
LoGateD02='LoGateD02'
 
Lobby_list=[InGateD01,\
            InGateD02,\
            LobbyD,\
            LoGateD01,\
            LoGateD02 ]
 
 
WorldDB01='WorldDB01'
WorldDB03='WorldDB03'
WorldDB04='WorldDB04'
Cache_list=[WorldDB01, \
            WorldDB03, \
            WorldDB04 ]
 
 
WorldD01='WorldD01'
WorldD03='WorldD03'
WorldD04='WorldD04'
Game_list=[ WorldD01, \
            WorldD03, \
            WorldD04 ]
 
 
ArenaLobby='ArenaLobby'
ArenaD01='ArenaD01'
ArenaD02='ArenaD02'
Dungeon01='Dungeon01'
Dungeon02='Dungeon02'
 
Arena_list=[ ArenaLobby,\
             ArenaD01,\
             ArenaD02,\
             Dungeon01, \
             Dungeon02 ]
 
 
AccountIn='AccountIn'
Achieve='Achieve'
CacheGate='CacheGate'
MarkDA='MarkDARA'
MarketDD='MarketDD'
MarkRA='MarkDARA'
MarketRD='MarketRD'
PostOffD='PostOffD'
Rank='Rank'
DuelBot='DuelBot'
Economy_list=[ AccountIn,\
               Achieve,\
               CacheGate,\
               MarkDA,\
               MarketDD,\
               MarkRA,\
               MarketRD,\
               PostOffD,\
               Rank,\
               DuelBot ]
 
 
 
def state_check(seq,name):
    try:
    state=(browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(seq+1)+']/td[5]')).text
        print name+ ": "+state
    except:
        print "Get state fail. "
 
    if state=="INVALID":
        os.system('echo "Service '+name+' is Invalid!!! Please check right now!" | mutt -e "my_hdr from:thlive<master@th.com>" -s " game service check" abc@domain.com')
        Msg=name+' INVALID '+ str(datetime.now())
        print Msg
        with open('/srv/salt/CheckServiceState/CheckServiceState.log',"a+") as logfile:
            logfile.write(Msg+'\n')
 
def page_state_check(list_name,length):
    for i in range(0,length):
        state_check(i,list_name[i])
    #print i,list_name[i]
 
 
def connect_selenium_server():
 
    try:
        global  browser
        browser= webdriver.Remote(
                command_executor="http://"+ seleniumServer +":4444/wd/hub",
                desired_capabilities={'browserName': 'chrome',
                                             'version': '2',
                                             'javascriptEnabled': True})
    except:
        global restart_time
        if restart_time>2:
            print "Selenium server restart fail."
            #email alert
            os.system('echo "Selenium server restart fail. Please check." | mutt -e "my_hdr from:thlive<master@th.com>" -s "selenium check" abc@domain.com')
            exit()
        else:
            restart_time+=1
        kill_process("chromedriver.exe")
        kill_process("java.exe")
        restart_selenium_server()
        print "restart time: "+str(restart_time)
        print "Connection error. Webdriver restarted"
        connect_selenium_server()
        #return
 
def LiveService_state_check():
    kill_process("chromedriver.exe")
    #kill_process("conhost.exe")
    global restart_time
    restart_time=0
 
    connect_selenium_server()
 
    ####open website          
    try:
         
        browser.get('http://'+username+':'+password+'@'+ monitorServer+'/monitoring/DaemonLobby.aspx')
         
        print(browser.title+'\n')
        browser.implicitly_wait(60)
    except:
        print "Open Website Error."
 
    time.sleep(5)
 
     
    browser.find_element_by_link_text('Lobby').click() 
    browser.implicitly_wait(10)
    print 'Lobby'
    page_state_check(Lobby_list,len(Lobby_list))
 
    browser.find_element_by_link_text('Cache').click()
    browser.implicitly_wait(10)
    print 'Cache'
    page_state_check(Cache_list,len(Cache_list))  
  
    browser.find_element_by_link_text('Game').click()
    browser.implicitly_wait(10)
    print 'Game'
    page_state_check(Game_list,len(Game_list))
     
    browser.find_element_by_link_text('Arena').click()
    browser.implicitly_wait(10)
    print 'Arena'
    page_state_check(Arena_list,len(Arena_list))
     
    browser.find_element_by_link_text('Economy').click()
    browser.implicitly_wait(10)
    print 'Economy'
    page_state_check(Economy_list,len(Economy_list))   
 
    browser.quit()   
 
LiveService_state_check()
```
{% endcode-tabs-item %}
{% endcode-tabs %}

If script return "INVALID", it will write to log file, use zabbix monitor that file and set alert. At the same time email alert will send to all related department.

4.Set schedule, run every two minutes.

```bash
vim /etc/crontab
*/2  *  *  *  *  root scl enable python27 "python /srv/salt/CheckServiceState/CheckServiceState.py"
```

