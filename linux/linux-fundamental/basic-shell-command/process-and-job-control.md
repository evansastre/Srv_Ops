# Process and Job Control

## Background and Foreground Processes

```text
command &    # Start command in background
Ctrl-c                #Kill the foreground process
Ctrl-z                #Suspend the foreground process

bg [%num]  #Background a suspended process.
fg [%num]  #Foreground a background process.
kill       #Kill a process by job number or PID.
jobs  [%num]  #List jobs.
jobs %+   #current job
jobs %-   #previous job

#Killing Processes
Ctrl-c #Kills the foreground proc.
kill [-sig] pid #Send a signal to a process.
kill -l #Display a list of signals.
kill 123
kill -15 123 #kill -TERM 123 , default
kill -9 123
```





