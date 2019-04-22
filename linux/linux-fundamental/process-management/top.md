# top

## top

top命令会显示当前系统中占用资源最多的一些进程（默认以CPU占用率排序）如果你想改变排序方式，可以在结果列表中点击O（大写字母O）会显示所有可用于排序的列，这个时候你就可以选择你想排序的列

```text
Current Sort Field:  P  for window 1:Def
Select sort field via field letter, type any other key to return

  a: PID        = Process Id              v: nDRT       = Dirty Pages count
  d: UID        = User Id                 y: WCHAN      = Sleeping in Function
  e: USER       = User Name               z: Flags      = Task Flags
  ........
```

如果只想显示某个特定用户的进程，可以使用-u选项

```text
$ top -u oracle
```

更多示例：[Can You Top This? 15 Practical Linux Top Command Examples](http://www.thegeekstuff.com/2010/01/15-practical-unix-linux-top-command-examples/)

## htop

A strong tool similart to top

## pstree

```text
yum install psmisc -y
pstree 
pstree  -up     #show all tree

```

## iotop

show interactive io - disk

## iftop

show interactive if - network

