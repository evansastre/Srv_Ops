# df

## df

显示文件系统的磁盘使用情况，默认情况下`df -k` 将以字节为单位输出磁盘的使用量

```text
$ df -k
Filesystem           1K-blocks      Used Available Use% Mounted on
/dev/sda1             29530400   3233104  24797232  12% /
/dev/sda2            120367992  50171596  64082060  44% /home
```

使用-h选项可以以更符合阅读习惯的方式显示磁盘使用量

```text
$ df -h
Filesystem                  Size   Used  Avail Capacity  iused      ifree %iused  Mounted on
/dev/disk0s2               232Gi   84Gi  148Gi    37% 21998562   38864868   36%   /
devfs                      187Ki  187Ki    0Bi   100%      648          0  100%   /dev
map -hosts                   0Bi    0Bi    0Bi   100%        0          0  100%   /net
map auto_home                0Bi    0Bi    0Bi   100%        0          0  100%   /home
/dev/disk0s4               466Gi   45Gi  421Gi    10%   112774  440997174    0%   /Volumes/BOOTCAMP
//app@izenesoft.cn/public  2.7Ti  1.3Ti  1.4Ti    48%        0 18446744073709551615    0%   /Volumes/public
```

使用-T选项显示文件系统类型

```text
$ df -T
Filesystem    Type   1K-blocks      Used Available Use% Mounted on
/dev/sda1     ext4    29530400   3233120  24797216  12% /
/dev/sda2     ext4   120367992  50171596  64082060  44% /home
```

