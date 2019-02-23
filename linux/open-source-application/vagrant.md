# Vagrant

[Vagrant Docs](https://www.vagrantup.com/docs/index.htmlhttps://www.vagrantup.com/docs/index.html)



Usage

1. Download and Install : vagrant, virtualbox

Download vagrant: [https://www.vagrantup.com/downloads.html](https://www.google.com/url?q=https%3A%2F%2Fwww.vagrantup.com%2Fdownloads.html&sa=D&sntz=1&usg=AFQjCNE24kc_BPH2Jbk0sOX9oE-m5pL3Tg)

Download virtualbox: [https://www.virtualbox.org/wiki/Downloads](https://www.google.com/url?q=https%3A%2F%2Fwww.virtualbox.org%2Fwiki%2FDownloads&sa=D&sntz=1&usg=AFQjCNFpVPZ1LROUoLBW-3yzRbtHjKwm8w)

Check

Vagrant 2.2.0

```text
$vagrant --version
Vagrant 2.2.0
$ VBoxManage --version
5.2.12r122591
```

2. Add blueking image to vagrant

Download bluking image: http://bkopen-10032816.file.myqcloud.com/paas/bk-django1.8-u2.box

bk-django1.8.box is the name of bluking image. Including centos7+Django+a series of blueking necessary units.

```text
vagrant box add bk bk-django1.8.box  # bk is defined for this box 
```

3. Initial

Make your own workstation path for vagrant

```text
mkdir /Users/BK/vagrant/django18  #for example
cd /Users/BK/vagrant/django18
vagrant init bk   #init.   

#will auto create "Vagrantfile" for configuring, we can settings like folder share or port-forward here. If share folder's patch not set, current path will be default path.
# For user "root" and "vagrant", default password is "vagrant".
vim Vagrant
#config.vm.box = "bk"
#config.vm.network "forwarded_port", guest: 8000, host: 1234

vagrant up        #start up 
vagrant ssh       #ssh to this environment
```

4.Config framework, create database

```text
cp framework.tar.gz /Users/BK/vagrant/django18/
cd /Users/BK/vagrant/django18/
tar xf framework.tar.gz

vagrant ssh  #ssh to blueking dev env
cd /vagrant/framework

mysql -u root
#create databas myapp01, myapp01 is APP_ID, will use in config file 
mysql>create database myapp01 default character set utf8 collate utf8_general_ci;
#change password for root
mysql>use mysql
mysql>show 
mysql>show columns from user;
mysql>select User,Host,Password from user;
mysql>update user set Password=password('vagrant') where User='root';
mysql>flush privileges;
mysql>exit

Edit ./conf/default.py
# APP_ID = 'myapp01'
# BK_PAAS_HOST = 'http://paas.bk.test.garena.com'

Edit ./conf/settings_development.py  conf/settings_testing.py conf/settings_production.py
#'NAME': myapp01,                        # database name (same as APP_ID)
#'USER': 'root',                  
#'PASSWORD': 'vagrant'

cd /vagrant/framework
python manage.py migrate
```

5.Run server

```text
#run
python manage.py runserver 0.0.0.0:8000

#if no DNS, you should set hosts both in bk env and your local
150.109.2.217 paas.bk.test.garena.com
150.109.2.217 cmdb.bk.test.garena.com
150.109.2.217 job.bk.test.garena.com
150.109.2.217 o.bk.test.garena.com
150.109.2.217 t.bk.test.garena.com

#for your local hosts, need one more rule
127.0.0.1     dev.bk.test.garena.com
```

Open browser,  [http://dev.bk.test.garena.com](http://dev.bk.test.garena.com):1234

more command of vagrant visit here:  [https://www.vagrantup.com/docs/cli/index.html](https://www.vagrantup.com/docs/cli/index.html)  






