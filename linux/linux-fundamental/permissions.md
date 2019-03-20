# Permissions

```bash
# Permission  File                       | Directory
# r read     Allows a file to be read.   | Allowd file names in the directory to be read.   
# w write    Allows a file to be modified. | Allows entries to be modified within the directory.
# x execute  Allow the exexution of a file | Allows access to contents and metadata for entries.

#Permission Categories
#u    User
#g    Group
#o    Other
#a    All

#display a user's groups
groups
#or 
id -Gn


```

![](../../.gitbook/assets/image%20%282%29.png)

```text
#change permission
#chmod        change mode command
#ugoa         user, group, other, all
+-=           Add, subtract, or set permissions
rwx           Read, Write, Execute

#example
chmod u=rwx,g=rx,o=     filename

```

```text
#Numeric Based Permissions
#  r        w         x
#  0        0         0    value for off
#  1        1         1    binary value for on 
#  4        2         1    base 10 value for on

#example
chmod u=7,g=5,o=0    filename

#Symbolic       Octal
-rwx------      700
-rwxr-xr-x      755
-rw-rw-r--      664
-rw-rw----      660
-rw-r--r--      644

```

