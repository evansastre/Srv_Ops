# AD Database

Active directory database uses the “**Extensible Storage Engine \(ESE\)**” which is an **indexed and sequential access method \(ISAM\) database**. It is uses record-oriented database architecture which provides extremely fast access to records. ESE indexes the data in the database file. This database file can grow up to 16 terabyte and hold over 2 billion records.

The default active directory database file location is **C:\Windows\NTDS**

\*\*\*\*

**Ntds.dit** – This is the physical active directory database file. This is where all the active directory data stored. It holds domain info, schema info and configuration info. Mainly it contain 3 tables.  
1\)    Link table  
2\)    Data table  
3\)    Security Depositor table

**Edb.log** – in here we can see the few log files starts with edb\*. Each of them are 10mb or less in size. It is the transaction log maintain by system to store the directory transaction before write in to the database file.

**Edb.chk** – it is the file to keep track of data transaction committed in to database from log files \(Edb\*.log\).

**Temp.edb** – This is used during the active directory database maintenance to hold data and also to store info about large in-progress AD data transactions.

**Res1.log and Res2.log** – Even we can’t see it in this example this is a file type which will store log entries if edb.log file full.

**SYSVOL**

SYSVOL is a shared folder which contains files which is common for the domain. This share will be created automatically when set up the DC. The default file location is **C:\Windows\SYSVOL** but it can be change during the DC setup.

[![addb2](http://www.rebeladmin.com/wp-content/uploads/2015/02/addb2.png)](http://www.rebeladmin.com/wp-content/uploads/2015/02/addb2.png)

[![addb3](http://www.rebeladmin.com/wp-content/uploads/2015/02/addb3.png)](http://www.rebeladmin.com/wp-content/uploads/2015/02/addb3.png)

Let’s see what sort of data sysvol folder will have.

**Group Policies** – Group policies will use to manage user and computers based on company requirements. It can be to control computer application, security, network behaviors etc. Those will apply to computer accounts when those are restarted and connect to the domain. User policies will apply when they log in to domain computers.

**Login Scripts** – It also used to store login scripts for the domain users. Those are load when users log in to domain computer. It can be batch file, PowerShell script or vbscript.

[![addb4](http://www.rebeladmin.com/wp-content/uploads/2015/02/addb4.png)](http://www.rebeladmin.com/wp-content/uploads/2015/02/addb4.png)

**Staging folders** – This is used to sync data and files between domain controllers.

**File system junctions** – an isolated location in hard disk which refers to the data located in different partition, or different storage device.

**System State**  


All most all backup solution allows you to backup “system states” in windows environment. When I ask some engineers “how you backup dc?” most of them says you need to backup system state. But how many of you know what exactly system state have?

It includes the following list of files and data.

**Active Directory DC Database file \(ntds.dit\)  
SYSVOL folder and its files  
Certificate Store  
User Profiles  
IIS metabase  
Boot files  
DLL cache folder  
Registry info  
COM+ and WMI info  
Cluster service info  
Windows Resource Protection system files**  


So if you looking to backup domain controller you need to back up the system state. The size of the system state backup depend of the size of the above files and folders.

