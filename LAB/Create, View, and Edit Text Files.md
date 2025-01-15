# Lab: Create, View, and Edit Text Files

In this lab you edit a text file with the vim editor.
As the student user on the workstation machine, use the lab command to prepare your system for this exercise.

This command prepares your environment and ensures that all required resources are available.

```
[student@workstation ~]$ lab start edit-review
```

---
## Instructions
1. On workstation, create the lab_file shell variable and assign `editing_final_lab.txt` as the value. List the student home directory, including hidden directories and files, and redirect the output to the `editing_final_lab.txt` file by using the shell variable.

   On the workstation machine, create the `lab_file` shell variable and assign a value of `editing_final_lab.txt`.
   
   Use the `ls -al` command in the student home directory and redirect the output to the `editing_final_lab.txt` file.

```
[student@workstation ~]$ lab_file=editing_final_lab.txt
[student@workstation ~]$ ls -al > $lab_file
```

2. Use Vim to edit the `editing_final_lab.txt` file. Use the `lab_file` shell variable.
```[student@workstation ~]$ vim $lab_file```

3. Enter the line-based visual mode of Vim. Your screen output might differ from these examples. Remove the first three lines of the `editing_final_lab.txt` file.

4. Use the arrow keys to position the cursor at the first character in the first line. Enter the line-based visual mode with `Shift+V`. Move down by using the down arrow key twice to select the first three lines. Delete the lines by typing `x`.

5. Enter the visual mode of `Vim`. Remove the last seven characters from the first column on the first line. Preserve only the first four characters of the first column.

   Use the arrow keys to position the cursor at the last character of the first column on the first line. Delete the selection by typing `x`.

   Use the arrow keys to position the cursor at the fifth character of the first column on the first line. Enter the visual mode by typing `v`.

6. Enter the visual block mode of `Vim`. Repeat the operation of the previous step, but this time select from the second to the last line. Preserve only the first four characters of the first column.

7. Use the arrow keys to position the cursor at the fifth character of the second line. Enter the visual mode by using the Ctrl+V control sequence.Use the arrow keys to position the cursor at the last character of the first column on the last line. Delete the selection by typing x.

8. Enter the visual block mode of `Vim` and remove the fourth column of the file.

9. Use the arrow keys to position the cursor at the first character of the fourth column. Enter the visual block mode by using `Ctrl+V`. Use the arrow keys to position the cursor at the last character and row of the fourth column. Delete the selection by typing x.

10. Enter the visual block mode of Vim to remove the time column, to leave the month and day columns on all lines.

11. Use the arrow keys to position the cursor at the first character of the current seventh column. Enter the visual block mode by typing Ctrl+V. Use the arrow keys to position the cursor at the last character of the seventh column on the last row. Delete the selection by typing x.

12. Enter the visual line mode of Vim and remove the rows that contain the Desktop and Public strings.

13. Use the arrow keys to position the cursor at any character on the Desktop row. Enter visual mode with uppercase V. The full line is selected. Delete the selection by typing x. Repeat the operation for the row with the Public string.

14. Save your changes and exit the file.

15. To save and exit the file, enter the last-line :wq command.

16. Back up the editing_final_lab.txt file and append the date (in seconds) at the end of the file name preceded with an underscore (_) character. Use the lab_file shell variable.
   
    Use the cp command to back up the editing_final_lab.txt file. Use the $(date ﻿+﻿%s) command at the end of the backup name preceded with an underscore character to make the name unique.

```
[student@workstation ~]$ cp $lab_file \
editing_final_lab_$(date +%s).txt
```

17. Append a dashed line to the editing_final_lab.txt file. The dashed line should contain 12 dash (-) characters for this lab to be graded correctly. Use the lab_file shell variable.
   
    Use the echo command with 12 dashes and append the output to the editing_final_lab.txt file.
    
```[student@workstation ~]$ echo "------------" >> $lab_file```

18. List the content of the Documents directory, and append the output to the editing_final_lab.txt file, and display the output in the terminal. Use the tee command and the lab_file shell variable.

    Use the ls command to list the Documents directory and pipe the output to the tee -a command to append the output to the editing_final_lab.txt file.

```bash
[student@workstation ~]$ ls Documents/ | tee -a $lab_file
lab_review.txt
```

> Confirm that the directory listing is at the bottom of the lab file. Use the lab_file shell variable.

```bash
[student@workstation ~]$ cat $lab_file
drwx  3 student    17 Mar  4  .ansible
-rw-  1 student    18 Nov  5  .bash_logout
-rw-  1 student   141 Nov  5  .bash_profile
-rw-  1 student   492 Nov  5  .bashrc
drwx  9 student  4096 Mar  8  .cache
drwx  8 student  4096 Mar  8  .config
drwx  2 student     6 Mar  8  Documents
drwx  2 student     6 Mar  8  Downloads
-rw-  1 student     0 Mar  8  editing_final_lab.txt
drwx  2 student    25 Mar  4  .grading
drwx  4 student    32 Mar  8  .local
drwx  2 student     6 Mar  8  Music
drwx  2 student     6 Mar  8  Pictures
drwx  2 student    77 Mar  4  .ssh
drwx  2 student     6 Mar  8  Templates
drwx  3 student    18 Mar  4  .venv
drwx  2 student     6 Mar  8  Videos
------------
lab_review.txt
```
## Evaluation
As the student user on the workstation machine, use the lab command to grade your work. Correct any reported failures and rerun the command until successful.
```[student@workstation ~]$ lab grade edit-review```
## Finish
On the workstation machine, change to the student user home directory and use the lab command to complete this exercise.
```[student@workstation ~]$ lab finish edit-review```
This concludes the section.

