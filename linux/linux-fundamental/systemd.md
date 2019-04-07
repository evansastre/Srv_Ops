# Systemd

## init 

```text
sudo /etc/init.d/apache2 start
#or
service apache2 start
```

This approach has two drawbacks.

* First, the startup time is long. The init process is a serial start, and the next process will be started only after the previous process is started.
* The second is the startup script is complicated. The init process just executes the startup script, no matter what else. Scripts need to handle various situations themselves, which often makes the scripts very long.

## systemd

Systemd was born to solve these problems. It is designed to provide a complete solution for system startup and management.

With Systemd, you don't need to use init again. Systemd replaces initd and becomes the first process of the system \(PID equals 1\), and other processes are its child processes.

The advantages of Systemd are that they are powerful and easy to use. The disadvantage is that the system is huge and complex. In fact, there are still many people who oppose Systemd, on the grounds that it is too complex and strongly coupled with the rest of the operating system, violating the "keep simple, keep stupid" Unix philosophy.

![](../../.gitbook/assets/systemd.png)

## System management

Systemd is not a command, but a set of commands that cover all aspects of system management.

### 3.1 systemctl

Systemctl is the main command of Systemd for managing systems



```text
# reboot
$ sudo systemctl reboot

# poweroff
$ sudo systemctl poweroff

# CPU stops working
$ sudo systemctl halt

# pause
$ sudo systemctl suspend

# Let the system go into hibernation
$ sudo systemctl hibernate

# Put the system into interactive sleep
$ sudo systemctl hybrid-sleep

# Start to enter rescue state (single user state)
$ sudo systemctl rescue
```

### 3.2 systemd-analyze 

The systemd-analyze command is used to view the startup time.

```text
# View startup time
$ systemd-analyze

# View the start time of each service
$ systemd-analyze blame

# Show waterfall-like startup process flow
$ systemd-analyze critical-chain

# Display the startup flow of the specified service
$ systemd-analyze critical-chain atd.service
```

