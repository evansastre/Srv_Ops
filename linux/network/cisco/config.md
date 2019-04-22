# config

思科常用命令大权  
1用户模式

2：特权模式  
enable  
show vlan  
show version  
show interface  
show mac-address-table  
show running-config  
copy running-config startup-config   
3：全局配置模式  
config terminal  
hostname  
enable password  
ip default-gateway  
4：接口配置模式  
interface 端口  
switchport mode trunk

5：line模式  
line console 0

第2章 交换机的基本配置

1.配置主机  
hostname   
2.查看交换机的配置  
show running-config  
使能口令  
enable password  
加密保存的使能口令  
enable secret   
配置IP地址  
interface vlan1  
ip address   
no shutdown  
配置交换机的网关  
ip default-gateway ipaddress  
查看交换机的MAC地址表  
show mac-address-table  
使用CDP协议  
show cdp  
show cdp interface   
show cdp neighbors  
show cdp neighbors detail  
show cdp traffic  
保存与删除交换机配置  
copy running-config startup-config

第三章：虚拟局域网（VLAN）

VLAN的概述  
VLAN是对连接在第2层交换机端口的网络用户的逻辑分段。

VLAN的作用：  
1。广播控制  
2。安全（副产品）  
3。带宽利用  
4。延迟

VLAN的种类  
静态：基于端口的VLAN  
动态：基于MAC地址的VLAN

在交换机上配置静态VLAN

创建VLAN  
1。CONFIG TERMINAL  
VLAN 2  
NAME 2

2。特权模式下  
VLAN DATABASE  
VLAN 2 NAME 2

查看VLAN  
SHOW VLAN  
删除VLAN  
NO VLAN 2  
验证：SHOW VLAN BRIEF

在VLAN中添加端口  
INTERFACE F0/2  
INTERFACE RANGE F0/2 - 5  
SWITCHPORT MODE ACCESS  
SWITCHPORT ACCESS VLAN 2

VLAN配置实例  
在交换机上添加VLAN2，VLAN3，VLAN3，端口范围分别为1-4，5-8，9-12

这个实例的作用就是让不同的VLAN的计算机之间的通信隔开。使达到减少广播域范围的作用。

  
一、交换机基本配置  
（1） 步骤1 ：配置主机名  
switch&gt;enable  
switch\#config t  
switch\(config\)\# hostname sw1  
\(2\) 步骤2 ：配置密码  
sw1\(config\)\#enable secret cisco  
sw1\(config\)\#line vty 0 15  
sw1\(config-line\)\#password cisco  
sw1\(config-line\)\#login  
\(3\)步骤3 ：接口基本配置  
sw1\(config\)\#interface f0/1  
sw1\(config-if\)\#duplex \(full\|half\|auto\)  
//duplex用来配置接口的双工模式：full-全双工 half-半双工 auto-自动监测双工的模式  
sw1\(config-if\)\#speed \(10\|100\|1000\|auto\)  
//speed命令用来配置交换机的接口速度 10-10mbps 100-100mbps 1000-1000mbps auto-自动监测接口速度  
（4）配置管理地址  
交换机允许被telnet ，这时需要在交换机上配置一个ip地址，这个地址是在vlan接口上配置的   
sw1\(config\)\#int vlan 1  
sw1\(config-if\)\#ip address 172.16.0.1 255.255.0.0  
sw1\(config-if\)\#no shutdown   
sw1\(config\)\#ip default-gateway 172.16.0.254  
//以上是vlan 1接口上配置了管理地址，接在vlan 1 上的计算机可以直接进行telnet 该地址，为了其他网段的计算机也可以telnet 交换机，

我们在交换机上配置了默认网关。  
（5） 保存配置  
sw1\#copy running-config startup-config  
二、交换机端口安全

（1）步骤1 ：检查r1的g0/0接口的mac地址  
r1\(config\)\#int g0/0  
r1\(config-if\)\#no shutdown   
r1\(config-if\)\#ip address 172.16.0.101 255.255.0.0  
r1\#show int g0/0 \(查看g0/0接口的mac地址\)  
（2）步骤2：配置交换机端口安全  
sw1\(config\)\#int f0/1  
sw1\(config-if\)\#shutdown   
sw1\(config-if\)\#switch mode access  
//以上命令是把端口改为访问模式，即用来接入计算机  
sw1\(config-if\)\#switch port-security  
//以上命令是打开交换机的端口安全功能   
sw1\(config-if\)\#switch port-security maximum 1  
//以上命令是只允许该端口下的mac条目最大数量为1，即只允许一个设备接入  
sw1\(config-if\)\#switch port-security violation \(protect\|shutdown\|restrict\)  
//命令含义是：protect :当新的计算机接入时，如果该接口的mac条目超过最大数量，则这个新的计算机将无法接入，而原有的计算机不受影响。  
shutdown :当新的计算机接入时，如果该接口的mac条目超过最大数量，则该接口将会被关闭，则这个新的计算机和原有的计算机都无法接入，需要管理员使用“no shutdown”命令重新打开。  
restrict: 当新的计算机接入时，如果该接口的mac条目超过最大数量，则这个新的计算机可以接入，然而交换机将发送警告信息。  
sw1\(config-if\)\#switch port-security mac-address 0019.5535.b828（r1的mac）  
//允许r1路由器从f0/1接口接入。  
sw1\(config-if\)\#no shutdown   
sw1\(config\)\#int vlan 1  
sw1\(config-if\)\#no shutdown   
sw1\(config-if\)\#ip address 172.16.0.1 255.255.0.0  
//以上是配置交换机的管理地址  
（3） 步骤3：检查mac地址表  
sw1\# show mac-address-table  
\(4\)步骤4 模拟非法接入  
r1\# ping 172.16.0.1  
通！  
在r1上修改g0/0的mac地址为另个地址，模拟式另外一台设备接入，  
r1\(config\)\#int g0/0  
r1\(config-if\)\#mac-address 12.12.12  
过几秒后，则在sw1 上出现提示f0/1接口被关闭  
sw1\#show int f0/1  
sw1\#show port-secutity   
//以上命令是查看端口安全的设置情况

三、交换机的密码恢复  
（1） 拔掉交换机电源，按住交换机前面面板的mode键不放，接上电源，  
（2） 输入flash\_init命令。  
（3） 输入load helper 命令  
（4） 输入dir flash:  
//config.text 就是交换机的启动配置文件，和路由器的startup-config 类似。  
\(5\) 输入rename flash:config.text flash:config.old命令  
//以上是将启动配置文件改名，这样交换机启动时就读不到config.text了，从而没有了密码。  
（6）输入boot 命令引导系统，这时就不要在按住mode键了。  
（7）当出现如下提示时，输入n:  
continue with the configuration dialog?:n  
\(8\) 用enable 命令，进入特权模式，并将文件config.old 该回config.text,命令如下。  
sw1\#rename flash:config.old flash:config.text  
\(9\) 将原配置装入内存，命令如下：  
sw1\#copy flash:config.text system:running-config  
\(10\) 修改各个密码：  
sw1\#config t  
sw1（config）\#enable secret cisco  
sw1（config）\#exit  
\(11\) 将配置写入nvram  
sw1\#copy running-config start-config

  
四、交换机的ios恢复  
（1）把计算机的串口和交换机的console口连接好，用超级终端软件连接上交换机，  
（2）交换机开机后，执行以下命令  
switch:flash\_init  
switch:load\_helper  
\(3\) 输入复制指令：  
switch:copy xmodem: flash:c2950-i6q412-mz.121-22.ea5a.bin  
\(4\)传送完毕后执行以下命令：  
switch :boot   
启动系统

  
cisco命令大全  
1.switch配置命令  
\(1\)模式转换命令  
用户模式----特权模式,使用命令"enable"  
特权模式----全局配置模式,使用命令"config t"  
全局配置模式----接口模式,使用命令"interface+接口类型+接口号"  
全局配置模式----线控模式,使用命令"line+接口类型+接口号"  
注:  
用户模式:查看初始化的信息.  
特权模式:查看所有信息、调试、保存配置信息  
全局模式：配置所有信息、针对整个路由器或交换机的所有接口  
接口模式：针对某一个接口的配置  
线控模式：对路由器进行控制的接口配置  
（2）配置命令  
show running config 显示所有的配置  
show versin 显示版本号和寄存器值  
shut down 关闭接口  
no shutdown 打开接口  
ip add +ip地址 配置IP地址  
secondary+IP地址 为接口配置第二个IP地址  
show interface+接口类型+接口号 查看接口管理性  
show controllers interface 查看接口是否有DCE电缆  
show history 查看历史记录  
show terminal 查看终端记录大小  
hostname+主机名 配置路由器或交换机的标识  
config memory 修改保存在NVRAM中的启动配置  
exec timeout 0 0 设置控制台会话超时为0  
service password-encryptin 手工加密所有密码  
enable password +密码 配置明文密码  
ena sec +密码 配置密文密码  
line vty 0 4/15 进入telnet接口  
password +密码 配置telnet密码  
line aux 0 进入AUX接口  
password +密码 配置密码  
line con 0 进入CON接口  
password +密码 配置密码  
bandwidth+数字 配置带宽  
no ip address 删除已配置的IP地址  
show startup config 查看NVRAM中的配置信息  
copy run-config atartup config 保存信息到NVRAM  
write 保存信息到NVRAM  
erase startup-config 清除NVRAM中的配置信息  
show ip interface brief 查看接口的谪要信息  
banner motd \# +信息 + \# 配置路由器或交换机的描素信息  
de script ion+信息 配置接口听描素信息  
vlan database 进入VLAN数据库模式  
vlan +vlan号+ 名称 创建VLAN  
switchport access vlan +vlan号 为VLAN为配接口  
interface vlan +vlan号 进入VLAN接口模式  
ip add +ip地址 为VLAN配置管理IP地址  
vtp+service/tracsparent/client 配置SW的VTP工作模式  
vtp +domain+域名 配置SW的VTP域名  
vtp +password +密码 配置SW的密码  
switchport mode trunk 启用中继  
no vlan +vlan号 删除VLAN  
show spamming-tree vlan +vlan号 查看VLA怕生成树议  
2．路由器配置命令  
ip route+非直连网段+子网掩码+下一跳地址 配置静态/默认路由  
show ip route 查看路由表  
router rip 激活RIP协议  
network +直连网段 发布直连网段  
interface lookback 0 激活逻辑接口  
passive-interface +接口类型+接口号 配置接口为被动模式   
debug ip +协议 动态查看路由更新信息  
undebug all 关闭所有DEBUG信息  
router eigrp +as号 激活EIGRP路由协议  
network +网段+子网掩码 发布直连网段  
show ip eigrp neighbors 查看邻居表  
show ip eigrp topology 查看拓扑表  
show ip eigrp traffic 查看发送包数量  
router ospf +process-ID 激活OSPF协议  
network+直连网段+area+区域号 发布直连网段  
show ip ospf 显示OSPF的进程号和ROUTER-ID  
encapsulation+封装格式 更改封装格式  
no ip admain-lookup 关闭路由器的域名查找  
ip routing 在三层交换机上启用路由功能   
show user 查看SW的在线用户  
clear line +线路号 清除线路  
3．三层交换机配置命令  
配置一组二层端口  
configure terminal 进入配置状态  
nterface range 进入组配置状态  
配置三层端口  
configure terminal 进入配置状态  
interface {{fastethernet \| gigabitethernet} interface-id} \| {vlan vlan-id} \| {port-channel port-channel-number} 进入端口配置

状态  
no switchport 把物理端口变成三层口  
ip address ip\_address subnet\_mask 配置IP地址和掩码  
no shutdown 激活端口  
例：  
Switch\(config\)\# interface gigabitethernet0/2  
Switch\(config-if\)\# no switchport  
Switch\(config-if\)\# ip address 192.20.135.21 255.255.255.0  
Switch\(config-if\)\# no shutdown  
配置VLAN  
configure terminal 进入配置状态  
vlan vlan-id 输入一个VLAN号, 然后进入vlan配态，可以输入一个新的VLAN号或旧的来进行修改。  
name vlan-name 可选\)输入一个VLAN名，如果没有配置VLAN名，缺省的名字是VLAN号前面用0填满的4位数，如VLAN0004是VLAN4的缺省名字  
mtu mtu-size \(可选\) 改变MTU大小  
例  
Switch\# configure terminal  
Switch\(config\)\# vlan 20  
Switch\(config-vlan\)\# name test20  
Switch\(config-vlan\)\# end  
或  
Switch\# vlan database  
Switch\(vlan\)\# vlan 20 name test20  
Switch\(vlan\)\# exit  
将端口分配给一个VLAN  
configure terminal 进入配置状态  
interface interface-id 进入要分配的端口  
switchport mode access 定义二层口  
switchport access vlan vlan-id 把端口分配给某一VLAN  
例  
Switch\# configure terminal   
Enter configuration commands, one per line. End with CNTL/Z.  
Switch\(config\)\# interface fastethernet0/1   
Switch\(config-if\)\# switchport mode access   
Switch\(config-if\)\# switchport access vlan 2  
Switch\(config-if\)\# end   
Switch\#

--------------------------------------------------------------------------------

  
配置VLAN trunk  
configure terminal 进入配置状态  
interface interface-Id 进入端口配置状态  
switchport trunk encapsulation {isl \| dot1q \| negotiate}配置trunk封装ISL 或 802.1Q 或自动协商  
switchport mode {dynamic {auto \| desirable} \| trunk} 配置二层trunk模式。  
dynamic auto—自动协商是否成为trunk  
dynamic desirable—把端口设置为trunk如果对方端口是trunk, desirable, 配置Native VLAN（802.1q）  
或自动模式，trunk—设置端口为强制的trunk方式，而不理会对方端口是否为trunk  
switchport access vlan vlan-id 可选\) 指定一个缺省VLAN, 如果此端口不再是trunk  
switchport trunk native vlan vlan-id 指定802.1Q native VLAN号  
例：  
Switch\# configure terminal   
Enter configuration commands, one per line. End with CNTL/Z.  
Switch\(config\)\# interface fastethernet0/4   
Switch\(config-if\)\# switchport mode trunk   
Switch\(config-if\)\# switchport trunk encapsulation dot1q   
Switch\(config-if\)\# end   
定义TRUNK允许的VLAN  
configure terminal子 进入配置状态  
interface interface-id 进入端口配置  
switchport mode trunk 配置二层口为trunk  
switchport trunk allowed vlan {add \| all \| except \| remove} vlan-list可选\) 配置trunk允许的VLAN.使用add, all, except, remove关健字  
no switchport trunk allowed vlan 允许所有VLAN通过  
例  
Switch\(config\)\# interface fastethernet0/1  
Switch\(config-if\)\# switchport trunk allowed vlan remove 2  
Switch\(config-if\)\# end  
配置Native VLAN（802.1q）  
configure terminal 进入配置状态  
interface interface-id 进入配置成802.1qtrunk的端口  
switchport trunk native vlan vlan-Id 配置native VLAN号  
no switchport trunk native vlan 端口配置命令回到缺省的状态  
配置基于端口权值的负载均衡

configure terminal 进入Switch 1配置状态  
vtp domain domain-name 配置VTP域  
vtp mode server 将Switch 1配置成VTP server.  
show vtp status 验证VTP的配置  
show vlan 验证VLAN  
configure terminal 进入配置状态  
interface fastethernet 0/1 进入F0/1端口  
switchport trunk encapsulation {isl \| dot1q \| negotiate}配置trunk封装  
switchport mode trunk 配置成trunk  
show interfaces fastethernet0/1 switchport 验证VLAN配置  
按以上步骤对想要负载均衡的接口进行配置  
在另一个交换机上进行此配置  
show vlan 当trunk已经起来，在switch2上验证已经学到相的vlan配置  
configure terminal 在Switch 1上进入配置状态  
interface fastethernet0/1 进入要配置的端口  
spanning-tree vlan 8 port-priority 10 将端口权值10赋与VLAN 8.  
spanning-tree vlan 9 port-priority 10 将端口权值10赋与VLAN 9.  
spanning-tree vlan 10 port-priority 10 将端口权值10赋与VLAN 10.  
interface fastethernet0/2 进入F0/2  
spanning-tree vlan 3 port-priority 10 将端口权值10赋与VLAN 3.  
spanning-tree vlan 4 port-priority 10 将端口权值10赋与VLAN 4  
spanning-tree vlan 5 port-priority 10 将端口权值10赋与VLAN 5  
spanning-tree vlan 6 port-priority 10 将端口权值10赋与VLAN 10  
end 退出  
show running-config 验证配置  
copy running-config startup-config 保存配置

配置STP路径值的负载均衡  
Trunk1走VLAN8－10，Trunk2走VLAN2－4

configure terminal 进入 Switch 1配置状态  
interface fastethernet 0/1 进入F0/1  
switchport trunk encapsulation {isl \| dot1q \| negotiate}配置封装  
switchport mode trunk 配置Trunk,缺省是ISL封装  
exit 退回  
在F0/2口上重复2－4步骤  
exit 退回  
show running-config 验证配置  
show vlan验证switch1 已经学到Vlan  
configure terminal 进入配置状态  
interface fastethernet 0/1 进入F0/1  
spanning-tree vlan 2 cost 30 设置Vlan2生成树路径值为30  
spanning-tree vlan 3 cost 30 设置Vlan3生成树路径值为30  
spanning-tree vlan 4 cost 30 设置Vlan4生成树路径值为30  
end 退出  
在switch1的F0/2上重复9－11步骤设置VLAN8,9，10生成树路径值为30  
end 退出  
show running-config 验证配置  
copy running-config startup-config 保存配置

  
switch&gt; ;按Ctrl+Break键  
switch:reset ;或用boot命令  
如果有配置文件进入用户模式，否则提交对话：

--- System Configuration Dialog ---

At any point you may enter a question mark '?' for help.  
Use ctrl-c to abort configuration dialog at any prompt.  
Default settings are in square brackets '\[\]'.  
Continue with configuration dialog? \[yes/no\]:y

Enter IP address:10.65.1.8  
Enter IP netmask:255.255.0.0

Would you like to enter a default gateway address? \[yes\]:  
IP address of default gateway:  
Enter host name \[Switch\]:swa

The enable secret is a one-way cryptographic secret used  
instead of the enable password when it exists.  
Enter enable secret:aaa

Would you like to configure a Telnet password? \[yes\]:  
Enter Telnet password:a

Would you like to enable as a cluster command switch? \[no\]:

The following configuration command was created:  
......  
Press RETURN to get started.  
swa&gt;en  
password:aaa  
swa\#

  
2.路由器的初始化  
路由器初始化与交换机类似，上电时按Ctrl+Break，进入ROM监控状态

router&gt; ；用户模式，按Ctrl+Break  
rommon&gt;reset ；进入ROM监控状态，复位引导  
Continue with configuration dialog? \[yes/no\]:yes

At any point you may enter a question mark '?' for help.  
Use ctrl-c to abort configuration dialog at any prompt.  
Default settings are in square brackets '\[ \]'.

Basic management setup configures only enough connectivity  
for management of the system， extended setup will ask you  
to configure each interface on the system

Would you like to enter basic management setup? \[yes/no\]:yes

Configuring global parameters:

Enter host name \[router\]:ra回车  
The enable secret is a password used to protect access to  
privileged EXEC and configuration modes. This password，  
after entered， becomes encrypted in the configuration.  
Enter enable secret:aaa回车  
The enable password is used when you do not specify an  
enable secret password，with some older software versions，  
and some boot p\_w\_picpaths.  
Enter enable password:aa回车  
The virtual terminal password is used to protect  
access to the router over a network interface.  
Enter virtual terminal password :a回车

Enter interface name used to connect to the management  
network from the above interface summary:FastEthernet0/0回车

Configuring interface FastEthernet0/0:回车  
Use the 100 Base-TX \(RJ-45\) connector? \[yes\]:回车  
Operate in full-duplex mode? \[no\]:回车  
Configure IP on this interface? \[yes\]:回车  
IP address for this interface \[ \]:10.1.1.1回车  
Subnet mask for this interface \[ \]:255.0.0.0回车

\[0\] Go to the IOS command prompt without saving this config.  
\[1\] Return back to the setup without saving this config.  
\[2\] Save this configuration to nvram and exit.  
Enter your selection \[2\]:回车

ra&gt;

  
3. 用命令行设置交换机和路由器的口令和主机名  
交换机和路由器的口令和主机名的设置基本相同，在提问对话时，  
回答n，则进入命令行的状态。  
先对交换机进行操作，双击SwitchA,出现：  
switch&gt;en ；第一次密码为空  
switch\#conf t ；进入全局配置模式  
switch\(config\)\#hostname swa ；设置交换机名  
swa\(config\)\#enable secret aaa ；设置特权加密口令为 aaa  
swa\(config\)\#enable password aax ；设置特权非密口令为 aax  
swa\(config\)\#line console 0 ；进入控制台口\(Rs232\)  
swa\(config-line\)\#password aa ；设置登录口令aa  
swa\(config-line\)\#login ；登录要求口令验证  
swa\(config-line\)\#line vty 0 4 ；进入虚拟终端virtual tty  
swa\(config-line\)\#password a ；设置登录口令a  
swa\(config-line\)\#login ；登录要求口令验证  
swa\(config-line\)\#exit ；返回上一层  
swa\(config\)\#exit ；返回上一层  
swa\#sh run ；看配置信息  
swa\#exit ；返回命令  
swa&gt;en  
password: ；请问输入哪个口 \(aaa\)  
secret是设置加密口令，一般都使用这种口令设置方式，它优先级高，  
即没设置secret口令时，非加密口令才有效。

路由器的设置与交换机类似，双击RouterA，进入用户模式，例如：  
router&gt;en  
router\#conf t  
router\(config\)\#hostname roa  
roa\(config\)\#  
......  
......  
与交换机相同，不现多述。

  
4. 清除交换机口令  
清除交换机口令，实际中是在开机时按住交换机上的mode按钮，在  
模拟软件中按Ctrl+Break，进入ROM方式switch:。  
配置文件是flash:config.text，与nvarm:startup-configuse相同。  
switch:flash\_init  
switch:dir flash:  
switch:delete flash:config.text  
switch:delete nvram:startup-configure  
switch:boot 或  
switch:reset  
因为没有了配置文件，所以重新引导后会提示对话，要求进行配置。  
有些情况下，最好用改名方法，修改口令后现将原配置恢复，再重新设置  
口令后存盘。例如：  
switch:flash\_init  
switch:rename flash:config.text config.bak  
switch:boot  
....  
switch&gt;en  
switch\#copy flash:config.bak running-configure  
switch\#conf t  
switch\(config\)\#en secret aaa  
switch\(config\)\#exit  
switch\#w 或  
switch\#copy run start  
switch\#reload

  
5. 清除路由器口令  
路由器2621的配置文件不让删除和改名，需要采用设置寄存器开关的  
方法实现。  
实际当中是在上电时，按Ctrl+Break。在软件模拟中，双击RouterA  
进入终端模式，再按Ctrl+Break进入rommon&gt;状态，操作如下：

rommon&gt; ；进入ROM监控状态  
rommon&gt;confreg 0x2142 ；跳过配置文件适用26xx 36xx 45xx  
rommon&gt;reset ；重新引导，等效于重开机

Continue with configuration dialog? \[yes/no\]:no  
router&gt;en  
router\#conf t  
router\(config\)\#enable secret bbb ；设置特权加密口令为 bbb  
router\(config\)＃c onfig-register 0x2102 ；正常使用配置文件  
router\(config\)\#exit  
router\#exit  
router&gt;  
router&gt;en  
password:bbb

6. 备份IOS和配置文件  
在实际工作中经常需要备份路由器的IOS和配置文件，以备系统有问题时的  
恢复。可以这样操作：  
router\#dir nvram:  
router\#copy flash:c2621.bin tftp:  
router\#copy startup-config tftp:  
router\#

