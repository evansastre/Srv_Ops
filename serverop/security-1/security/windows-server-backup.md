# Windows Server Backup

## **To setup windows backup:**

### diskpart

Create file cmd.txt 

{% code-tabs %}
{% code-tabs-item title="cmd.txt" %}
```bash
select volume D
shrink desired 51200
convert dynamic
create volume simple size=51200
assign letter=Z
format fs=ntfs label="Server Backup"
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Excute

```bash
salt '*' cp.get_file salt://cmd.txt 'D:\cmd.txt'
salt '*' cmd.run 'diskpart /s D:\cmd.txt'
#Check
salt '*' cmd.run 'pushd Z:\'
```

### Install feature "Windows server backup"

```bash
salt '*' cmd.run 'dism /online /enable-feature /featurename:WindowsServerBackup'
#salt '*' cmd.run 'dism /online /enable-feature /featurename:WindowsServerBackupCommandlet'
```

## **To perform windows backup:**

### Backup 

```bash
salt '*' cmd.run 'wbadmin start systemstatebackup -backuptarget:Z: -quiet'
```

### Keep Version

```bash
salt '*' cmd.run 'wbadmin delete backup -keepVersions:3'
```

## **To perform recovery use windows backup:**

### [Disable McAfee Agent](http://gtoconfluence.garenanow.com:8090/display/BNS/Disable+McAfee+Agent) <a id="WindowsServerBackup-DisableMcAfeeAgent"></a>



### Uninstall Anti-Virus <a id="WindowsServerBackup-UninstallAnti-Virus"></a>

```bash
#open control panel to unstall VirusScan
#then use command uninstall Agent
cd "C:\software\McAfee\Common Framework"
FrmInst.exe /remove=agent
```

### Recovery <a id="WindowsServerBackup-Recovery"></a>

```bash
#get versions, for example get version : 04/09/2018-03:02
salt '*' cmd.run 'wbadmin get versions -backupTarget:Z:'
#recovery  !!!need close anti-virus
salt '*' cmd.run 'wbadmin start systemstaterecovery -backuptarget:Z: -version:04/09/2018-03:02 -quiet'
```

### Mcafee Recovery after reboot <a id="WindowsServerBackup-McafeeRecoveryafterreboot"></a>

```bash
#1.Copy these folder from other server to unstalled-mcafee server
X:\software\McAfee\VirusScan Enterprise\RepairCache\
C:\ProgramData\McAfee\Common Framework\
 
#2.Open control panel to uninstall agent and virus-scan again
#3.Delete related folders
#4.Install Mcafee with normal way
```

