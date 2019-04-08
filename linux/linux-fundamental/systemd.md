# Systemd

## 1.init 

```text
sudo /etc/init.d/apache2 start
#or
service apache2 start
```

This approach has two drawbacks.

* First, the startup time is long. The init process is a serial start, and the next process will be started only after the previous process is started.
* The second is the startup script is complicated. The init process just executes the startup script, no matter what else. Scripts need to handle various situations themselves, which often makes the scripts very long.

## 2.systemd

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

### 3.3 hostnamectl 

The hostnamectl command is used to view information about the current host.

```text
#Display information about the current host
$ hostnamectl
#Set the host name.
$ sudo hostnamectl set-hostname rhel7 
```

### 3.4 localectl 

The localectl command is used to view localization settings.

```text
#View localization settings
$ localectl
#Set localization parameters.
$ sudo localectl set-locale LANG=en_GB.utf8 
$ sudo localectl set-keymap en_GB
```

### 3.5 timedatectl

```text
# View current time zone settings
$ timedatectl

# Show all available time zones
$ timedatectl list-timezones

# Set the current time zone
$ sudo timedatectl set-timezone America/New_York
$ sudo timedatectl set-time YYYY-MM-DD
$ sudo timedatectl set-time HH:MM:SS
```

### 3.6 loginctl

```text
# List current session
$ loginctl list-sessions

# List the currently logged in user
$ loginctl list-users

# List information showing the specified user
$ loginctl show-user ruanyf
```

## 4. Unit

### 4.1 Meaning

Systemd can manage all system resources. Different resources are collectively referred to as Units.

Units are divided into 12 types.

* Service unit：系统服务
* Target unit：多个 Unit 构成的一个组
* Device Unit：硬件设备
* Mount Unit：文件系统的挂载点
* Automount Unit：自动挂载点
* Path Unit：文件或路径
* Scope Unit：不是由 Systemd 启动的外部进程
* Slice Unit：进程组
* Snapshot Unit：Systemd 快照，可以切回某个快照
* Socket Unit：进程间通信的 socket
* Swap Unit：swap 文件
* Timer Unit：定时器

The systemctl list-units command can view all Units of the current system.

```text
# List the running Unit
$ systemctl list-units

# List all Units, including no configuration files found or failed to start
$ systemctl list-units --all

# List all units that are not running
$ systemctl list-units --all --state=inactive

# List all units that failed to load
$ systemctl list-units --failed

# List all running units of type service
$ systemctl list-units --type=service
```

### 4.2 Status of Unit

```text
# Display system status
$ systemctl status

# Display the status of a single unit
$ sysystemctl status bluetooth.service

# Display the status of a unit on the remote host
$ systemctl -H root@rhel7.example.com status httpd.service
```

In addition to the status command, systemctl also provides a simple method for three query states, mainly for use in the internal judgment statements of the script.

```text
# Show if a Unit is running
$ systemctl is-active application.service

# Display whether a Unit is in a startup failure state
$ systemctl is-failed application.service

# Display whether a Unit service has established a startup link
$ systemctl is-enabled application.service
```

### 4.3 Unit Management

```text
#Start a service now
$ sudo systemctl start apache.service

# Stop a service immediately
$ sudo systemctl stop apache.service

# Restart a service
$ sudo systemctl restart apache.service

# Kill all child processes of a service
$ sudo systemctl kill apache.service

# Reload a service's configuration file
$ sudo systemctl reload apache.service

# overload all modified configuration files
$ sudo systemctl daemon-reload

# Display all the underlying parameters of a Unit
$ systemctl show httpd.service

# Display the value of the specified attribute of a Unit
$ systemctl show -p CPUShares httpd.service

# Set the specified attribute of a Unit
$ sudo systemctl set-property httpd.service CPUShares=500
```

### 4.4 Dependencies

There is a dependency between Units: A depends on B, which means that Systemd will start B when it starts A.

The systemctl list-dependencies command lists all the dependencies of a Unit.

```text
$ systemctl list-dependencies nginx.service
```

Among the output of the above command, some dependencies are of the Target type \(see below\), and the default is not expanded. If you want to expand Target, you need to use the --all parameter.

```text
$ systemctl list-dependencies --all nginx.service
```

## 5. Unit's configuration file

5.1 Overview

Each Unit has a configuration file that tells Systemd how to start the Unit.

By default, Systemd reads the configuration file from the directory /etc/systemd/system/. However, most of the files stored inside are symbolic links, pointing to the directory /usr/lib/systemd/system/, where the real configuration files are stored.

The systemctl enable command is used to establish a symbolic link relationship between the two directories above.

```text
$ sudo systemctl enable clamd@scan.service
# equals to
$ sudo ln -s '/usr/lib/systemd/system/clamd@scan.service' '/etc/systemd/system/multi-user.target.wants/clamd@scan.service'
```

If the boot file is set to boot, the systemctl enable command is equivalent to activating the boot.  
Correspondingly, the systemctl disable command is used to revoke the symbolic link relationship between the two directories, which is equivalent to canceling the boot.

```text
$ sudo systemctl disable clamd@scan.service
```

The suffix name of the configuration file is the type of the unit, such as sshd.socket. If omitted, Systemd defaults to .service, so sshd is interpreted as sshd.service.

### 5.2 Status of the configuration file

```text
# List all configuration files
$ systemctl list-unit-files

# List the configuration files of the specified type
$ systemctl list-unit-files --type=service
```

This list shows the status of each profile, for a total of four.

* enabled：Launch link has been established
* disabled：Did not create a launch link
* static：This configuration file does not have an \[Install\] section \(cannot be executed\) and can only be used as a dependency on other configuration files.
* masked：The configuration file is forbidden to create a launch link

Note that it is not clear from the status of the configuration file that the Unit is running. This must be done with the systemctl status command mentioned earlier.

```text
$ systemctl status bluetooth.service
```

Once the configuration file is modified, let SystemD reload the configuration file and restart it, otherwise the modification will not take effect.

```text
$ sudo systemctl daemon-reload
$ sudo systemctl restart httpd.service
```

### 5.3 Format of the configuration file

```text
$ systemctl cat atd.service

[Unit]
Description=ATD daemon

[Service]
Type=forking
ExecStart=/usr/bin/atd

[Install]
WantedBy=multi-user.target
```

### 5.4 Blocks of configuration files

The \[Unit\] block is usually the first block of the configuration file that defines the metadata for the Unit and the relationship to other Units. Its main fields are as follows.

* `Description`：Short description
* `Documentation`：Document Address
* `Requires`：Other Units that the current Unit depends on. If they are not running, the current Unit will fail to start.
* `Wants`：Other Units that match the current Unit, if they are not running, the current Unit will not start failing.
* `BindsTo`：Similar to Requires, if the Unit specified by it exits, it will cause the current Unit to stop running.
* `Before`：If the Unit specified by this field is also to be started, it must be started after the current Unit.
* `After`：If the Unit specified by this field is also to be started, it must be started before the current Unit.
* `Conflicts`：The Unit specified here cannot be run simultaneously with the current Unit.
* `Condition`：The condition that the current Unit must be run, otherwise it will not run.
* `Assert`：The condition that the current Unit must be run, otherwise it will fail to start.

\[Install\] is usually the last block of the configuration file, used to define how to start, and whether to boot. Its main fields are as follows.

* WantedBy: Its value is one or more Targets. The current Unit activation \(enable\) symbolic link will be placed in the /etc/systemd/system directory under the subdirectory of the Target name + .wants suffix. 
* RequiredBy: Its value is one or more Targets. When the current Unit is activated, the symbolic link will be placed in the /etc/systemd/system directory under the subdirectory of the Target name + .required suffix. 
* Alias: Alias that the current Unit can be used to start 
* Also: Other Units that will be activated at the same time when Unit is activated \(enable\)

The \[Service\] block is used for the configuration of the Service. Only the Unit of the Service type has this block. Its main fields are as follows.

* Type: Defines the behavior of the process at startup. It has the following values. 
* Type=simple: default value, execute the command specified by ExecStart, start the main process 
* Type=forking: Create a child process from the parent process in fork mode. After the creation, the parent process will immediately exit. 
* Type=oneshot: One-time process, Systemd will wait for the current service to exit, and then continue to execute 
* Type=dbus: The current service is started by D-Bus 
* Type=notify: After the current service is started, Systemd will be notified, and then continue to execute. 
* Type=idle: The current service will run if other tasks are executed. ExecStart: Command to start the current service 
* ExecStartPre: Command executed before starting the current service 
* ExecStartPost: Command executed after starting the current service ExecReload: Command executed when restarting the current service 
* ExecStop: Command executed when the current service is stopped ExecStopPost: Stops commands executed after their service 
* RestartSec: Number of seconds to automatically restart the current service interval 
* Restart: defines what circumstances Systemd will automatically restart the current service, possible values ​​include always \(always restart\), on-success, on-failure, on-abnormal, on-abort, on-watchdog 
* TimeoutSec: Defines the number of seconds Systemd waits before stopping the current service Environment: Specify environment variables

## 6. Target

When you start your computer, you need to start a large number of Units. If you start each time, it is obviously inconvenient to write out which Units are needed for this startup. The solution for Systemd is Target.

Simply put, Target is a Unit group with many related Units. When a Target is started, Systemd will start all the Units inside. In this sense, the concept of Target is similar to a "state point". Starting a Target is like starting up to a certain state.

In the traditional init startup mode, there is a concept of RunLevel, which is similar to the role of Target. The difference is that RunLevel is mutually exclusive, it is not possible to start multiple RunLevels at the same time, but multiple Targets can be started at the same time.

```text
# View all Targets of the current system
$ systemctl list-unit-files --type=target

# View all Units included in a Target
$ systemctl list-dependencies multi-user.target

# View the default target at startup
$ systemctl get-default

# Set the default target at startup
$ sudo systemctl set-default multi-user.target

# When switching Target, the process started by the previous Target is not closed by default.
# systemctl isolate command to change this behavior,
# Close all processes in the previous Target that do not belong to the next Target.
$ sudo systemctl isolate multi-user.target
```

The correspondence between Target and traditional RunLevel is as follows.

```text
Traditional runlevel      New target name     Symbolically linked to...

Runlevel 0           |    runlevel0.target -> poweroff.target
Runlevel 1           |    runlevel1.target -> rescue.target
Runlevel 2           |    runlevel2.target -> multi-user.target
Runlevel 3           |    runlevel3.target -> multi-user.target
Runlevel 4           |    runlevel4.target -> multi-user.target
Runlevel 5           |    runlevel5.target -> graphical.target
Runlevel 6           |    runlevel6.target -> reboot.target
```

The main differences between it and the init process are as follows.）配置文件的位置，以前init进程的配置文件是/etc/inittab，各种服务的配置文件存放在/etc/sysconfig目录。现在的配置文件主要存放在/lib/systemd目录，在/etc/systemd目录里面的修改可以覆盖原始设置。

1.  The default RunLevel \(set in the /etc/inittab file\) is now replaced by the default Target, located in /etc/systemd/system/default.target, usually symbolically linked to graphical.target \(graphical interface\) or multi-user .target \(multi-user command line\).
2. The location of the startup script, previously in the /etc/init.d directory, symbolically linked to different RunLevel directories \(such as /etc/rc3.d, /etc/rc5.d, etc.\), now stored in /lib/ Systemd/system and /etc/systemd/system directories.
3. The location of the configuration file. The configuration file of the previous init process is /etc/inittab. The configuration files of various services are stored in the /etc/sysconfig directory. The current configuration file is mainly stored in the /lib/systemd directory, and the changes in the /etc/systemd directory can override the original settings.

## 7. log management

Systemd centrally manages the startup logs for all Units. The advantage is that you can view all logs \(kernel logs and application logs\) with just one command of journalctl. The configuration file for the log is /etc/systemd/journald.conf.

Journalctl is powerful and has a lot of usage.

```text
# View all logs (by default, only the logs that are started this time)
$ sudo journalctl

# View kernel logs (do not show application logs)
$ sudo journalctl -k

# View the log of the system startup this time.
$ sudo journalctl -b
$ sudo journalctl -b -0

# View the log that was last started (you need to change the settings)
$ sudo journalctl -b -1

# View logs for a specified time
$ sudo journalctl --since="2012-10-30 18:17:16"
$ sudo journalctl --since "20 min ago"
$ sudo journalctl --since yesterday
$ sudo journalctl --since "2015-01-10" --until "2015-01-11 03:00"
$ sudo journalctl --since 09:00 --until "1 hour ago"

# Display the latest 10 lines of logs at the end
$ sudo journalctl -n

# a log showing the specified number of lines at the end
$ sudo journalctl -n 20

# Real-time scrolling to display the latest logs
$ sudo journalctl -f

# View logs for a specified service
$ sudo journalctl /usr/lib/systemd/systemd

# View the log of the specified process
$ sudo journalctl _PID=1

# View the log of a script for a path
$ sudo journalctl /usr/bin/bash

# View the log of the specified user
$ sudo journalctl _UID=33 --since today

# View the log of a Unit
$ sudo journalctl -u nginx.service
$ sudo journalctl -u nginx.service --since today

# Scrolls the latest log of a Unit in real time
$ sudo journalctl -u nginx.service -f

# Combine logs showing multiple Units
$ journalctl -u nginx.service -u php-fpm.service --since today

# View logs of the specified priority level (and above), a total of 8 levels
# 0: emerg
# 1: alert
# 2: crit
# 3: err
# 4: warning
# 5: notice
# 6: info
# 7: debug
$ sudo journalctl -p err -b

# Log default page output, --no-pager changed to normal standard output
$ sudo journalctl --no-pager

# Output in JSON format (single line)
$ sudo journalctl -b -u nginx.service -o json

# Output in JSON format (multiple lines) for better readability
$ sudo journalctl -b -u nginx.serviceqq
 -o json-pretty

# Show the hard disk space occupied by the log
$ sudo journalctl --disk-usage

# Specify the maximum space occupied by the log file
$ sudo journalctl --vacuum-size=1G

# Specify how long the log file is saved
$ sudo journalctl --vacuum-time=1years
```





























