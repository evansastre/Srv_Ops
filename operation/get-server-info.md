# get server info

**Get server hostname, private IP, public IP, private MAC address, public MAC address, service tag, os, model.**  
put **hardware.sls** into /srv/salt/

run command: 

```bash
salt '*' state.sls hardware | grep -A1 stdout | egrep -iv 'stdout|--'
or
salt 'minion_id' state.sls hardware | grep -A1 stdout | egrep -iv 'stdout|--'
or
salt -N group_name salt '*' state.sls hardware | grep -A1 stdout | egrep -iv 'stdout|--'
```

Then you can copy and paste the output list to Excel.  


{% code-tabs %}
{% code-tabs-item title="hardware.sls" %}
```bash
{% if grains['os'] == 'Windows' %}
{% set macs = [] -%}
{% set ips = [] -%}
{% for ifname,ip in grains['ip4_interfaces'].iteritems() %}
  {% do ips.insert(0,ip[0]) if ip[0].split('.')[0] == '10' -%}
  {% do ips.append(ip[0]) if ip[0].split('.')[0] != '10' -%}
  {% do macs.insert(0,grains['hwaddr_interfaces'][ifname]) if ip[0].split('.')[0] == '10' %}
  {% do macs.append(grains['hwaddr_interfaces'][ifname]) if ip[0].split('.')[0] != '10' %}
{% endfor %}
echo {{ grains['nodename'] }} , {{ ips | join(' , ') }} , {{ macs | join(' , ') }} , {{ grains['serialnumber'] }} , {{ grains['osfullname'] }} , {{ grains['mem_total'] }} , {{ grains['productname'] }}:
  cmd.run
{% endif %}
{% if grains['os'] == 'CentOS' %}
{% set macs = [] -%}
{% set ips = [] -%}
{% for ifname,ip in grains['ip4_interfaces'].iteritems() %}
  {% if ifname == 'em1' or ifname == 'em2' %}
    {% do ips.insert(0,ip[0]) if ip[0].split('.')[0] == '10' -%}
    {% do ips.append(ip[0]) if ip[0].split('.')[0] != '10' -%}
    {% do macs.insert(0,grains['hwaddr_interfaces'][ifname]) if ip[0].split('.')[0] == '10' %}
    {% do macs.append(grains['hwaddr_interfaces'][ifname]) if ip[0].split('.')[0] != '10' %}
  {% endif %}
{% endfor %}
echo {{ grains['nodename'] }} , {{ ips | join(' , ') }} , {{ macs | join(' , ') }} , {{ grains['serialnumber'] }} , {{ grains['osfullname'] }} , {{ grains['mem_total'] }} , {{ grains['productname'] }}:
  cmd.run
{% endif %}
```
{% endcode-tabs-item %}
{% endcode-tabs %}



**Below is the command to get hardware spec:**

* Windows Server

```bash
Whostnamesalt $i cmd.run 'hostname' | tail -n -1 | sed 's/ //g'`
wWAN=`salt $i network.ip_addrs | tail -n 1 | sed 's/\ //g' | cut -d - -f2`
wLAN=`salt $i network.ip_addrs | tail -n 2 | head -n 1 | sed 's/\ //g' | cut -d - -f2`
Wserialnumber=`salt $i grains.item serialnumber | tail -n 1 | sed 's/ //g'`
Wosfullname=`salt $i grains.item osfullname | tail -n 1 | sed 's/^ *//g'`
Wmemory=`salt $i cmd.run 'wmic ComputerSystem get TotalPhysicalMemory' | tail -n 1 | sed 's/ //g'`
Wmodel=`salt $i grains.item productname | tail -n 1 | sed 's/\ //g'`
wCPU=`salt $i cmd.run 'wmic CPU get name' | tail -n 1 | sed 's/^ *//g'`
wCPU_number=`salt $i cmd.run 'wmic CPU get Name' | grep -v '^$' | grep -v '^ *$' | sed '1,2d' | wc -l`
```

* Linux Server

```bash

Lhostname=`salt $i cmd.run 'hostname' | tail -n -1 | sed 's/ //g'`
LWAN=`salt $i network.ip_addrs | tail -n 1 | sed 's/\ //g' | cut -d - -f2`
LLAN=`salt $i network.ip_addrs | tail -n 2 | head -n 1 | sed 's/\ //g' | cut -d - -f2`
Lserialnumber=`salt $i grains.item serialnumber | tail -n 1 | sed 's/ //g'`
Losfullname=`salt $i cmd.run 'cat /etc/issue' | tail -n 2 | head -n 1 | sed 's/^ *//g' | cut -d '(' -f1`
Lmemory=`salt $i cmd.run 'free -m' | grep 'Mem' | awk '{print $2}'`
Lmodel=`salt $i grains.item productname | tail -n 1 | sed 's/\ //g'`
lCPU=`salt $i cmd.run 'cat /proc/cpuinfo' | grep name | cut -d : -f2 | tail -n 1`
LCPU_number=`salt $i cmd.run 'cat /proc/cpuinfo' | grep 'physical id' | sort | uniq -c | wc -l`
```

* get MAC address

```bash
salt 'xxx' cmd.run 'ipconfig /all| findstr /I /R "Local.Area.Connection Physical.Address IPv4.Address" ' | grep -B 1 IPv4 | cut -d : -f 2 | sed '/--/d'
```

* get user info \(win\)

```bash
salt '*' cmd.run 'net user' | grep -v 'User\ accounts\ for' | grep -v 'The\ command\ ' | grep -v '\-\-\-' | sed '/^\s*$/d'

```

* get user info \(cent\)

```bash
salt '*' cmd.run 'getent passwd'
```

* get machine type \(cent\)

```bash
salt '*' cmd.run 'dmidecode | grep "Product"'
```

  




  


