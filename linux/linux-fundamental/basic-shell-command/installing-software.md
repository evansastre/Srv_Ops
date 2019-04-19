# Installing software

## yum 

```text
yum search string  #Search for string
yum info [package] #Display info
yum install [-y]   #package Install package
yum remove package #Remove package
```

## rpm

```text
rpm -qa
#List all installed packages.
rpm -qf /path/to/file
#List the file’s package.

rpm -ql package
#List package’s files.
rpm -ivh package.rpm
#Install package.
rpm -e package
#Erase (uninstall) package.
```



## APT

```text
apt-cache search string
#Search for string.
apt-get install [-y] package
#Install package.
apt-get remove package
#Remove package, leaving configuration.
apt-get purge package
#Remove package, deleting configuration.
apt-cache show package
#Display information about package.
```

## dpkg

```text
dpkg -l
#List installed packages.
dpkg -S /path/to/file
#List file’s package.
dpkg -L package
#List all files in package.
dpkg -i package.deb
#Install package.
```

