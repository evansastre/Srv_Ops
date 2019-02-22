# Screen



### Starting screen

To start `screen`, enter the following command:

```text
 screen
```



### General commands

**Note:** Every `screen` command begins with `Ctrl-a`.

| `Ctrl-a c` | Create new window \([shell](https://kb.iu.edu/d/agvf)\) |
| :--- | :--- |
| `Ctrl-a k` | Kill the current window |
| `Ctrl-a w` | List all windows \(the current window is marked with "\*"\) |
| `Ctrl-a 0-9` | Go to a window numbered 0-9 |
| `Ctrl-a n` | Go to the next window |
| `Ctrl-a` `Ctrl-a` | Toggle between the current and previous window |
| `Ctrl-a [` | Start copy mode |
| `Ctrl-a ]` | Paste copied text |
| `Ctrl-a ?` | Help \(display a list of commands\) |
| `Ctrl-a` `Ctrl-\` | Quit `screen` |
| `Ctrl-a D` \(Shift-d\) | Power detach and logout |
| `Ctrl-a d` | Detach but keep shell window open |



#### To copy a block

To get into copy mode, press `Ctrl-a [` .

To move the cursor, press the `h`, `j`, `k`, and `l` \(the letter l\) keys. The `0` \(the number 0\) or `^` \(the caret\) moves to the start of the line and `$` \(the dollar sign\) moves to the end of the line. `Ctrl-b` scrolls the cursor back one page and `Ctrl-f` scrolls forward one page. To set the left and right margins of copy, press `c` and `C` \(Shift-c\). The Spacebar starts selecting the text and ends selecting the text. To abort copy mode, press `Ctrl-g`.

#### To paste a block

To paste the copied text to the current window \(as many times as you want\), press `Ctrl-a ]`.

