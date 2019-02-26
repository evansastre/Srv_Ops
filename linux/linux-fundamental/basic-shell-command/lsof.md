# lsof

查看某个文件被哪些进程在读写

[lsof](https://www.baidu.com/s?wd=lsof&tn=24004469_oem_dg&rsv_dl=gh_pl_sl_csd)是什么意思

list open files

查看某个文件被哪些进程在读写

lsof 文件名  
  
查看某个进程打开了哪些文件  
lsof –c 进程名  
lsof –p 进程号  
  
lsof用法小全  
lsof abc.txt 显示开启文件abc.txt的进程  
lsof -i :22 知道22端口现在运行什么程序  
lsof -c nsd 显示nsd进程现在打开的文件  
lsof -g gid 显示归属gid的进程情况  
lsof +d /usr/local/ 显示目录下被进程开启的文件  
lsof +D /usr/local/ 同上，但是会搜索目录下的目录，时间较长  
lsof -d 4 显示使用[fd](https://www.baidu.com/s?wd=fd&tn=24004469_oem_dg&rsv_dl=gh_pl_sl_csd)为4的进程  
lsof -i \[i\] 用以显示符合条件的进程情况

