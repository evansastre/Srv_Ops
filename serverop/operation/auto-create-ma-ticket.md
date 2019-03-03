# auto create MA ticket

```text
from selenium import webdriver
from selenium.webdriver.support.ui import Select
import time
import re

introduction = '''Please input 3numbers: \n
1-TH     1-DEV     0-WindowsUpdate-No
2-VN     2-STG     1-WindowsUpdate-Yes
         3-LIVE    
_____    ______    ___________________\n'''

#This parameters need to be updated everytime:
#-------------------------------------------------------------------
parameter = 121
email = ' Halloween V2 Build Deployment'
content = '''\
[Server]
• HalloweenEvent_Server_ver(1.2.70.490)_rel(0913).rar.pgp
[Client]
• HalloweenEvent_Client_ver(1.2.70.490)_rel(0913).rar.pgp
'''
windowsupdatelist='''\
   KB4099633 
   8e951203-5d8e-4f69-9560-ce698c4f7a77 
   KB4099637 
   724b7684-e4d6-47a6-b9b6-c0e7d1382b6b 
   KB4284826 
   999fa80e-c59d-4ff6-8268-c6a8c365f428'''
#-------------------------------------------------------------------
#input your jira username and password here:
user = ""
password = ""


c = content.split('\n')
server_patch, client_patch = c[1], c[3]

pattern_build = re.compile(r"(.+)_Server")
build = pattern_build.findall(server_patch)[0]

pattern_version = re.compile(r"\s([vV]\d)")
version = pattern_version.findall(email)[0]

p = []
for i in str(parameter):
    p.append(i)
if p[0] == '1':
    game_region = 'TH'
elif p[0] == '2':
    game_region = 'VN'
else:
    game_region = 'SEA'
if p[1] == '1':
    server = 'DEV'
elif p[1] == '2':
    server = 'STG'
elif p[1] == '3':
    server = 'LIVE'
else:
    server = 'ALL'
windowsupdate = int(p[2])

if game_region == 'TH':
    gto_person = 'ABC'
    qa_person = 'EFG'
    region_id = '10011'
    change_requestor = 'K'
    approve_person = 'B'
elif game_region == 'VN':
    gto_person = 'LL'
    qa_person = 'Hu'
    region_id = '10013'
    change_requestor = 'K'
    approve_person = 'M'
else:
    pass

today = time.strftime("%w", time.localtime(time.time()))
if server == 'LIVE':
    if game_region == 'TH':
        if int(today) <= 3:
            time_diff = 3 - int(today)
        else:
            time_diff = 10 - int(today)
        date = time.strftime("%d %b %Y", time.localtime(time.time() + time_diff * 24 * 60 * 60))
        start_time = time.strftime("%d/%b/%y 6:00 AM", time.localtime(time.time() + time_diff * 24 * 60 * 60))
        end_time = time.strftime("%d/%b/%y 11:00 AM", time.localtime(time.time() + time_diff * 24 * 60 * 60))
    elif game_region == 'VN':
        if int(today) <= 2:
            time_diff = 2 - int(today)
        else:
            time_diff = 9 - int(today)
        date = time.strftime("%d %b %Y", time.localtime(time.time() + time_diff * 24 * 60 * 60))
        start_time = time.strftime("%d/%b/%y 6:00 AM", time.localtime(time.time() + time_diff * 24 * 60 * 60))
        end_time = time.strftime("%d/%b/%y 11:00 AM", time.localtime(time.time() + time_diff * 24 * 60 * 60))
else:
    date = time.strftime("%d %b %Y", time.localtime(time.time()))
    start_time = time.strftime("%d/%b/%y %H:%M %p", time.localtime(time.time() + 60 * 60))
    end_time = time.strftime("%d/%b/%y %H:%M %p", time.localtime(time.time() + 2 * 60 * 60))

if (not windowsupdate) or (windowsupdate and server == 'LIVE'):
    ticket_tittle = 'BNS | ' + game_region + ' | ' + date + ' | ' + server + ' ' + build + ' Build Server/Client patch Release (' + version + ')'
    rollback_plan = 'rollback to previous FA build'
    if windowsupdate:
        description = '*+Email:+*\n' + email + '\n*+File Lists:+*\n' + content + '\nInstall following Windows Updates:\n' + windowsupdatelist
    else:
        description = '*+Email:+*\n' + email + '\n*+File Lists:+*\n' + content
else:
    ticket_tittle = 'BNS | ' + game_region + ' | ' + date + ' | ' + server + ' ' + 'WindowsUpdate'
    description = 'Install following Windows Updates:\n' + windowsupdatelist
    rollback_plan = 'Recover use most recent windows backup.'

change_plan_list = []
change_plan_list.append('Stop Service -- ' + gto_person)
change_plan_list.append('Backup Service -- ' + gto_person)
if (not windowsupdate) or (windowsupdate and server == 'LIVE'):
    change_plan_list.append('Apply Server Patch -- ' + gto_person + '\n  ' + server_patch)
if windowsupdate:
    change_plan_list.append('Windows Backup -- ' + gto_person + "\n   salt '*' cmd.run 'wbadmin start systemstatebackup -backuptarget:Z: -quiet'")
    change_plan_list.append("Install windows updates:\n   salt '*' win_wua.list_updates\n   salt '*' win_wua.install_updates guid=[]\n" + windowsupdatelist)
    change_plan_list.append('Server Reboot -- ' + gto_person)
change_plan_list.append('Start Service -- ' + gto_person)
if (not windowsupdate) or (windowsupdate and server == 'LIVE'):
    change_plan_list.append('Apply Client Build -- ' + qa_person + '\n   ' + client_patch)
change_plan_list.append('In game Test -- ' + qa_person)

change_plan = ''
i = 1
for todolist in change_plan_list:
    change_plan = change_plan + str(i) + '. ' + todolist + '\n'
    i += 1


if server == 'DEV':
    test_plan = 'This process has been tested by NC before without issue'
else:
    test_plan = 'This process has been tested on Dev servers before without issue'
change_result_detail = 'All good.'


browser = webdriver.Chrome('/Users/zhoukl/Documents/chromedriver')
browser.get('http://gtojira.garenanow.com:8100/')

browser.find_element_by_id("login-form-username").send_keys(user)
time.sleep(0.1)

browser.find_element_by_id("login-form-password").send_keys(password)
browser.find_element_by_name("login").click()
time.sleep(0.5)


create_button = browser.find_element_by_id("create_link")
create_button.click()
time.sleep(0.5)


browser.find_element_by_id('priority-field').click()
browser.find_element_by_id('priority-field').clear()
browser.find_element_by_id('priority-field').send_keys('P4')


browser.find_element_by_xpath('//*[@id="summary"]').send_keys(ticket_tittle)

region = Select(browser.find_element_by_xpath('//*[@id="customfield_10021"]'))
region.deselect_by_value('-1')
region.select_by_value(region_id)

game = Select(browser.find_element_by_xpath('//*[@id="customfield_10030"]'))
game.select_by_value('10664')

risk = Select(browser.find_element_by_xpath('//*[@id="customfield_10037"]'))
risk.select_by_value('10069')

impact = Select(browser.find_element_by_xpath('//*[@id="customfield_10038"]'))
impact.select_by_value('10072')

browser.find_element_by_xpath('//*[@id="customfield_10501"]').send_keys(change_plan)
browser.find_element_by_xpath('//*[@id="customfield_10502"]').send_keys(rollback_plan)
browser.find_element_by_xpath('//*[@id="customfield_10500"]').send_keys(version)
browser.find_element_by_xpath('//*[@id="customfield_10503"]').send_keys(test_plan)

test_result = Select(browser.find_element_by_xpath('//*[@id="customfield_10504"]'))
test_result.select_by_value('10700')

browser.find_element_by_xpath('//*[@id="customfield_10201"]').send_keys(start_time)
browser.find_element_by_xpath('//*[@id="customfield_10200"]').send_keys(end_time)
browser.find_element_by_xpath('//*[@id="customfield_10040"]').click()
browser.find_element_by_xpath('//*[@id="customfield_10040"]').send_keys(change_requestor)
browser.find_element_by_xpath('//*[@id="reporter-field"]').click()
browser.find_element_by_xpath('//*[@id="reporter-field"]').clear()
browser.find_element_by_xpath('//*[@id="reporter-field"]').send_keys(gto_person)
browser.find_element_by_xpath('//*[@id="customfield_10039"]').click()
browser.find_element_by_xpath('//*[@id="customfield_10039"]').send_keys(approve_person)
browser.find_element_by_xpath('//*[@id="assignee-field"]').click()
browser.find_element_by_xpath('//*[@id="assignee-field"]').clear()
browser.find_element_by_xpath('//*[@id="assignee-field"]').send_keys(gto_person)

change_result = Select(browser.find_element_by_xpath('//*[@id="customfield_10601"]'))
change_result.select_by_value('10803')

#browser.find_element_by_xpath('//*[@id="assign-to-me-trigger"]').click()
browser.find_element_by_xpath('//*[@id="customfield_10407"]').send_keys(server + ' servers')
browser.find_element_by_xpath('//*[@id="description"]').send_keys(description)
browser.find_element_by_xpath('//*[@id="customfield_10602"]').send_keys(change_result_detail)

# time.sleep(10)
#browser.find_element_by_xpath('//*[@id="create-issue-submit"]').click()
#browser.close()
```

