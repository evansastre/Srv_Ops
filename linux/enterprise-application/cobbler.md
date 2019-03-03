# Cobbler

Traditional pxe: pxe+dhcp+tftp+kickstart only support 



For centos, suse, vmware esxi

[https://github.com/wsgzao/autoinstall/](https://github.com/wsgzao/autoinstall/)



## 通过COBBLER自动安装ESXI6.5

**环境：**

操作系统:

CentOS7.4

网卡：

ens32:dhcp –&gt;internet

ens34:172.16.100.100\(static\)

最好能访问INTERNET,直接从epel源安装，否则有些包安装很不方便

### 1.准备工作

  
  安装系统、配置IP、禁用防火墙、禁用SELINUX..

```text
sed -i 's/SELINUX\=enforcing/SELINUX\=disabled/' /etc/selinux/config 
setenforce 0
systemctl disable firewalld.service 
```

### 2.安装EPEL源

 用EPEL源安装Cobbler很方便

```text
rpm -ivh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
yum repolist
```

### **3**.安装cobbler及相关软件

```text
yum install -y cobbler cobbler-web httpd xinetd tftp-server  pykickstart dhcp
```

版本：

```text
[root@cobbler ~]# rpm -qa|grep cobbler
cobbler-2.8.2-1.el7.x86_64
cobbler-web-2.8.2-1.el7.noarch
```

### 4.配置DHCP使用的接口\(Option\)

```text
[root@cobbler ~]# cat /etc/sysconfig/dhcpd
# Command line options here
DHCPDARGS=ens34#指定DHCP SERVER使用的接口
[root@cobbler ~]# 
```

### 5.开启tftp服务

```text
sed -i 's/disable.*\<yes\>/disable \t\t\= no/g' /etc/xinetd.d/tftp 
```

### 6.重启xinetd服务

```text
    systemctl enable xinetd.service
    systemctl enable rsyncd.service
    systemctl restart xinetd.service
    systemctl restart rsyncd.service
```

### 7.启动服务httpd & cobblerd服务

```text
    systemctl enable httpd.service
    systemctl enable cobblerd.service
    systemctl start httpd.service
    systemctl start cobblerd.service 
```

### 8.下载loaders 

loader包括不同的引导文件\(其实就是syslinux相关的内容\)

```text
root@cobbler ~]# cobbler get-loaders
task started: 2017-12-27_080136_get_loaders
task started (id=Download Bootloader Content, time=Wed Dec 27 08:01:36 2017)
downloading https://cobbler.github.io/loaders/README to /var/lib/cobbler/loaders/README
downloading https://cobbler.github.io/loaders/COPYING.elilo to /var/lib/cobbler/loaders/COPYING.elilo
downloading https://cobbler.github.io/loaders/COPYING.yaboot to /var/lib/cobbler/loaders/COPYING.yaboot
downloading https://cobbler.github.io/loaders/COPYING.syslinux to /var/lib/cobbler/loaders/COPYING.syslinux
downloading https://cobbler.github.io/loaders/elilo-3.8-ia64.efi to /var/lib/cobbler/loaders/elilo-ia64.efi
downloading https://cobbler.github.io/loaders/yaboot-1.3.17 to /var/lib/cobbler/loaders/yaboot
downloading https://cobbler.github.io/loaders/pxelinux.0-3.86 to /var/lib/cobbler/loaders/pxelinux.0
downloading https://cobbler.github.io/loaders/menu.c32-3.86 to /var/lib/cobbler/loaders/menu.c32
downloading https://cobbler.github.io/loaders/grub-0.97-x86.efi to /var/lib/cobbler/loaders/grub-x86.efi
downloading https://cobbler.github.io/loaders/grub-0.97-x86_64.efi to /var/lib/cobbler/loaders/grub-x86_64.efi
*** TASK COMPLETE ***
[root@cobbler ~]# 
```

### 9.修改cobbler配置文件

首先生成MD5加密的密码串：

```text
[root@cobbler ~]# openssl passwd -1 'www.54lqy.COM'
$1$2ULUTdGJ$YZ2yXrPQZslILPduEIr6Y.
[root@cobbler ~]# 
```

修改配置文件：

```text
cp /etc/cobbler/settings /etc/cobbler/settings.orig
vi /etc/cobbler/settings
编辑以下几行为对应的信息:
[root@cobbler ~]# grep -v '^#' /etc/cobbler/settings|grep -E -w '(next_server|server|default_password_crypted|manage_dhcp|pxe_just_once|manage_rsync)'
default_password_crypted: "$1$2ULUTdGJ$YZ2yXrPQZslILPduEIr6Y."  #系统安装后默认的root密码(MD5加密)
manage_dhcp: 1                      #由cobbler来管理DHCP
next_server: 172.16.100.100         #指定NEXT_SERVER(TFTP-SERVER)为本机IP
pxe_just_once: 1                    #防止已安装过操作系统的服务器重复安装
server: 172.16.100.100              #指定为本机的IP地址
manage_rsync: 1                     #由cobbler来管理rsync
[root@cobbler ~]# 
```

### 10.配置DHCP

  
  上面配置已设定dhcp由cobbler来控制，不用再去配置/etc/dhcp/dhcpd.conf（会自动同步）  
只更改与IP相关的选项（其它保持默认）：

```text
cat /etc/cobbler/dhcp.template 
..............cut..............
subnet 172.16.100.0 netmask 255.255.255.0 {
     option routers             172.16.100.1;
     option subnet-mask         255.255.255.0;
     range dynamic-bootp        172.16.100.200 172.16.100.230;
     default-lease-time         21600;
     max-lease-time             43200;
     next-server                $next_server;       #这里引用cobbler配置文件的next_server变量
..............cut...............
```

### 11.配置检查

```text
[root@cobbler ~]# systemctl restart cobblerd.service
[root@cobbler ~]# cobbler check
The following are potential configuration items that you may want to fix:

    1 : debmirror package is not installed, it will be required to manage debian deployments and repositories
    2 : fencing tools were not found, and are required to use the (optional) power management features. install cman or fence-agents to use them

    Restart cobblerd and then run 'cobbler sync' to apply changes.
[root@cobbler ~]# 
```

> 1:与debian相关的镜像；  
> 2:fence设备\(配置过RHCS的都知道是干嘛用的..\)；  
> 这两项这里均用不到，可以不用理会。
>
> > /\*  
> > 如果是强迫症患者，可通过以下方法来处理\(所有包安装完毕大约占50M左右空间\)：  
> > yum install -y debmirror  
> > 然后配置：  
> > sed -i -e ‘s/\@dists/dists/g;s/\@arches/arches/g’ /etc/debmirror.conf  
> > yum install -y fence-agent\*  
> > 然后再运行cobbler check,会发现整个世界都清静了..  
> > \[root@cobbler ~\]\# cobbler check  
> > No configuration problems found. All systems go.  
> > \[root@cobbler ~\]\#  
> > \*/

**！！重启一次操作系统！！**

### 12.加载ESXi ISO

安装的版本为：VMware-VMvisor-Installer-6.5.0.update01-5969303.x86\_64.iso

```text
mount /dev/cdrom /media/cdrom
```

### 13.导入ESXI操作系统

```text
[root@cobbler ~]# cobbler import --path=/media/cdrom --name=Esxi6.5U1 --arch=x86_64
task started: 2018-01-06_110127_import
task started (id=Media import, time=Sat Jan  6 11:01:27 2018)
Found a candidate signature: breed=vmware, version=esxi51
running: /usr/bin/file /var/www/cobbler/ks_mirror/Esxi6.5U1-x86_64/s.v00
received on stdout: /var/www/cobbler/ks_mirror/Esxi6.5U1-x86_64/s.v00: gzip compressed data, was "vmvisor-sys.vxz-psigned", from Unix, last modified: Fri Jul  7 12:33:27 2017

received on stderr: 
Found a candidate signature: breed=vmware, version=esxi60
running: /usr/bin/file /var/www/cobbler/ks_mirror/Esxi6.5U1-x86_64/s.v00
received on stdout: /var/www/cobbler/ks_mirror/Esxi6.5U1-x86_64/s.v00: gzip compressed data, was "vmvisor-sys.vxz-psigned", from Unix, last modified: Fri Jul  7 12:33:27 2017

received on stderr: 
Found a candidate signature: breed=vmware, version=esxi5
running: /usr/bin/file /var/www/cobbler/ks_mirror/Esxi6.5U1-x86_64/s.v00
received on stdout: /var/www/cobbler/ks_mirror/Esxi6.5U1-x86_64/s.v00: gzip compressed data, was "vmvisor-sys.vxz-psigned", from Unix, last modified: Fri Jul  7 12:33:27 2017

received on stderr: 
Found a candidate signature: breed=vmware, version=esxi55
running: /usr/bin/file /var/www/cobbler/ks_mirror/Esxi6.5U1-x86_64/s.v00
received on stdout: /var/www/cobbler/ks_mirror/Esxi6.5U1-x86_64/s.v00: gzip compressed data, was "vmvisor-sys.vxz-psigned", from Unix, last modified: Fri Jul  7 12:33:27 2017

received on stderr: 
No signature matched in /var/www/cobbler/ks_mirror/Esxi6.5U1-x86_64
!!! TASK FAILED !!!
[root@cobbler ~]# 
```

如报如上错误，表示没有符合esxi6.5的签名

先更新签名：

```text
root@cobbler ~]# cobbler signature update
task started: 2017-12-27_113815_sigupdate
task started (id=Updating Signatures, time=Wed Dec 27 11:38:15 2017)
Successfully got file from https://cobbler.github.io/signatures/2.8.x/latest.json
*** TASK COMPLETE ***
[root@cobbler ~]# 
```

但是更新后也没有ESXI6.5的签名信息\(最高是esxi60\)：

```text
[root@cobbler cobbler]# cobbler signature report|grep esxi
        esxi4
        esxi5
        esxi51
        esxi55
        esxi60
[root@cobbler cobbler]# 
```

修改签名文件，增加对ESXI6.5的支持：

```text
cd /var/lib/cobbler
cp distro_signatures.json distro_signatures.json.orig
```

编辑distro\_signatures.json:  
在”freebsd”与”esxi60″之间，增加以下字段\(注意格式\)：

```text
"esxi65": {
    "signatures":["tboot.b00"],
    "version_file":"vmware-esx-base-osl\\.txt",
    "version_file_regex":"^(VMware )?ESXi (v)?6\\.5.*$",
    "kernel_arch":"tools\\.t00",
    "kernel_arch_regex":"^.*(x86_64).*$",
    "supported_arches":["x86_64"],
    "supported_repo_breeds":[],
    "kernel_file":"mboot\\.c32",
    "initrd_file":"imgpayld\\.tgz",
    "isolinux_ok":false,
    "default_kickstart":"/var/lib/cobbler/kickstarts/sample_esxi6.ks",
    "kernel_options":"",
    "kernel_options_post":"",
    "template_files":"/etc/cobbler/pxe/bootcfg_esxi65.template=$local_img_path/cobbler-boot.cfg",
    "boot_files":["*.*"]
   }
  },
```

重启服务并验证是否已生效：

```text
[root@cobbler cobbler]# cobbler signature reload
Signatures were successfully loaded
[root@cobbler cobbler]# systemctl restart cobblerd.service
[root@cobbler cobbler]# cobbler signature report|grep esxi
        esxi4
        esxi5
        esxi51
        esxi55
        esxi60
        esxi65
[root@cobbler cobbler]# 
```

### 14.重新导入ESXI65系统

```text
[root@cobbler ~]# cobbler import --path=/media/cdrom --name=ESXI65U1 --arch=x86_64
task started: 2017-12-27_125344_import
task started (id=Media import, time=Wed Dec 27 12:53:44 2017)
Found a candidate signature: breed=vmware, version=esxi65
running: /usr/bin/file /var/www/cobbler/ks_mirror/ESXI65U1-x86_64/vmware-esx-base-osl.txt
received on stdout: /var/www/cobbler/ks_mirror/ESXI65U1-x86_64/vmware-esx-base-osl.txt: UTF-8 Unicode text, with very long lines, with CRLF line terminators

received on stderr: 
Found a matching signature: breed=vmware, version=esxi65
Adding distros from path /var/www/cobbler/ks_mirror/ESXI65U1-x86_64:
running: /usr/bin/file /var/www/cobbler/ks_mirror/ESXI65U1-x86_64/tools.t00
received on stdout: /var/www/cobbler/ks_mirror/ESXI65U1-x86_64/tools.t00: gzip compressed data, was "tools-light.tar", from Unix, last modified: Fri Jul  7 12:26:30 2017

received on stderr: 
creating new distro: ESXI65U1-x86_64
trying symlink: /var/www/cobbler/ks_mirror/ESXI65U1-x86_64 -> /var/www/cobbler/links/ESXI65U1-x86_64
creating new profile: ESXI65U1-x86_64
associating repos
*** TASK COMPLETE ***
[root@cobbler ~]# 
```

### 15.同步配置

```text
[root@cobbler cobbler]# cobbler sync  
task started: 2017-12-27_125702_sync
task started (id=Sync, time=Wed Dec 27 12:57:02 2017)
-------cut-----
*** TASK COMPLETE ***
[root@cobbler cobbler]# 
```

### 16.查看引导文件：cobbler-boot.cfg （不用修改）

```text
[root@cobbler ~]# head -5 /var/lib/tftpboot/images/ESXI65U1-x86_64/cobbler-boot.cfg
bootstate=0
title=Loading ESXi installer
prefix=/images/ESXI65U1-x86_64
kernel=tboot.b00
kernelopt=runweasel ks=http://172.16.100.100:80/cblr/svc/op/ks/profile/ESXI65U1-x86_64
[root@cobbler ~]# 
```

### 17.配置kickstart文件

```text
cp /var/lib/cobbler/kickstarts/sample_esxi6.ks /var/lib/cobbler/kickstarts/esxi6.ks

[root@cobbler pxelinux.cfg]# cat  /var/lib/cobbler/kickstarts/esxi6.ks
#
# Sample scripted installation file
# for ESXi 6+
#

vmaccepteula
reboot --noeject
rootpw --iscrypted $default_password_crypted    #使用cobbler设置的密码

install --firstdisk --overwritevmfs
clearpart --firstdisk --overwritevmfs

##$SNIPPET('network_config')  #注释掉此行（否则安装程序配置网络的时候会报错）
network --bootproto=dhcp      #增加此行

%pre --interpreter=busybox

$SNIPPET('kickstart_start')
$SNIPPET('pre_install_network_config')

%post --interpreter=busybox

$SNIPPET('kickstart_done')
[root@cobbler pxelinux.cfg]# 
```

更改默认kickstarts文件为上述修改后的文件：

```text
[root@cobbler cobbler]# cobbler profile list
   ESXI65U1-x86_64
[root@cobbler cobbler]# cobbler profile edit --name=ESXI65U1-x86_64 --kickstart=/var/lib/cobbler/kickstarts/esxi6.ks
[root@cobbler cobbler]# cobbler report
distros:
-------------cut-------
profiles:
==========
Name                           : ESXI65U1-x86_64
TFTP Boot Files                : {}
Comment                        : 
DHCP Tag                       : default
Distribution                   : ESXI65U1-x86_64
Enable gPXE?                   : 0
Enable PXE Menu?               : 1
Fetchable Files                : {}
Kernel Options                 : {}
Kernel Options (Post Install)  : {}
Kickstart                      : /var/lib/cobbler/kickstarts/esxi6.ks
Kickstart Metadata             : {}
Management Classes             : []
Management Parameters          : <<inherit>>
-----------cut---------

[root@cobbler cobbler]# 
```

### 18.修改引导配置文件

```text
[root@cobbler snippets]# cat /var/lib/tftpboot/pxelinux.cfg/default 
DEFAULT menu
PROMPT 0
MENU TITLE Cobbler 
TIMEOUT 50              #超时时间
TOTALTIMEOUT 6000
ONTIMEOUT ESXI65U1-x86_64       #不手动干预时，默认从ESXI65U1-x86_64引导

LABEL local
        MENU LABEL (local)
        MENU DEFAULT
        LOCALBOOT -1

LABEL ESXI65U1-x86_64
        kernel /images/ESXI65U1-x86_64/mboot.c32
        MENU LABEL ESXI65U1-x86_64
        ipappend 2
        append -c /images/ESXI65U1-x86_64/cobbler-boot.cfg

MENU end
```

**注：修改完上述文件不用同步，同步后又会恢复默认。**

### 19.客户机安装操作系统

```text
   把此环境与ESXi服务器接入到同一网络(如果是笔记本的VM,可以把DHCP的网卡设备“桥接“模式)
   ESXi服务器从网络启动就可以自动安装ESXi系统。
   可用vmware workstation创建一个类型为ESXI的虚拟机来测试
```

**日志目录及文件**：

/var/log/cobbler/cobbler.log \#cobbler的主要日志文件

/var/log/cobbler \#日志目录

/var/log/messages \#也会记录一些信息

**更新-EFI引导安装：**

从EFI引导安装

  如果服务器从EFI引导，可按如下方法配置：

1.设置efi引导文件  
  把esxi光盘的bootx64.efi文件替换grub-x86\_64.efi文件\(或者更改dhcp配置文件，指定为esxi的bootx64.efi\)

```text
~]# cp /var/lib/tftpboot/grub/grub-x86_64.efi /var/lib/tftpboot/grub/grub-x86_64.efi.bak
~]# cp /media/cdrom/efi/boot/bootx64.efi /var/lib/tftpboot/grub/grub-x86_64.efi
(注：这里ESXI光盘mount 在/media/cdrom)
```

2.生成boot.cfg文件

```text
ln -s /var/lib/tftpboot/images/ESXI65U1-x86_64/cobbler-boot.cfg  /var/lib/tftpboot/grub/boot.cfg
```

3.客户机从EFI引导安装

默认引导文件：

```text
]# cat /var/lib/tftpboot/grub/efidefault 
default=0
timeout=0

title ESXI65U1-x86_64
    root (nd)
    kernel /images/ESXI65U1-x86_64/mboot.c32  ks=http://172.16.100.100/cblr/svc/op/ks/profile/ESXI65U1-x86_64  lang=  text 
    initrd /images/ESXI65U1-x86_64/imgpayld.tgz
]#
```

