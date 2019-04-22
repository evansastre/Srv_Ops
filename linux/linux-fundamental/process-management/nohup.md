# nohup

```text
# Run the command without hanging up. 
# This command can continue to run the corresponding process after you log out of the account / close the terminal.

# nohup Command [ Arg ... ] [　& ]
```

The nohup command runs the command specified by the Command parameter and any associated Arg parameters, ignoring all hang up \(SIGHUP\) signals. Run the program in the background with the nohup command after logging out. To run the nohup command in the background, add & \(the symbol for "and"\) to the end of the command. Whether or not the output of the nohup command is reset to the terminal, the output is appended to the nohup.out file in the current directory. If the current directory's nohup.out file is not writable, the output is reset to the $HOME/nohup.out file. If no files can be created or opened for appending, the command specified by the Command parameter is not callable. If the standard error is a terminal, then the output of the specified command to the standard error is reset as the standard output to the same file descriptor.

Exit Status: This command returns the following exit values: 

126 You can find but not call the command specified by the Command parameter. 127 The nohup command has an error or cannot find the command specified by the Command parameter. 

Otherwise, the exit status of the nohup command is the exit status of the command specified by the Command parameter.

If the job is submitted using the nohup command, by default all output from the job is reset to a file named nohup.out unless an output file is specified otherwise: nohup command &gt; myout.file 2&gt;&1 

& In the above example, the output is reset to the myout.file file.

```text
#We have a test.php that needs to run in the background, 
#and we want to run regularly in the background, then use nohup:
nohup /root/test.php &
(nohup sh make.sh &)
```





