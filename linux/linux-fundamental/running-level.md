# running level



1. \#   0 - halt \(Do NOT set initdefault to this\)  
2. \#   1 - Single user mode  
3. \#   2 - Multiuser, without NFS \(The same as 3, if you do not have networking\)  
4. \#   3 - Full multiuser mode  
5. \#   4 - unused  
6. \#   5 - X11  
7. \#   6 - reboot \(Do NOT set initdefault to this\)  



```text
init 0  #equal to halt
init 6  #equal to reboot

$cd /etc/rc.d
$ls
init.d  rc0.d  rc1.d  rc2.d  rc3.d  rc4.d  rc5.d  rc6.d  rc.local

```

Run a service\(nginx\) only in level 3 and 5

```text
chkconfig nginx off
chkconfig --level 35 nginx on
```











