# Switch User and running commands as others

## su

```text
su [username] #change user ID or become superuser
-             #A hyphen is used to provide an environment similar to what the user would expect had the user logged in directly.
-c command    #Specify a command to be executed.

whoami #Displays the effective username.

#Example
$export TEST=1
$echo $TEST   
1
$su oracle 
$whoami
oracle
$echo $TEST  #Show 1 here, still in current account's environment
1
$exit
su - oracle
$echo $TEST  #show nothing here, because now in oracle's environment 

$pwd
/home/oracle 


#Example
$su -c 'echo $ORACLE_HOME' oracle #nothing return
$su -c 'echo $ORACLE_HOME' - oracle #show something
/u01/app/oracle/product/current
```

## sudo

```text
sudo #Execute a command as another user, typically the superuser.
sudo -l      #List available commands.
sudo command #Run command as root.
sudo -u root command #Same as above.
sudo -u user command #Run as user.

sudo su #Switch to the superuser account.
sudo su - #Switch to the superuser account with root’s environment.
sudo su - username #Switch to the username account.

visudo #edit /etc/sudoers

#Sudoers Format
user host=(users) [NOPASSWD:]commands
adminuser ALL=(ALL) NOPASSWD:ALL
jason linuxsvr=(root) /etc/init.d/oracle

```

