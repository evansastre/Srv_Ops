# Cron

```text
Crontab Format

* * * * * command
| | | | |
| | | | +-- Day of the Week (0-6)
| | | +---- Month of the Year (1-12)
| | +------ Day of the Month (1-31)
| +-------- Hour (0-23)
+---------- Minute (0-59)

# Run every Monday at 07:00.
0 7 * * 1 /opt/sales/bin/weekly-report
| | | | |
| | | | +-- Day of the Week (0-6)
| | | +---- Month of the Year (1-12)
| | +------ Day of the Month (1-31)
| +-------- Hour (0-23)
+---------- Minute (0-59)
```

## Redirecting Output

```text
# Run at 02:00 every day and
# send output to a log file.
0 2 * * * /root/backupdb > /tmp/db.log 2>&1
```

## Examples

```text
# Run every 30 minutes.
0,30 * * * * /opt/acme/bin/half-hour-check
# Another way to do the same thing.
*/2 * * * * /opt/acme/bin/half-hour-check
# Run for the first 5 minutes of the hour
0-4 * * * * /opt/acme/bin/first-five-mins
```

## Crontab Shortcuts

```text
@yearly    0 0 1 1 *
@annually  0 0 1 1 *
@monthly   0 0 1 * *
@weekly    0 0 * * 0
@daily     0 0 * * *
@midnight  0 0 * * *
@hourly    0 * * * *
```

## Using the Crontab Command

```text
crontab file  #Install a new crontab from file.
crontab -l    #List your cron jobs.
crontab -e    #Edit your cron jobs.
crontab -r    #Remove all of your cron jobs.
```



查看某个用户的crontab入口

```text
$ crontab -u john -l
```

设置一个每十分钟执行一次的计划任务

```text
*/10 * * * * /home/ramesh/check-disk-space
```

更多示例：[Linux Crontab: 15 Awesome Cron Job Examples](http://www.thegeekstuff.com/2009/06/15-practical-crontab-examples/)









