# Lab: Access the Command Line

In this lab, you will use the Bash shell to execute commands.

As the `student` user on the workstation machine, use the `lab` command to prepare your system for this exercise. This ensures that all required resources are available.  
```bash
[student@workstation ~]$ lab start cli-review
```

---

## Instructions

### 1. Display the Current Time and Date
Use the `date` command to display the current time and date.
```bash
[student@workstation ~]$ date
Mon Feb 28 01:57:25 PM PDT 2022
```

### 2. Display Time in 24-Hour Format
Use the `+%R` argument with the `date` command to display the current time in 24-hour clock time.
```bash
[student@workstation ~]$ date +%R
13:58
```

### 3. Determine File Type
Check the file type of `/home/student/zcat` to see if it is readable by humans using the `file` command.
```bash
[student@workstation ~]$ file zcat
zcat: a /usr/bin/sh script, ASCII text executable
```

### 4. Display File Size
Use the `wc` command to display the number of lines, words, and bytes in the `zcat` file. Use the Bash shortcut `Esc+. ` to reuse the file name from the previous command.
```bash
[student@workstation ~]$ wc Esc+.
[student@workstation ~]$ wc zcat
  51  299 1988 zcat
```

### 5. Display First 10 Lines of a File
Use the `head` command to display the first 10 lines of the `zcat` file. Try the `Esc+.` shortcut again.
```bash
[student@workstation ~]$ head Esc+.
[student@workstation ~]$ head zcat
#!/bin/sh
# Uncompress files to standard output.
...
```

### 6. Display Last 10 Lines of a File
Use the `tail` command to display the last 10 lines of the `zcat` file.
```bash
[student@workstation ~]$ tail Esc+.
[student@workstation ~]$ tail zcat
...
exec gzip -cd "$@"
```

### 7. Repeat Commands Efficiently
Repeat the previous command with four or fewer keystrokes using either:
- The `UpArrow` key to scroll back through the command history.
- The `!!` shortcut to rerun the last command.
```bash
[student@workstation ~]$ !!
tail zcat
...
```

### 8. Display Last 20 Lines of a File
Use the `tail -n 20` option to display the last 20 lines in the file. Edit the previous command with minimal keystrokes using `Ctrl+A` to move to the beginning of the line and `Ctrl+RightArrow` to jump words.
```bash
[student@workstation ~]$ tail -n 20 zcat
...
```

### 9. Run a Command from History
Use the `history` command to find the desired `date +%R` command, then run it using `!number`.
```bash
[student@workstation ~]$ history
1   date
2   date +%R
3   file zcat
...
[student@workstation ~]$ !2
date +%R
14:02
```

---

## Evaluation
Use the `lab grade` command to grade your work. Correct any reported failures and rerun the command until successful.
```bash
[student@workstation ~]$ lab grade cli-review
```

---

## Finish
After completing the lab, return to the home directory and use the `lab finish` command to ensure resources from this exercise do not impact upcoming exercises.
```bash
[student@workstation ~]$ lab finish cli-review
```
