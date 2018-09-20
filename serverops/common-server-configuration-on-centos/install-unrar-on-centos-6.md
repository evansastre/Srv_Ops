# Install unrar on CentOS 6

```bash
cd /tmp
wget http://www.rarlab.com/rar/rarlinux-x64-5.3.b4.tar.gz
tar -zxvf rarlinux-x64-5.3.b4.tar.gz

#Both rar and unrar command are located in rar sub-directory. Just do cd to rar directory, type:
cd rar 
./unrar

#copy rar and unrar file to /usr/local/bin directory

sudo cp rar unrar /usr/bin
#To extract file with full path:

unrar x file.rar
```

