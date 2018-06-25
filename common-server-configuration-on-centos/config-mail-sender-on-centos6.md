# Config mail sender on centos6

### install

```bash
yum install mutt sendmail
vim /etc/Muttrc
```

### **find and config:**

```bash
set sendmail="/usr/sbin/senmail -oem -oi"
#save and quit editor:
!wq
```

### restart sendmail

```bash
service sendmail restart chkconfig sendmail on
```

### Test

```bash
echo "Alert message!!!" | mutt -e "my_hdr from:sender<sender@mydomain.com>" -s "[Warning]Title " receiver@xxxx.com
```



