# Game Service Version

## For LIVE

{% code-tabs %}
{% code-tabs-item title="GameServiceVersion\_before.sh" %}
```bash
cd /srv/salt/LIVE_Scripts/GameServiceVersion/
scl enable python27 "python /srv/salt/LIVE_Scripts/GameServiceVersion/GameServiceVersion.py | tee GameServiceVersion_before.txt"
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="GameServiceVersion\_after.sh" %}
```bash
cd /srv/salt/LIVE_Scripts/GameServiceVersion/
 
scl enable python27 "python /srv/salt/LIVE_Scripts/GameServiceVersion/GameServiceVersion.py | tee GameServiceVersion_after.txt"
 
sdiff -E  GameServiceVersion_before.txt GameServiceVersion_after.txt
if [[ $? == "0" ]]
then
    echo "=====================No Game Service Version Change============================"
else
    echo "============================Version Change====================================="
    sdiff -E -s GameServiceVersion_before.txt GameServiceVersion_after.txt
fi
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="GameServiceVersion.py" %}
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
 
monitorServer='10.xx.xx.xx'
seleniumServer='10.xx.xx.xx'
seleniumServer_Hostname="xxx-eO"
 
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
     
username="twxxx"
password="xxxxxxxxxx"
 
 
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
 
def version_check(seq,name):
    try:
    state=(browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(seq+1)+']/td[6]')).text
        print name+ ": "+state
    except:
        print "Get state fail. "
 
def page_version_check(list_name,length):
    for i in range(0,length):
        version_check(i,list_name[i])
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
            os.system('echo "Selenium server restart fail, please check." | mutt -e "my_hdr from:thlivesalt<saltmaster@th.com>" -s "game service check" abc@domain.com')
        #email alert
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
 
def LiveService_version_check():
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
    page_version_check(Lobby_list,len(Lobby_list))
 
    browser.find_element_by_link_text('Cache').click()
    browser.implicitly_wait(10)
    print 'Cache'
    page_version_check(Cache_list,len(Cache_list))  
  
    browser.find_element_by_link_text('Game').click()
    browser.implicitly_wait(10)
    print 'Game'
    page_version_check(Game_list,len(Game_list))
     
    browser.find_element_by_link_text('Arena').click()
    browser.implicitly_wait(10)
    print 'Arena'
    page_version_check(Arena_list,len(Arena_list))
     
    browser.find_element_by_link_text('Economy').click()
    browser.implicitly_wait(10)
    print 'Economy'
    page_version_check(Economy_list,len(Economy_list))   
 
    browser.quit()   
 
LiveService_version_check()
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## For Dev/Stage

{% code-tabs %}
{% code-tabs-item title="GameServiceVersion\_before.sh" %}
```bash
cd /srv/salt/QA_script/GameServiceVersion/
folder_abs=/srv/salt/QA_script/GameServiceVersion/
folder=QA_script/GameServiceVersion/
Env=TH
 
salt $Env'-Func' cmd.script salt://$folder'GameServiceVersion_Func.bat'
salt $Env'-Func' cmd.run 'type D:\GameServiceVersion.txt'  | grep -v "GameName" > $folder_abs'GameServiceVersion_before.txt'
 
salt $Env'-Game01' cmd.script salt://$folder'GameServiceVersion_Game01.bat'
salt $Env'-Game01' cmd.run 'type D:\GameServiceVersion.txt'  | grep -v "GameName" > $folder_abs'GameServiceVersion_before_Game01.txt'
 
salt $Env'-Game02' cmd.script salt://$folder'GameServiceVersion_Game02.bat'
salt $Env'-Game02' cmd.run 'type D:\GameServiceVersion.txt'  | grep -v "GameName" > $folder_abs'GameServiceVersion_before_Game02.txt'
 
 
sdiff -E -s GameServiceVersion_before_Game01.txt GameServiceVersion_before_Game02.txt
 
if [[ $? == "0" ]]
then
    echo >> GameServiceVersion_before.txt
    cat GameServiceVersion_before_Game01.txt >> GameServiceVersion_before.txt
    rm -f GameServiceVersion_before_Game0*.txt
else
    echo Game01 and Game02 service file version different!!!!!!!!!!!!
    exit
fi
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="GameServiceVersion\_after.sh" %}
```bash
GameServiceVersion_after
cd /srv/salt/QA_script/GameServiceVersion/
folder_abs=/srv/salt/QA_script/GameServiceVersion/
folder=QA_script/GameServiceVersion/
Env=TH
 
salt $Env'-Func' cmd.script salt://$folder'GameServiceVersion_Func.bat'
salt $Env'-Func' cmd.run 'type D:\GameServiceVersion.txt'  | grep -v "GameName" > $folder_abs'GameServiceVersion_after.txt'
 
salt $Env'-Game01' cmd.script salt://$folder'GameServiceVersion_Game01.bat'
salt $Env'-Game01' cmd.run 'type D:\GameServiceVersion.txt'  | grep -v "GameName" > $folder_abs'GameServiceVersion_after_Game01.txt'
 
salt $Env'-Game02' cmd.script salt://$folder'GameServiceVersion_Game02.bat'
salt $Env'-Game02' cmd.run 'type D:\GameServiceVersion.txt'  | grep -v "GameName" > $folder_abs'GameServiceVersion_after_Game02.txt'
 
 
sdiff -E -s GameServiceVersion_after_Game01.txt GameServiceVersion_after_Game02.txt
 
if [[ $? == "0" ]]
then
    echo >> GameServiceVersion_after.txt
    cat GameServiceVersion_after_Game01.txt >> GameServiceVersion_after.txt
    rm -f GameServiceVersion_after_Game0*.txt
else
    echo Game01 and Game02 service file version different!!!!!!!!!!!!
    exit
fi
 
 
sdiff -E  GameServiceVersion_before.txt GameServiceVersion_after.txt
if [[ $? == "0" ]]
then
    echo "=====================No Game Service Version Change============================"
else
    echo "============================Version Change====================================="
    sdiff -E -s GameServiceVersion_before.txt GameServiceVersion_after.txt
fi

```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="GameServiceVersion\_Func.bat" %}
```bash
> D:\GameServiceVersion.txt set /p="AccountInventoryDaemon " < nul
wmic datafile where name="D:\\Service\\AccountInventoryDaemon\\bin\\AccountInventoryDaemon.exe" get Version /value | find "Version" >> D:\GameServiceVersion.txt
 
>> D:\GameServiceVersion.txt set /p="AchievementDaemon " < nul
wmic datafile where name="D:\\Service\\AchievementDaemon\\bin\\AchievementDaemon.exe" get Version /value | find "Version" >> D:\GameServiceVersion.txt
 
>> D:\GameServiceVersion.txt set /p="ArenaLobby " < nul
wmic datafile where name="D:\\Service\\ArenaLobby\\bin\\ArenaLobby.exe" get Version /value | find "Version" >> D:\GameServiceVersion.txt
 
>> D:\GameServiceVersion.txt set /p="CacheGate " < nul
wmic datafile where name="D:\\Service\\CacheGate\\bin\\CacheGate.exe" get Version /value | find "Version" >> D:\GameServiceVersion.txt
 
>> D:\GameServiceVersion.txt set /p="DuelbotDaemon " < nul
wmic datafile where name="D:\\Service\\DuelbotDaemon\\bin\\DuelbotDaemon.exe" get Version /value | find "Version" >> D:\GameServiceVersion.txt
 
>> D:\GameServiceVersion.txt set /p="InfoGateDaemon " < nul
wmic datafile where name="D:\\Service\\InfoGateDaemon\\bin\\InfoGateDaemon.exe" get Version /value | find "Version" >> D:\GameServiceVersion.txt
 
>> D:\GameServiceVersion.txt set /p="LobbyDaemon " < nul
wmic datafile where name="D:\\Service\\LobbyDaemon\\bin\\LobbyDaemon.exe" get Version /value | find "Version" >> D:\GameServiceVersion.txt
 
>> D:\GameServiceVersion.txt set /p="LobbyGate " < nul
wmic datafile where name="D:\\Service\\LobbyGate\\bin\\LobbyGate.exe" get Version /value | find "Version" >> D:\GameServiceVersion.txt
 
>> D:\GameServiceVersion.txt set /p="ManagementDaemon " < nul
wmic datafile where name="D:\\Service\\ManagementDaemon\\bin\\ManagementDaemon.exe" get Version /value | find "Version" >> D:\GameServiceVersion.txt
 
>> D:\GameServiceVersion.txt set /p="ManagementAgent " < nul
wmic datafile where name="D:\\Service\\ManagementAgent\\bin\\ManagementAgent.exe" get Version /value | find "Version" >> D:\GameServiceVersion.txt
 
>> D:\GameServiceVersion.txt set /p="MarketAgent(MarketDealerAgent) " < nul
wmic datafile where name="D:\\Service\\MarketDealerAgent\\bin\\MarketAgent.exe" get Version /value  | find "Version" >> D:\GameServiceVersion.txt
>> D:\GameServiceVersion.txt set /p="MarketAgent(MarketReaderAgent) " < nul
wmic datafile where name="D:\\Service\\MarketReaderAgent\\bin\\MarketAgent.exe" get Version /value  | find "Version" >> D:\GameServiceVersion.txt
 
>> D:\GameServiceVersion.txt set /p="MarketDealerDaemon " < nul
wmic datafile where name="D:\\Service\\MarketDealerDaemon\\bin\\MarketDealerDaemon.exe" get Version /value  | find "Version" >> D:\GameServiceVersion.txt
 
>> D:\GameServiceVersion.txt set /p="MarketReaderDaemon " < nul
wmic datafile where name="D:\\Service\\MarketReaderDaemon\\bin\\MarketReaderDaemon.exe" get Version /value  | find "Version" >> D:\GameServiceVersion.txt
 
>> D:\GameServiceVersion.txt set /p="PostOfficeDaemon " < nul
wmic datafile where name="D:\\Service\\PostOfficeDaemon\\bin\\PostOfficeDaemon.exe" get Version /value  | find "Version" >> D:\GameServiceVersion.txt
 
>> D:\GameServiceVersion.txt set /p="RankingDaemon " < nul
wmic datafile where name="D:\\Service\\RankingDaemon\\bin\\RankingDaemon.exe" get Version /value  | find "Version" >> D:\GameServiceVersion.txt
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="GameServiceVersion\_Game01.bat" %}
```bash
> D:\GameServiceVersion.txt set /p="CacheDaemon " < nul
wmic datafile where name="D:\\Service\\CacheDaemon01\\bin\\CacheDaemon.exe" get Version /value | find "Version" >> D:\GameServiceVersion.txt
 
 
>> D:\GameServiceVersion.txt set /p="GameDaemon " < nul
wmic datafile where name="D:\\Service\\GameDaemon01\\bin\\GameDaemon.exe" get Version /value | find "Version" >> D:\GameServiceVersion.txt
>> D:\GameServiceVersion.txt set /p="GameDaemon " < nul
wmic datafile where name="D:\\Service\\ArenaDaemon01\\bin\\GameDaemon.exe" get Version /value | find "Version" >> D:\GameServiceVersion.txt
 
 
>> D:\GameServiceVersion.txt set /p="ManagementAgent " < nul
wmic datafile where name="D:\\Service\\ManagementAgent\\bin\\ManagementAgent.exe" get Version /value | find "Version" >> D:\GameServiceVersion.txt
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="GameServiceVersion\_Game02.bat" %}
```bash
> D:\GameServiceVersion.txt set /p="CacheDaemon " < nul
wmic datafile where name="D:\\Service\\CacheDaemon02\\bin\\CacheDaemon.exe" get Version /value | find "Version" >> D:\GameServiceVersion.txt
 
 
>> D:\GameServiceVersion.txt set /p="GameDaemon " < nul
wmic datafile where name="D:\\Service\\GameDaemon02\\bin\\GameDaemon.exe" get Version /value | find "Version" >> D:\GameServiceVersion.txt
>> D:\GameServiceVersion.txt set /p="GameDaemon " < nul
wmic datafile where name="D:\\Service\\ArenaDaemon02\\bin\\GameDaemon.exe" get Version /value | find "Version" >> D:\GameServiceVersion.txt
 
 
>> D:\GameServiceVersion.txt set /p="ManagementAgent " < nul
wmic datafile where name="D:\\Service\\ManagementAgent\\bin\\ManagementAgent.exe" get Version /value | find "Version" >> D:\GameServiceVersion.txt
```
{% endcode-tabs-item %}
{% endcode-tabs %}

