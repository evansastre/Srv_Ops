# SVN

## SVN server

Install 

```text
brew install svn
svnserve --version
```

Create repo

```text
svnadmin create /patch/dir
```

Modify config files :   under svn/conf - svnserve.conf、passwd、authz

svnserve.conf:

```text
#Do not leave any space one left
anon-access = read
auth-access = write
password-db = passwd
authz-db = authz
```

passwd:

```text
[users]
# harry = harryssecret
# sally = sallyssecret
test1 = 123456
```

authz:

```text
## add SVN group  = test1， test2
svn_group = test1, test2

## group privilege under [/]  
[/]
## @groupname = （rw）
@svn_group = rw
```

Start SVN:

```text
sudo svnserve -d -r /svn
#test
telnet localhost 3690
```

Close SVN

```text
ps aux | grep svn
#kill pid
```

\*\*\*\*

## **SVN client**

Download and Install Cornerstone

Click "Add Repository" 

Fill "SVN Server" 

Server:127.0.0.1

Name: \(username set in passwd file\)

Passsword:\(password set in passwd file\)

Click "Add"

Click "Check Out Working Copy"









