# Config mail sender on centos

```bash
#install
yum install mutt sendmail

vim /etc/Muttrc
# find and config:  
set sendmail="/usr/sbin/senmail -oem -oi"
# save and quit editor:  
!wq

#restart sendmail
service sendmail restart
chkconfig sendmail on

#Test
echo "Alert message!!!" | mutt -e "my_hdr from:sender<sender@mydomain.com>" -s "[Warning]Title " receiver@xxxx.com
```

IPtables rule enable sendmail

{% code-tabs %}
{% code-tabs-item title="/etc/sysconfig/iptables" %}
```bash
-A INPUT -i lo -j ACCEPT
-A OUTPUT -o lo -j ACCEPT
*------*
 
#mail outgoing
-A OUTPUT -p tcp --dport 25 -j ACCEPT
#DNS outgoing
-A OUTPUT -p udp --dport 53 -j ACCEPT
#allow the related/established connections
-A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
-A OUTPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
 
*------*
-A INPUT -j DROP
-A OUTPUT -j DROP
```
{% endcode-tabs-item %}
{% endcode-tabs %}

