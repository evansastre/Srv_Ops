# Kernel Upgrade

```text
#check kernel version
uname -sr

#enable the ELRepo repository
rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
rpm -Uvh http://www.elrepo.org/elrepo-release-7.0-3.el7.elrepo.noarch.rpm 
yum --disablerepo="*" --enablerepo="elrepo-kernel" list available

#install the latest mainline stable kernel
yum --enablerepo=elrepo-kernel install kernel-ml

#Set Default Kernel Version in GRUB
#Open and edit the file /etc/default/grub and set GRUB_DEFAULT=0. 
#recreate the kernel configuration
grub2-mkconfig -o /boot/grub2/grub.cfg

reboot

```

