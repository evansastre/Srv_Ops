# Centos6.\* upgrade glibc

**situation** libc.so.6: version GLIBC\_2.14 not found

**show version** 

```bash
strings /lib64/libc.so.6 |grep GLIBC_ 
ll /lib64/libc**
```

we can see

{% hint style="info" %}
"/lib64/libc.so.6 -&gt; /lib64/libc-2.12.so"
{% endhint %}

**Install** 

download [glibc-2.14](url) [http://ftp.gnu.org/gnu/glibc/glibc-2.14.tar.gz](http://ftp.gnu.org/gnu/glibc/glibc-2.14.tar.gz) 

```bash
cd /tmp 
wget http://ftp.gnu.org/gnu/glibc/glibc-2.14.tar.gz
#extract 
tar -xzvf glibc-2.14.tar.gz
#install
cd glibc-2.14
mkdir build # build folder "build" under "glibc-2.14
cd build 
../configure --prefix=/opt/glibc-2.14 #config glibc and set glibc-2.14 install path 
make && make install #make install glibc-2.14
#re-build glibc link  
rm -rf /lib64/libc.so.6 #delete libc.so.6 first
ln -s /opt/glibc-2.14/lib/libc-2.14.so /lib64/libc.so.6
```

**mention** 

```bash
#Delete libc.so.6 may cause system command unstable, we can use below to fix it: 
LD_PRELOAD=/opt/glibc-2.14/lib/libc-2.14.so ln -s /opt/glibc-2.14/lib/libc-2.14.so /lib64/libc.so.6
#Or if that way fail, we can roll back: 
LD_PRELOAD=/lib64/libc-2.12.so ln -s /lib64/libc-2.12.so /lib64/libc.so.6
```



