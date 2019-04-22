# history - shell history and Tab cpmpletion

## Path for store history file

```text
~/.bash_history
~/.history
~/.histfile
```

## history command

```text
history   #Displays the shell history
histsize  #controls the number of commands to retain in history
export HISTSIZE=1000   #defualt 500

!N  #Repeat command line number N
!!  #Repeat the previous command line
!string  #Repeat the most recent command starting with "string"

!:N <Event> <Sepatator> <Word>
!  #Represents a command line(or event) 
   #!=The most recent command line.
   #!=!!
:N  #Represent a word on the command line 
  0 = command, 1 = first atgument,etc
  
#Example
$head files.txt sorted_files.txt notes.txt
<Output from head command here>
$!!
head files.txt sorted_files.txt notes.txt
<Output from head command here>
$vi !:2
vi sorted_files.txt
<vi editor starts>

!^   #Represents the first atgument.
      1^ = !:1
!$   #Represents the last argument.

$head files.txt sorted_files.txt notes.txt
!^ = files.txt
!$ = notes.txt

```

## Searching shell history

```text
Ctrl-r #Reverse shell history search
Enter  #Execute the command
Arrows #Change the command
Ctrl-g #Cancel the search

```

## Tab Completion

Tab autocompletion

* Commands
* Files, directories, paths
* Environment Variables
* Usernames\(~\)



