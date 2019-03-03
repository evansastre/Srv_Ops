# Firewall monitor

{% code-tabs %}
{% code-tabs-item title="FirewallAnalysis.py" %}
```text

#!/usr/bin/python
# -*- coding: UTF-8 -*-

import sys
from dictdiffer import diff

firewall_compare_before = str(sys.argv[1])
firewall_compare_after = str(sys.argv[2])
firewall_new = str(sys.argv[3])
game = str(sys.argv[4])
first = str(sys.argv[5])

def generate_dic(filepath, compare_path_before, compare_path_after):
    try:
        with open(filepath, 'r') as f:
            firewall_lib = {}
            rule_list ={}
            rule_content = {}
            list_missing = []
            line = f.readline().rstrip('\n')
            while line:
                if game in line:
                    server_current = line
                    line = f.readline().rstrip('\n')
                    continue
                if 'command not found' in line:
                    firewall_lib[server_current] = {'Error':{'Message':'This server is not Windows server.'}}
                    line = f.readline().rstrip('\n')
                    continue
                if 'Not connected' in line:
                    print 'Server', server_current, 'Salt Not Connected, please check the salt-minion service.'
                    list_missing.append(server_current)
                    firewall_lib[server_current] = {'Error':{'Message':'Salt Not Connected, please check the salt-minion service.'}}
                    line = f.readline().rstrip('\n')
                    continue
                if 'No response' in line:
                    print 'Server', server_current, 'Salt minion no response, please check again.'
                    list_missing.append(server_current)
                    firewall_lib[server_current] = {'Error':{'Message':'Salt minion no response, please check again.'}}
                    line = f.readline().rstrip('\n')
                    continue
                element_pair = line.split(":")
                if 'Rule Name' in element_pair[0]:
                    rule_current = element_pair[1]
                if 'Type' in element_pair[0] and 'Code' in element_pair[1]:
                    temp = element_pair[:]
                    line = f.readline().rstrip('\n')
                    element_pair = line.split(":")
                    rule_content[temp[0]] = element_pair[0]
                    rule_content[temp[1]] = element_pair[1]
                    line = f.readline().rstrip('\n')
                    continue
                try:
                    rule_content[element_pair[0]] = element_pair[1]
                    line = f.readline().rstrip('\n')
                except IndexError:
                    print 'The firewall file is empty, please check and try again'
                    sys.exit()
                if 'Rule Name' in line:
                    rule_content_copy = rule_content.copy()
                    rule_current = rule_current + '-' + rule_content_copy['Direction']
                    rule_list[rule_current] = rule_content_copy
                    rule_content.clear()
                if game in line or not line:
                    rule_content_copy = rule_content.copy()
                    rule_current = rule_current + '-' + rule_content_copy['Direction']
                    rule_list[rule_current] = rule_content_copy
                    rule_content.clear()
                    rule_list_copy = rule_list.copy()
                    firewall_lib[server_current] = rule_list_copy
                    rule_list.clear()
    except IOError:
        print "Read firewall original file filewall_standard_new error"
        sys.exit()
    try:
        firewall_lib_copy = firewall_lib.copy()
        if not first == '1':
            with open(compare_path_after, 'r') as car:
                last_firewall = car.readline()
                last_firewall_lib = eval(last_firewall)
            if len(list_missing):
                for missing_server in list_missing:
                    missing_rule_copy = last_firewall_lib[missing_server].copy()
                    firewall_lib_copy[missing_server].update(missing_rule_copy)
            with open(compare_path_before, 'w+') as cbw:
                cbw.write(str(last_firewall_lib))
        with open(compare_path_after, 'w+') as caw:
            caw.write(str(firewall_lib_copy))
    except IOError:
        print "Write firewall comparing file firewall_compare_before/after error"
        sys.exit()
    return firewall_lib


def compare_firewall_change(compare_path_before, compare_path_after):
    try:
        with open(compare_path_before, 'r') as cb:
            line_before = cb.readline()
            dict_before = eval(line_before)
        with open(compare_path_after, 'r') as ca:
            line_after = ca.readline()
            dict_after = eval(line_after)
    except IOError:
        print "Read firewall comparing file firewall_compare_before/after error"
        sys.exit()
    difference = diff(dict_before, dict_after)
    change_server = []
    change_type = []
    change_rule = []
    change_element = []
    change_content = []
    change_repeat = []
    repeat_rule = {}
    repeat_element = {}
    repeat_content = {}
    times = 0
    count = 0
    for ops in difference:
        change_type.append(ops[0])
        element_pair = ops[1].split('.')
        change_server.append(element_pair[0])
        if not ops[2][0][0] == 'Error':
            count += 1
        if len(element_pair) == 1:
            change_rule.append('')
            change_element.append('')
        if len(element_pair) == 2:
            change_rule.append(element_pair[1])
            change_element.append('')
        if len(element_pair) == 3:
            change_rule.append(element_pair[1])
            change_element.append(element_pair[2])
            change_repeat.append(element_pair[0] + '.' + element_pair[1])
        change_content.append(ops[2])
    if count > 0:
        print 'There are total', count, 'operations.'
    for changes in change_repeat:
        if change_repeat.count(changes) > 1:
            repeat_rule[changes] = change_repeat.count(changes)
    for i in range(len(change_content)):
        if change_server[i] == '':
            if change_type[i] == 'add':
                for k in range(len(change_content[i])):
                    print 'New server was added : ', change_content[i][k][0]
                    for key, value in dict_after[change_content[i][k][0]].items():
                        print '    ', key, ':', value
            elif change_type[i] == 'remove':
                print change_content[i]
                for k in range(len(change_content[i])):
                    print 'Old server was removed : ', change_content[i][k][0]
                    for key, value in dict_before[change_content[i][k][0]].items():
                        print '    ', key, ':', value
            else:
                print 'No add/remove on server'
        elif change_rule[i] == '':
             if change_type[i] == 'add':
                 for k in range(len(change_content[i])):
                     if change_content[i][k][0] == 'Error':
                         pass
                     else:
                        print 'Server', change_server[i], 'executed a', change_type[i], 'operation on rule', change_content[i][k][0], ': ALL'
                        print 'New rule is:'
                        for key, value in change_content[i][k][1].items():
                            print '    ', key, ':', value
             elif change_type[i] == 'remove':
                 for k in range(len(change_content[i])):
                     if change_content[i][k][0] == 'Error':
                         pass
                     else:
                        print 'Server', change_server[i], 'executed a', change_type[i], 'operation on rule', change_content[i][k][0], ': ALL'
                        print 'Previous rule is:'
                        for key, value in change_content[i][k][1].items():
                            print '    ', key, ':', value
             else:
                 print 'No add/remove on rule'
        elif change_type[i] == 'add':
            element_add = []
            print 'Server', change_server[i], 'executed a', change_type[i], 'operation on rule', change_rule[i], ':'
            for k in range(len(change_content[i])):
                element_add.append(change_content[i][k][0])
                print '     Added element: (', change_content[i][k][0], ':', change_content[i][k][1], ')'
            print 'New rule is:'
            for key, value in dict_after[change_server[i]][change_rule[i]].items():
                if key in element_add:
                    print'    (', key, ':', value, ')'
                    continue
                print '    ', key, ':', value
        elif change_type[i] == 'remove':
            element_remove = []
            print 'Server', change_server[i], 'executed a', change_type[i], 'operation on rule', change_rule[i], ':'
            for k in range(len(change_content[i])):
                element_remove.append(change_content[i][k][0])
                print '     Removed element: (', change_content[i][k][0], ':', change_content[i][k][1], ')'
            print 'Previous rule is:'
            for key, value in dict_before[change_server[i]][change_rule[i]].items():
                if key in element_remove:
                    print '    (', key, ':', value, ')'
                    continue
                print '    ', key, ':', value
        elif change_type[i] == 'change':
            repeat_key = change_server[i] + '.' + change_rule[i]
            if repeat_key in repeat_rule.keys():
                repeat_times = repeat_rule[repeat_key]
                repeat_content[change_element[i]] = change_content[i]
                times += 1
                if times >= repeat_times:
                    repeat_content_copy = repeat_content.copy()
                    repeat_element[change_rule[i]] = repeat_content_copy
                    repeat_content.clear()
                    print 'Server', change_server[i], 'executed', times, change_type[i], 'operations on rule', change_rule[i]
                    print 'Changed rule is：'
                    for key, value in dict_before[change_server[i]][change_rule[i]].items():
                        if key in repeat_element[change_rule[i]].keys():
                            print '    (', key, ':', repeat_element[change_rule[i]][key][0] + ' -> ' + repeat_element[change_rule[i]][key][1],  ')'
                            continue
                        print '    ', key, ':', value
                    times = 0
            else:
                print 'Server', change_server[i], 'executed a', change_type[i], 'operation on rule', change_rule[i], ':', change_element[i], 'From "', change_content[i][0], '" to "', change_content[i][1], '"'
                print 'Changed rule is：'
                for key, value in dict_before[change_server[i]][change_rule[i]].items():
                    if key == change_element[i]:
                        print '    (', key, ':', value + ' -> ' + change_content[i][1], ')'
                        continue
                    print '    ', key, ':', value
        else:
            print 'No change/add/remove detected.'
    return

def print_firewall_list(firewall_lib, arrangement):
    if arrangement == 'a-l':
        for server, rulelist in firewall_lib.items():
            print '\n' + server + '\n'
            for rule, content in rulelist.items():
                print rule + '\n'
                for element, value in content.items():
                    print element, ':', value
                print '\n'
    elif arrangement == 'a-r':
        for server, rulelist in firewall_lib.items():
            print '\n' + server + '\n'
            for rule, content in rulelist.items():
                print content
    elif arrangement == 'e-l':
        for server, rulelist in firewall_lib.items():
            print server + '\n'
            for rule, content in rulelist.items():
                if 'Enabled' in content:
                    enable = content['Enabled']
                    if enable == 'Yes':
                        for element, value in content.items():
                            print element, ':', value
                        print '\n'
                else:
                    print 'not applicable', '\n'
    elif arrangement == 'e-r':
        for server, rulelist in firewall_lib.items():
            print server + '\n'
            for rule, content in rulelist.items() :
                if 'Enabled' in content:
                    enable = content['Enabled']
                    if enable == 'Yes':
                        print content
                else:
                    print 'not applicable', '\n'
    elif arrangement == 'c':
        server_number = 0
        for server in firewall_lib.keys():
            print server
            server_number += 1
        print 'Total', server_number, 'servers.'
    else:
        print 'Wrong argument! Please use it as:\nprint_firewall_list(firewall_lib, e-r,e-l,a-r,a-l,c)'

lib_new = generate_dic(firewall_new, firewall_compare_before, firewall_compare_after)

if not first == '1':
    compare_firewall_change(firewall_compare_before, firewall_compare_after)

#print_firewall_list(lib_new, 'e-r')
```
{% endcode-tabs-item %}
{% endcode-tabs %}



{% code-tabs %}
{% code-tabs-item title="CheckFirewall.sh" %}
```text
#!/bin/bash
#define

#Define Game and Region
game="GameN1"

#Set Alert Receiver
Sender=$(hostname)"<saltmaster@GameN1.com>"
Receiver="user1@gameN1.com"

#Set file/log path
log_path='/var/log/firewall_monitoring/'
result_path='/var/log/firewall_monitoring/change_result/'
compare_path='/var/log/firewall_monitoring/compare/'
date=$(date "+%Y-%m-%d_%H:%M:%S")
firewall_all='firewall_all_'$date'.txt'
firewall_standard='firewall_standard_'$date'.txt'
firewall_compare_before=$compare_path'firewall_compare_before.txt'
firewall_compare_after=$compare_path'firewall_compare_after.txt'
change_result=$log_path'change_result/change_result_'$date'.txt'

#Check Log Path/File
if [[ ! -d $log_path ]];then
    mkdir -p $log_path
fi
if [[ ! -d $result_path ]];then
    mkdir -p $result_path
fi
if [[ ! -d $compare_path ]];then
    mkdir -p $compare_path
fi
if [[ ! -f $firewall_compare_before ]];then
    touch $firewall_compare_before
fi
if [[ -f $firewall_compare_after ]];then
    touch $firewall_compare_after
fi


#Check if it is the first time you run this script
if [[ ! -s $firewall_compare_after ]];then
    first=1
    echo 'This is the first time you run this script. You need run it twice to start check firewall change.'
else
    first=0
fi

#Clear Old Log
#Set Maximum logs amount to be stored
reserved_log=200

if [[ $first == 0 ]]; then
    log_all=$(ls $log_path'firewall_all'* | wc -l)
    log_standard=$(ls $log_path'firewall_standard'* | wc -l)
    log_result=$(ls $result_path'change_result'* | wc -l)
    delete_all=$[$log_all-$reserved_log]
    delete_standard=$[$log_standard-$reserved_log]
    delete_result=$[$log_result-$reserved_log]
    if [ $log_all -gt $reserved_log ];then
        delete_log=$(ls -tr $log_path'firewall_all'* | head -$delete_all)
        rm -rf $delete_log
    fi
    if [ $log_standard -gt $reserved_log ];then
        delete_log=$(ls -tr $log_path'firewall_standard'* | head -$delete_standard)
        rm -rf $delete_log
    fi
    if [ $log_result -gt $reserved_log ];then
        delete_log=$(ls -Srt $result_path'change_result'* | head -$delete_result)
        rm -rf $delete_log
    fi
fi

#Get All Firewall Rules
salt 'GameN1*' cmd.run 'netsh advfirewall firewall show rule name=all' > $log_path$firewall_all

#Transform Firewall File to Standard Format
cat $log_path$firewall_all | sed '/Grouping:\s*$/c\    Grouping:                             N\/A' | grep -v '\-\-' | sed 's/:\s*/:/g' | sed 's/^\ *//g' | sed 's/\ *$//g'| sed 's/:$//g' | grep -v '^$' | grep -v '^Ok.$' | sed 's/\ \ \ */:/g' | sed 's/:$/:N\/A/g' > $log_path$firewall_standard
firewall_new=$log_path$(ls $log_path | tail -n 1)
#Run Compare Diff Script
python /srv/salt/firewall_monitoring/FirewallAnalysis.py $firewall_compare_before $firewall_compare_after $firewall_new $game $first > $change_result

check_result=$(cat $change_result | grep -v 'Profiles' | grep -v 'Grouping' | grep -v 'Edge traversal')

#Check Change result and Send Email
if [[ -s $change_result ]]; then
    echo "${check_result}"
    echo "${check_result}" | mutt -e "my_hdr from:"$Sender -s "[Warning] Windows Firewall Modified!" $Receiver
else
    echo 'Firewall No Changes.'
fi


```
{% endcode-tabs-item %}
{% endcode-tabs %}

