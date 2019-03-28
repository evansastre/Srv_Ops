# Esxi- move management to another vSwitch

1. Open ESXi shell.
2. Under ESXi local console, use "alt+F1" entry ESXi shell.
3. vi /etc/vmware/esx.conf, below is an example

```text
# vSwitch0
/net/vswitch/child[0000]/...
/net/vswitch/child[0000]/name = "vSwitch0"
/net/vswitch/child[0000]/numPorts = "128"
# vSwitch0->portGroupA
/net/vswitch/child[0000]/portgroup/child[0000]/name = "portGroupA"
/net/vswitch/child[0000]/portgroup/child[0000]/teamPolicy/uplinks[0000]/pnic = "vmnic0"
# vSwitch0->portGroupB
/net/vswitch/child[0000]/portgroup/child[0001]/name = "portGroupB"
/net/vswitch/child[0000]/portgroup/child[0001]/teamPolicy/uplinks[0000]/pnic = "vmnic0"
/net/vswitch/child[0000]/uplinks/child[0000]/pnic = "vmnic0"

# vSwitch1
/net/vswitch/child[0001]/...
/net/vswitch/child[0001]/name = "vSwitch1"
/net/vswitch/child[0001]/numPorts = "128"
# vSwitch1->portGroupC (Management Network)
/net/vswitch/child[0001]/portgroup/child[0000]/name = "portGroupC"
/net/vswitch/child[0001]/portgroup/child[0000]/teamPolicy/uplinks[0000]/pnic = "vmnic1"
# vSwitch1->portGroupD
/net/vswitch/child[0001]/portgroup/child[0001]/name = "portGroupD"
/net/vswitch/child[0001]/portgroup/child[0001]/teamPolicy/uplinks[0000]/pnic = "vmnic1"
/net/vswitch/child[0001]/uplinks/child[0000]/pnic = "vmnic1"
```

\(1\) Check the firewall rule of this esxi, if you can ping but can not access its management web

\(2\) Make sure each vswitch has its uplinks

```text
/net/vswitch/child[0000]/uplinks/child[0000]/pnic = "vmnic0"
/net/vswitch/child[0001]/uplinks/child[0000]/pnic = "vmnic1"
```

4. Now, we want to move `portGroupC` from `vSwitch1` to `vSwitch0`, so the configuration is like this:

```text
vSwitch0        --> vmnic0
|--portGroupA
|--portGroupB
|--portGroupC

vSwitch1        --> vmnic1
|--portGroupD
```

To do this, we:

* Identify all of the `portGroupC` lines, which start with `/net/vswitch/child[0001]/portgroup/child[0000]`. Move those entries up with the `vSwitch0` config \(not necessary, but makes things clearer when editing\).
* Change `/net/vswitch/child[0001]` to `/net/vswitch/child[0000]` on each line \(because we're moving it to that switch\).
* Realize that there is already a `/net/vswitch/child[0000]/portgroup/child[0000]`\(`portGroupA`\), and change `portGroupC` to `/portgroup/child[0002]`.
* Realize that our uplink for that port group is now incorrect \(if specified\), and change `uplinks[0000]/pnic =` from `vmnic1` to `vmnic0` \(because that is the vmnic serving that vSwitch.\)

The final config should look like this:

```text
# vSwitch0
/net/vswitch/child[0000]/...
/net/vswitch/child[0000]/name = "vSwitch0"
/net/vswitch/child[0000]/numPorts = "128"
# vSwitch0->portGroupA
/net/vswitch/child[0000]/portgroup/child[0000]/name = "portGroupA"
/net/vswitch/child[0000]/portgroup/child[0000]/teamPolicy/uplinks[0000]/pnic = "vmnic0"
# vSwitch0->portGroupB
/net/vswitch/child[0000]/portgroup/child[0001]/name = "portGroupB"
/net/vswitch/child[0000]/portgroup/child[0001]/teamPolicy/uplinks[0000]/pnic = "vmnic0"
# vSwitch1->portGroupC
/net/vswitch/child[0000]/portgroup/child[0002]/name = "portGroupC"
/net/vswitch/child[0000]/portgroup/child[0002]/teamPolicy/uplinks[0000]/pnic = "vmnic0"
/net/vswitch/child[0000]/uplinks/child[0000]/pnic = "vmnic0"

# vSwitch1
/net/vswitch/child[0001]/...
/net/vswitch/child[0001]/name = "vSwitch1"
/net/vswitch/child[0001]/numPorts = "128"
# vSwitch1->portGroupD
/net/vswitch/child[0001]/portgroup/child[0000]/name = "portGroupD"
/net/vswitch/child[0001]/portgroup/child[0000]/teamPolicy/uplinks[0000]/pnic = "vmnic1"
/net/vswitch/child[0001]/uplinks/child[0000]/pnic = "vmnic1"
```

  
5. Other changes

* Set IP for management 
* Set Vlan ID for management
* Choose vmnic for management
* Change PA rules if need









