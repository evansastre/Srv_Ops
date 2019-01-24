# File management

```text
#cat    :   show whole content
#head/tail  :   show head or tail of a file
#more/less  : browser  the content, less has more function than more.[Space]down page, [any type]down one line, [Q]quit

#tail -f filename  :   Display the data is writing to the file.
```

```text
####vi
##movement
#k j :  up or down one line,   <5>+<k> move 5line 
#h l :  left or right one charactor
#w b :  right or left one word
#^   :  go to beginning of one line
#$   :  go to end of one line
#gg Go to the first line
#G Go to the last line

#i I : insert current position or begining of line
#80i<Text><Esc>= Insert<Text>80times
#80_<Esc>=Insert"_"80times
#a A : add after current position or ending of line
#o Open a new line below the current line
#O Open a new line above the current line

# :wq or :x   :   save and quit
# :n   :  go to number n line
# :$   :  go to last line

# :set nu    :set nonu    : show line number or not 

#x :  delete a charactor
#dw:  delete one word
#dd:  delete one line
#D:   delete from current position

#r :  replace current charactor
#cw:  change current word
#cc:  change current line
#c$:  change from current position
#C :  same as c$

#~ :  Reverse case of a Charactor, like a->A, A-a

#yy : copy current line
#y3w: copy 3 words
#y$:  copy rest of current line
#p  : paste copied or deleted content 

#u :undo
#Ctrl-R : Redo

#/   : start a forward search
#?   : srart a reverse search
#n   : next 
#N   : previous

```





