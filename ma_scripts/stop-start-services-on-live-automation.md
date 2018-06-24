# Stop/Start services on Live automation



Use selenium to operate service management website.

### Prepare: {#Stop/StartservicesonLiveautomation-Prepare:}

#### install python support units on saltmaster server {#Stop/StartservicesonLiveautomation-installpythonsupportunitsonsaltmasterserver}

\# install Python 2.7

1. sudo yum install centos-release-scl \# install SCL 
2. sudo yum install python27
3. scl enable python27 bash
4. pip install --upgrade pip
5. yum install gcc
6. pip install psutil
7. pip install -U selenium  

Set firewall rule on AdminWeb and PA to enable communication between saltmaster and AdminWeb.

#### install selenium and java support units on webadmin server \(QA:app1  Live:webadmin \) {#Stop/StartservicesonLiveautomation-installseleniumandjavasupportunitsonwebadminserver(QA:app1Live:webadmin)}

selenium-server:install JRE

selenium-server file need:

1. selenium-server: [http://selenium-release.storage.googleapis.com/3.6/selenium-server-standalone-3.6.0.jar](http://selenium-release.storage.googleapis.com/3.6/selenium-server-standalone-3.6.0.jar) or find latest version below: [http://www.seleniumhq.org/download/](http://www.seleniumhq.org/download/)
2. chrome webdriver [http://www.seleniumhq.org/docs/03\_webdriver.jsp](http://www.seleniumhq.org/docs/03_webdriver.jsp) or [https://sites.google.com/a/chromium.org/chromedriver/](https://sites.google.com/a/chromium.org/chromedriver/)
3. java JRE [http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html)

{% code-tabs %}
{% code-tabs-item title="start\_selenium\_server.bat" %}
```bash
java  -jar selenium-server-standalone-3.6.0.jar
pause >nul
```
{% endcode-tabs-item %}
{% endcode-tabs %}

#### documents to learn python and selenium {#Stop/StartservicesonLiveautomation-documentstolearnpythonandselenium}

selenium:

[http://selenium-python.readthedocs.io/getting-started.html](http://selenium-python.readthedocs.io/getting-started.html)

[http://www.seleniumhq.org/docs/](http://www.seleniumhq.org/docs/)

python:

[https://www.tutorialspoint.com/python/index.htm](https://www.tutorialspoint.com/python/index.htm)

### Test on QA {#Stop/StartservicesonLiveautomation-TestonQA}

[stop\_Service\_VN\_Stage.py](http://gtoconfluence.garenanow.com:8090/download/attachments/3543728/stop_Service_VN_Stage.py?version=1&modificationDate=1507805184000&api=v2)

[start\_Service\_VN\_Stage.py](http://gtoconfluence.garenanow.com:8090/download/attachments/3543728/start_Service_VN_Stage.py?version=1&modificationDate=1507805184000&api=v2)

upload script to saltmaster

#### change in different area {#Stop/StartservicesonLiveautomation-changeindifferentarea}

1.username password for server \[not in python script\]  
2.monitorServer and seleniumServer   
3.QA use 'servicename' but live use 'hostname', change xpath 2 to 1  
4.all hostname, seq and list define  
5.in main function, change all excute Seq

#### step to update stop&start python script {#Stop/StartservicesonLiveautomation-steptoupdatestop&startpythonscript}

### 1.

```bash
cd /srv/salt/QA_script/
rm -f stop_Service_Stage.py 
rm -f stop_Service_Stage.pyc
rm -f start_Service_Stage.py 
rm -f start_Service_Stage.pyc 
```

### 2.upload script

### 3.

```bash
mv /home/huangsl/stop_Service_Stage.py /srv/salt/QA_script/
mv /home/huangsl/start_Service_Stage.py /srv/salt/QA_script/
chmod +x stop_Service_Stage.py
chmod +x start_Service_Stage.py
```

### 4.

```text
python -m compileall .
chmod +x stop_Service_Stage.pyc
chmod +x start_Service_Stage.pyc
```

### 5.

```bash
rm -f stop_Service_Stage.py
rm -f start_Service_Stage.py
```

###  6.excute

adminweb:

open selenium-server

saltmaster:

```bash
scl enable python27 bash
python stop_Service_Stage.pyc [encoded account] [encoded password] [your name in trust list]
python start_Service_Stage.pyc [encoded account] [encoded password] [your name in trust list]
```

for example:

\[VN QA\]

```bash
scl enable python27 bash
python stop_Service_Stage.pyc s8nZzs_c2OjXwuHh1w== 28bWxpG0p-PUzNzas9XKk9TN283G [name] 
python start_Service_Stage.pyc s8nZzs_c2OjXwuHh1w== 28bWxpG0p-PUzNzas9XKk9TN283G [name]
```

can use force mode by:

```bash
scl enable python27 bash
python stop_Service_Stage.pyc s8nZzs_c2OjXwuHh1w== 28bWxpG0p-PUzNzas9XKk9TN283G huangsl --forcre
python start_Service_Stage.pyc s8nZzs_c2OjXwuHh1w== 28bWxpG0p-PUzNzas9XKk9TN283G huangsl --forcre
```

{% code-tabs %}
{% code-tabs-item title="stop\_Service\_LIVE.py" %}
```python
#!/bin/python
# -*- coding: utf-8 -*-
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
import time
import sys
import subprocess
import base64
 
FlagForceMode=False
monitorServer='10.xx.xx.xx'
seleniumServer='10.xx.xx.xx'
 
#kill chromedriver process
def kill_process(myprocess):
    subprocess.call(["salt", "AdminWeb","cmd.exec_code","python", \
                     "import psutil ; PROCNAME = '"+ myprocess +"' ; "+ \
                     "[proc.kill() for proc in psutil.process_iter() if proc.name() == PROCNAME]"])
 
 
##############kill_process("chromedriver.exe")
 
users=['user1','user2','user3','user4','user5','user6']
 
#get input username and password
def decode(key, enc):
    dec = []
    enc = base64.urlsafe_b64decode(enc)
    for i in range(len(enc)):
        key_c = key[i % len(key)]
        dec_c = chr((256 + ord(enc[i]) - ord(key_c)) % 256)
        dec.append(dec_c)
    return "".join(dec)
     
if len(sys.argv)==4 or len(sys.argv)==5:
    try:
        username=decode("decodekey", str(sys.argv[1]))
        password=decode("decodekey", str(sys.argv[2]))
    user=sys.argv[3]
        if (len(sys.argv)==5 and (sys.argv[4]=="--Force" or sys.argv[4]=="--force" or  sys.argv[4]=="--FORCE") ):
            FlagForceMode=True
    except:
        print "username or password input Error"
        quit()
else:
    print "Please check arguments.Usage:python script.py [username] [password] [your_name]."
    quit()
 
     
def check_user():
    for i in users:
        if i==user:
            return
    print "You are not a trusted user."
    quit()
check_user()
 
 
 
InGateD01_seq=1
InGateD02_seq=2
LobbyD_seq=3
LoGateD01_seq=4
LoGateD02_seq=5
InGateD01='InGateD01'
InGateD02='InGateD02'
InGateD_list=[[str(InGateD01_seq),InGateD01],\
                    [str(InGateD02_seq),InGateD02]]
InGateD_list_len=len(InGateD_list)
LobbyD='LobbyD'
LoGateD01='LoGateD01'
LoGateD02='LoGateD02'
LoGateD_list=[[str(LoGateD01_seq),LoGateD01],\
                    [str(LoGateD02_seq),LoGateD02]]
LoGateD_list_len=len(LoGateD_list)
 
 
WorldDB01_seq=1
WorldDB03_seq=2
WorldDB04_seq=3
 
 
WorldDB01='WorldDB01'
WorldDB03='WorldDB03'
WorldDB04='WorldDB04'
 
 
 
WorldDB_list=[[str(WorldDB01_seq),WorldDB01], \
                    [str(WorldDB03_seq),WorldDB03], \
                    [str(WorldDB04_seq),WorldDB04]]
 
WorldDB_list_len=len(WorldDB_list)
 
 
WorldD01_seq=1
WorldD03_seq=2
WorldD04_seq=3
 
 
WorldD01='WorldD01'
WorldD03='WorldD03'
WorldD04='WorldD04'
 
 
WorldD_list=[ [str(WorldD01_seq),WorldD01], \
                    [str(WorldD03_seq),WorldD03], \
                    [str(WorldD04_seq),WorldD04]]
WorldD_list_len=len(WorldD_list)
 
 
ArenaLobby_seq=1
ArenaD01_seq=2
ArenaD02_seq=3
Dungeon01_seq=4
Dungeon02_seq=5
ArenaLobby='ArenaLobby'
ArenaD01='ArenaD01'
ArenaD02='ArenaD02'
ArenaD_list=[[str(ArenaD01_seq),ArenaD01],\
                   [str(ArenaD02_seq),ArenaD02]]
ArenaD_list_len=len(ArenaD_list)
Dungeon01='Dungeon01'
Dungeon02='Dungeon02'
Dungeon_list=[[str(Dungeon01_seq),Dungeon01],\
                    [str(Dungeon02_seq),Dungeon02]]
Dungeon_list_len=len(Dungeon_list)
 
 
AccountIn_seq=1
Achieve_seq=2
CacheGate_seq=3
#CraftD_seq=4
MarkDA_seq=4
MarketDD_seq=5
MarkRA_seq=6
MarketRD_seq=7
PostOffD_seq=8
Rank_seq=9
DuelBot_seq=10
AccountIn='AccountIn'
Achieve='Achieve'
CacheGate='CacheGate'
#CraftD='CraftD'
MarkDA='MarkDARA'
MarketDD='MarketDD'
MarkRA='MarkDARA'
MarketRD='MarketRD'
PostOffD='PostOffD'
Rank='Rank'
DuelBot='DuelBot'
 
 
def cooldown_click(seq,name):
    state="NOT RUNNING"
    state_orin=state
     
    while True:
        if state=="RUNNING" :
            print "Retryed"
        if state=="COOLDOWNED" or state=="STOPPED":
            return
        try:
            state=(browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(seq)+']/td[5]')).text
            element_name=(browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(seq)+']/td[1]')).text
            print element_name
            if element_name==name:
                elem_button=browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+ str(seq) +']/td[4]/button[2]')
                elem_button.click()  #click cooldown
 
                 
      
        except:
            print name+" cooldown failed\n retrying..."
            time.sleep(1)
            continue
        break
    alert = browser.switch_to.alert
    print alert.text+'\n'
    #alert.dismiss()
    alert.accept()
    time.sleep(1)
    alert = browser.switch_to.alert
    alert.accept()
    if FlagForceMode==True:
        time.sleep(1)
        alert = browser.switch_to.alert
        alert.accept()
    
def cooldown_check(seq,name):
    #state=(browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(seq)+']/td[5]')).text
    #print name+ ": "+state
    state="NOT COOLDOWNED"
    state_orin=state
     
    while state!="COOLDOWNED":
        if state=="STOPPED":
            return
        time.sleep(1)
        try:
            state=(browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(seq)+']/td[5]')).text
            print name+ ": "+state
        except:
            state=state_orin
            #print name+ ": "+state
     
    print name+ ": "+state
 
def stop_click(seq,name):
    try:
        #state=(browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(seq)+']/td[5]')).text
        #print name+ ": "+state
        state="NOT COOLDOWNED"
        state_orin=state
 
        while True:
            if state=="COOLDOWNED" :
                print "Retryed"
            if state=="STOPPED":
                return
            try:
                state=(browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(seq)+']/td[5]')).text
                elem_button=browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+ str(seq) +']/td[4]/button')
                elem_button.click()  #click STOP
                 
            except:
                time.sleep(1)
                continue
            break
         
        alert = browser.switch_to.alert
        print alert.text+'\n'
        #alert.dismiss()
        alert.accept()
        time.sleep(1)
        alert = browser.switch_to.alert
        alert.accept()
        if FlagForceMode==True:
            time.sleep(1)
            alert = browser.switch_to.alert
            alert.accept()
  
    except:
        print name+" stop failed\n  retrying..."
        quit()   
         
def stop_check(seq,name):
    state="NOT STOPPED"
    state_orin=state
     
    while state!="STOPPED":
        time.sleep(1)
        try:
            state=(browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(seq)+']/td[5]')).text
            print name+ ": "+state
         
        except:
            state=state_orin
            #print name+ ": "+state
     
    print name+ ": "+state
 
 
def cooldown_and_stop(seq,name):
    cooldown_click(seq,name)
    cooldown_check(seq,name)
    stop_click(seq,name)
    stop_check(seq,name)
 
def cooldown_and_stop_mult(list_name,length):
    for i in range(0,length):
        cooldown_click(list_name[i][0],list_name[i][1])
    for i in range(0,length):
        cooldown_check(list_name[i][0],list_name[i][1])
    for i in range(0,length):
        stop_click(list_name[i][0],list_name[i][1])
    for i in range(0,length):
        stop_check(list_name[i][0],list_name[i][1])
 
def cooldown_and_stop_dealer():
     
    cooldown_click(MarketDD_seq,MarketDD)
    cooldown_check(MarketDD_seq,MarketDD)
    time.sleep(1)
     
    cooldown_and_stop(MarkDA_seq,MarkDA)
    time.sleep(1)
     
    stop_click(MarketDD_seq,MarketDD)
    stop_check(MarketDD_seq,MarketDD)
 
 
 
def stop_Service_Live():
     
    global browser
    browser= webdriver.Remote(
                command_executor="http://"+ seleniumServer +":4444/wd/hub",
                desired_capabilities={'browserName': 'chrome',
                                             'version': '2',
                                             'javascriptEnabled': True})                                    
 
    ####open website          
    try:
         
        browser.get('http://'+username+':'+password+'@'+ monitorServer+'/monitoring/DaemonLobby.aspx')
        #browser.maximize_window()
         
        print(browser.title+'\n')
        browser.implicitly_wait(60)
    except:
        print "Open Website Error."
        #htmlunit
 
    ####ways to locate element, example below
    ####browser.find_element_by_xpath('//*[@id="rowContents"]/tr[1]/td[4]/button[2]').click()
    ####browser.find_element_by_css_selector('#rowContents > tr:nth-child(1) > td.serviceCell > button.serviceButton.cooldown').click()
    time.sleep(5)
 
     
    browser.find_element_by_link_text('Lobby').click()
    browser.implicitly_wait(10)
 
    if FlagForceMode==True:
        browser.find_element_by_xpath('//*[@id="forceCheckBox"]').click()
 
    cooldown_and_stop_mult(LoGateD_list,LoGateD_list_len)
    cooldown_and_stop_mult(InGateD_list,InGateD_list_len)
     
    browser.find_element_by_link_text('Arena').click()
    browser.implicitly_wait(10)
    if FlagForceMode==True:
        browser.find_element_by_xpath('//*[@id="forceCheckBox"]').click()
    cooldown_and_stop_mult(ArenaD_list,ArenaD_list_len)
    cooldown_and_stop_mult(Dungeon_list,Dungeon_list_len)
     
 
    browser.find_element_by_link_text('Game').click()
    browser.implicitly_wait(10)
    if FlagForceMode==True:
        browser.find_element_by_xpath('//*[@id="forceCheckBox"]').click()
 
    cooldown_and_stop_mult(WorldD_list,WorldD_list_len)
     
    browser.find_element_by_link_text('Economy').click()
    browser.implicitly_wait(10)
    if FlagForceMode==True:
        browser.find_element_by_xpath('//*[@id="forceCheckBox"]').click()
     
    cooldown_and_stop(DuelBot_seq,DuelBot)
   # print DuelBot
   # print (browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(DuelBot_seq)+']/td[1]')).text
 
    cooldown_and_stop(Achieve_seq,Achieve)
   # print Achieve
   # print (browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(Achieve_seq)+']/td[1]')).text
 
    browser.find_element_by_link_text('Arena').click()
    browser.implicitly_wait(10)
    if FlagForceMode==True:
        browser.find_element_by_xpath('//*[@id="forceCheckBox"]').click()
 
    cooldown_and_stop(ArenaLobby_seq,ArenaLobby)
   # print ArenaLobby
   # print (browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(ArenaLobby_seq)+']/td[1]')).text
 
    browser.find_element_by_link_text('Economy').click()
    browser.implicitly_wait(10)
    if FlagForceMode==True:
        browser.find_element_by_xpath('//*[@id="forceCheckBox"]').click()
 
    cooldown_and_stop_dealer()
 
 
    cooldown_and_stop(MarkRA_seq,MarkRA)
   # print MarkRA
   # print (browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(MarkRA_seq)+']/td[1]')).text
 
    cooldown_and_stop(MarketRD_seq,MarketRD)
   # print MarketRD
   # print (browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(MarketRD_seq)+']/td[1]')).text
    
   ####Craft not use any more####
   # cooldown_and_stop(CraftD_seq,CraftD)
   # print CraftD
   # print (browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(CraftD_seq)+']/td[1]')).text
 
    browser.find_element_by_link_text('Lobby').click()
    browser.implicitly_wait(10)
    if FlagForceMode==True:
        browser.find_element_by_xpath('//*[@id="forceCheckBox"]').click()
 
    cooldown_and_stop(LobbyD_seq,LobbyD)
   # print LobbyD
   # print (browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(LobbyD_seq)+']/td[1]')).text
     
    browser.find_element_by_link_text('Economy').click()
    browser.implicitly_wait(10)
    if FlagForceMode==True:
        browser.find_element_by_xpath('//*[@id="forceCheckBox"]').click()
 
    cooldown_and_stop(PostOffD_seq,PostOffD)
   # print PostOffD
   # print (browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(PostOffD_seq)+']/td[1]')).text
 
    cooldown_and_stop(CacheGate_seq,CacheGate)
   # print CacheGate
   # print (browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(CacheGate_seq)+']/td[1]')).text
 
    browser.find_element_by_link_text('Cache').click()
    browser.implicitly_wait(10)
    if FlagForceMode==True:
        browser.find_element_by_xpath('//*[@id="forceCheckBox"]').click()
 
     
    cooldown_and_stop_mult(WorldDB_list,WorldDB_list_len)
 
  
    browser.find_element_by_link_text('Economy').click()
    browser.implicitly_wait(10)
    if FlagForceMode==True:
        browser.find_element_by_xpath('//*[@id="forceCheckBox"]').click()
 
    cooldown_and_stop(AccountIn_seq,AccountIn)
    #print AccountIn
    #print (browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(AccountIn_seq)+']/td[1]')).text
 
    cooldown_and_stop(Rank_seq,Rank)
   # print Rank
   # print (browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(Rank_seq)+']/td[1]')).text
 
    print "stop all services done."
    kill_process("chromedriver.exe")
    kill_process("java.exe")
 
stop_Service_Live()
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="start\_Service\_LIVE.py" %}
```python
#!/bin/python
# -*- coding: utf-8 -*-
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
import time
import sys
import subprocess
import base64
 
 
FlagForceMode=False
monitorServer='10.xx.xx.xx'
seleniumServer='10.xx.xx.xx'
 
 
#kill chromedriver process
def kill_process(myprocess):
    subprocess.call(["salt","AdminWeb","cmd.exec_code","python", \
                     "import psutil ; PROCNAME = '"+ myprocess +"' ; "+ \
                     "[proc.kill() for proc in psutil.process_iter() if proc.name() == PROCNAME]"])
 
 
#kill_process("chrome.exe")
kill_process("chromedriver.exe")
 
 
 
users=['user1','user2','user3','user4','user5','user6']
 
#get input username and password
def decode(key, enc):
    dec = []
    enc = base64.urlsafe_b64decode(enc)
    for i in range(len(enc)):
        key_c = key[i % len(key)]
        dec_c = chr((256 + ord(enc[i]) - ord(key_c)) % 256)
        dec.append(dec_c)
    return "".join(dec)
 
 
if len(sys.argv)==4 or len(sys.argv)==5 :
    try:
        username=decode("decodekey", str(sys.argv[1]))
        password=decode("decodekey", str(sys.argv[2]))
        user=sys.argv[3]
        if (len(sys.argv)==5 and (sys.argv[4]=="--Force" or sys.argv[4]=="--force" or  sys.argv[4]=="--FORCE")):
            FlagForceMode=True
    except:
        print "username or password input Error"
        quit()
else:
    print "Please check arguments.Usage:python script.py [username] [password] [your_name]."
    quit()
 
def check_user():
    for i in users:
        if i==user:
            return
    print "You are not a trusted user."
    quit()
check_user()
 
#Lobby
InGateD01_seq=1
InGateD02_seq=2
LobbyD_seq=3
LoGateD01_seq=4
LoGateD02_seq=5
InGateD01='InGateD01'
InGateD02='InGateD02'
InGateD_list=[[str(InGateD01_seq),InGateD01],\
                    [str(InGateD02_seq),InGateD02]]
InGateD_list_len=len(InGateD_list)
LobbyD='LobbyD'
 
LoGateD01='LoGateD01'
LoGateD02='LoGateD02'
LoGateD_list=[[str(LoGateD01_seq),LoGateD01],\
                    [str(LoGateD02_seq),LoGateD02]]
LoGateD_list_len=len(LoGateD_list)
 
 
 
#Cache
WorldDB01_seq=1
WorldDB03_seq=2
WorldDB04_seq=3
 
 
WorldDB01='WorldDB01'
WorldDB03='WorldDB03'
WorldDB04='WorldDB04'
 
 
WorldDB_list=[[str(WorldDB01_seq),WorldDB01], \
                    [str(WorldDB03_seq),WorldDB03], \
                    [str(WorldDB04_seq),WorldDB04]]
 
WorldDB_list_len=len(WorldDB_list)
 
#Game
WorldD01_seq=1
WorldD03_seq=2
WorldD04_seq=3
 
 
WorldD01='WorldD01'
WorldD03='WorldD03'
WorldD04='WorldD04'
 
WorldD_list=[ [str(WorldD01_seq),WorldD01], \
                    [str(WorldD03_seq),WorldD03], \
                    [str(WorldD04_seq),WorldD04]]
 
WorldD_list_len=len(WorldD_list)
 
#Arena
ArenaLobby_seq=1
ArenaD01_seq=2
ArenaD02_seq=3
Dungeon01_seq=4
Dungeon02_seq=5
ArenaLobby='ArenaLobby'
ArenaD01='ArenaD01'
ArenaD02='ArenaD02'
ArenaD_list=[[str(ArenaD01_seq),ArenaD01],\
                   [str(ArenaD02_seq),ArenaD02]]
ArenaD_list_len=len(ArenaD_list)
 
Dungeon01='Dungeon01'
Dungeon02='Dungeon02'
Dungeon_list=[[str(Dungeon01_seq),Dungeon01],\
                    [str(Dungeon02_seq),Dungeon02]]
Dungeon_list_len=len(Dungeon_list)
 
 
#Economy
AccountIn_seq=1
Achieve_seq=2
CacheGate_seq=3
#CraftD_seq=4
MarkDA_seq=4
MarketDD_seq=5
MarkRA_seq=6
MarketRD_seq=7
PostOffD_seq=8
Rank_seq=9
DuelBot_seq=10
AccountIn='AccountIn'
Achieve='Achieve'
CacheGate='CacheGate'
#CraftD='CraftD'
MarkDA='MarkDARA'
MarketDD='MarketDD'
MarkRA='MarkDARA'
MarketRD='MarketRD'
PostOffD='PostOffD'
Rank='Rank'
DuelBot='DuelBot'
 
 
 
def start_click(seq,name):
    state="NOT STOPPED"
    state_orin=state
     
    while True:
        if state=="STOPPED" :
            print "Retryed"
        if state=="RUNNING":
            return
        try:
            state=(browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(seq)+']/td[5]')).text
            element_name=(browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(seq)+']/td[1]')).text
            print element_name
            if element_name==name:
                elem_button=browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+ str(seq) +']/td[4]/button')
                elem_button.click()  #click start
 
                 
      
        except:
            print name+" start failed\n retrying..."
            time.sleep(1)
            continue
        break
    alert = browser.switch_to.alert
    print alert.text+'\n'
    #alert.dismiss()
    alert.accept()
    time.sleep(1)
    alert = browser.switch_to.alert
    alert.accept()
    if FlagForceMode==True:
        time.sleep(1)
        alert = browser.switch_to.alert
        alert.accept()
 
    
def start_check(seq,name):
    #state=(browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(seq)+']/td[5]')).text
    #print name+ ": "+state
    state="NOT RUNNING"
    state_orin=state
     
    while state!="RUNNING":
        time.sleep(1)
        try:
            state=(browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(seq)+']/td[5]')).text
            print name+ ": "+state
        except:
            state=state_orin
            #print name+ ": "+state
     
    print name+ ": "+state
 
def start(seq,name):
    start_click(seq,name)
    start_check(seq,name)
 
def start_mult(list_name,length):
    for i in range(0,length):
        start_click(list_name[i][0],list_name[i][1])
    for i in range(0,length):
        start_check(list_name[i][0],list_name[i][1])
 
def start_Service_Live():
    
    global browser
    browser= webdriver.Remote(
                command_executor="http://"+ seleniumServer +":4444/wd/hub",
                desired_capabilities={'browserName': 'chrome',
                                             'version': '2',
                                             'javascriptEnabled': True})                                    
 
    ####open website          
    try:
         
        browser.get('http://'+username+':'+password+'@'+ monitorServer+'/monitoring/Economy.aspx')
        #browser.maximize_window()
         
        print(browser.title+'\n')
        browser.implicitly_wait(60)
    except:
        print "Open Website Error."
        #htmlunit
 
    ####ways to locate element, example below
    ####browser.find_element_by_xpath('//*[@id="rowContents"]/tr[1]/td[4]/button[2]').click()
    ####browser.find_element_by_css_selector('#rowContents > tr:nth-child(1) > td.serviceCell > button.serviceButton.cooldown').click()
  
     
    browser.find_element_by_link_text('Economy').click()
    browser.implicitly_wait(10)
    if FlagForceMode==True:
        browser.find_element_by_xpath('//*[@id="forceCheckBox"]').click()
 
    start(Rank_seq,Rank)
    #print Rank
    #print (browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(Rank_seq)+']/td[1]')).text#
 
    start(AccountIn_seq,AccountIn)
    #print AccountIn
    #print (browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(AccountIn_seq)+']/td[1]')).text
 
    browser.find_element_by_link_text('Cache').click()
    browser.implicitly_wait(10)
    if FlagForceMode==True:
        browser.find_element_by_xpath('//*[@id="forceCheckBox"]').click()
 
    start_mult(WorldDB_list,WorldDB_list_len)
    #for i in range(0,WorldDB_list_len):
    #    seq=WorldDB_list[i][0]
    #    hostname=(browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(seq)+']/td[1]')).text
    #    cooldown_and_stop(seq,hostname)
        #print WorldDB_list[i][1]
        #print hostname
         
    browser.find_element_by_link_text('Economy').click()
    browser.implicitly_wait(10)
    if FlagForceMode==True:
        browser.find_element_by_xpath('//*[@id="forceCheckBox"]').click()
 
    start(CacheGate_seq,CacheGate)
    #print CacheGate
    #print (browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(CacheGate_seq)+']/td[1]')).text
     
    start(PostOffD_seq,PostOffD)
    #print PostOffD
    #print (browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(PostOffD_seq)+']/td[1]')).text
 
    browser.find_element_by_link_text('Lobby').click()
    browser.implicitly_wait(10)
    if FlagForceMode==True:
        browser.find_element_by_xpath('//*[@id="forceCheckBox"]').click()
 
    start(LobbyD_seq,LobbyD)
    #print LobbyD
    #print (browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(LobbyD_seq)+']/td[1]')).text
     
    browser.find_element_by_link_text('Economy').click()
    browser.implicitly_wait(10)
    if FlagForceMode==True:
        browser.find_element_by_xpath('//*[@id="forceCheckBox"]').click()
     
    ####Craft not use anymore####
    #start(CraftD_seq,CraftD)
    #print CraftD
    #print (browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(CraftD_seq)+']/td[1]')).text   
 
    start(MarketRD_seq,MarketRD)
    #print MarketRD
    #print (browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(MarketRD_seq)+']/td[1]')).text
 
    start(MarkRA_seq,MarkRA)
    #print MarkRA
    #print (browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(MarkRA_seq)+']/td[1]')).text
  
    start(MarketDD_seq,MarketDD)
    #print MarketDD
    #print (browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(MarketDD_seq)+']/td[1]')).text
 
    start(MarkDA_seq,MarkDA)
    #print MarkDA
    #print (browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(MarkDA_seq)+']/td[1]')).text   
 
    browser.find_element_by_link_text('Arena').click()
    browser.implicitly_wait(10)
    if FlagForceMode==True:
        browser.find_element_by_xpath('//*[@id="forceCheckBox"]').click()
 
    start(ArenaLobby_seq,ArenaLobby)
    #print ArenaLobby
    #print (browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(ArenaLobby_seq)+']/td[1]')).text
 
    browser.find_element_by_link_text('Economy').click()
    browser.implicitly_wait(10)
    if FlagForceMode==True:
        browser.find_element_by_xpath('//*[@id="forceCheckBox"]').click()
 
    start(Achieve_seq,Achieve)
    #print Achieve
    #print (browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(Achieve_seq)+']/td[1]')).text
     
    start(DuelBot_seq,DuelBot)
    #print DuelBot
    #print (browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(DuelBot_seq)+']/td[1]')).text
 
    browser.find_element_by_link_text('Game').click()
    browser.implicitly_wait(10)
    if FlagForceMode==True:
        browser.find_element_by_xpath('//*[@id="forceCheckBox"]').click()
     
    start_mult(WorldD_list,WorldD_list_len)
    #for i in range(0,WorldD_list_len):
    #    seq=WorldD_list[i][0]
    #    hostname=(browser.find_element_by_xpath('//*[@id="rowContents"]/tr['+str(seq)+']/td[1]')).text
            #cooldown_and_stop(seq,hostname)
        #print WorldD_list[i][1]
        #print hostname
 
    browser.find_element_by_link_text('Arena').click()
    browser.implicitly_wait(10)
    if FlagForceMode==True:
        browser.find_element_by_xpath('//*[@id="forceCheckBox"]').click()
 
    start_mult(Dungeon_list,Dungeon_list_len)
    start_mult(ArenaD_list,ArenaD_list_len)   
 
 
    browser.find_element_by_link_text('Lobby').click()
    browser.implicitly_wait(10)
    if FlagForceMode==True:
        browser.find_element_by_xpath('//*[@id="forceCheckBox"]').click()
     
    start_mult(InGateD_list,InGateD_list_len)
    start_mult(LoGateD_list,LoGateD_list_len)
 
    print "start all services done."
    kill_process("chromedriver.exe")
    kill_process("java.exe")
 
start_Service_Live()
```
{% endcode-tabs-item %}
{% endcode-tabs %}

