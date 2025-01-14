# Lab: Monitor and Manage Linux Processes

In this lab, you locate and manage processes that use the most resources on a system.

On workstation, run the lab start processes-review command. The command runs a start script to determine whether the serverb host is reachable on the network.
```bash
[student@workstation ~]$ lab start processes-review
```
---
### Instructions
On workstation, open two terminal windows side by side. In this section, these terminals are referred to as left and right. On each terminal window, log in to serverb as the student user.
Create the process101 script in the */home/student/bin directory*. The process101 script generates artificial CPU load.
```bash
#!/bin/bash
while true; do
  var=1
  while [[ var -lt 50000 ]]; do
    var=$(($var+1))
  done
  sleep 1
done
```
On workstation, open two terminal windows side by side. In each terminal, use the ssh command to log in to the serverb machine as the student user.
```bash
[student@workstation ~]$ ssh student@serverb
...output omitted...
[student@serverb ~]$
```
In the left terminal shell, create the /home/student/bin directory.
```
[student@serverb ~]$ mkdir /home/student/bin
```
In the left terminal shell, create the process101 script. Press the i key to enter the Vim interactive mode. Type :wq to save the file.
```
[student@serverb ~]$ vim /home/student/bin/process101
```
```bash
#!/bin/bash
while true; do
  var=1
  while [[ var -lt 50000 ]]; do
    var=$(($var+1))
  done
  sleep 1
done
```
Make the process101 script executable.
```
[student@serverb ~]$ chmod +x /home/student/bin/process101
```
In the right terminal shell, run the top utility.
Size the window to be as tall as possible.
```bash
[student@serverb ~]$ top
top - 17:02:43 up 42 min,  2 users,  load average: 0.00, 0.00, 0.00
Tasks: 120 total,   1 running, 119 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.0 sy,  0.0 ni,100.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
MiB Mem :   1774.8 total,   1420.7 free,    206.3 used,    147.8 buff/cache
MiB Swap:      0.0 total,      0.0 free,      0.0 used.   1417.3 avail Mem

 PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
   1 root      20   0  105972  17592  10292 S   0.0   1.0   0:01.30 systemd
   2 root      20   0       0      0      0 S   0.0   0.0   0:00.00 kthreadd
   3 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 rcu_gp
   4 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 rcu_par_gp
   6 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/0:0H-event+
...output omitted...
```
In the left terminal shell, verify the number of logical CPUs on the virtual machine. Run the process101 script in the background.
Verify the number of logical CPUs.
```bash
[student@serverb ~]$ grep "model name" /proc/cpuinfo | wc -l
2
```
Change to the >/home/student/bin directory. Run the process101 script in the background.
```bash
[student@serverb ~]$ cd /home/student/bin

[student@serverb bin]$ process101 &
[1] 1161
```
In the right terminal shell, observe the top display. Note the process ID (PID), and view the CPU percentage that the process101 process uses. The CPU percentage that the process uses should hover around 10% to 15%. Toggle the top utility display between load, threads, and memory. Return to the CPU usage display of the top utility.
>Press Shift+m.
```bash
top - 17:11:24 up 51 min,  2 users,  load average: 0.16, 0.07, 0.02
Tasks: 118 total,   1 running, 117 sleeping,   0 stopped,   0 zombie
%Cpu(s):  7.8 us,  0.7 sy,  0.0 ni, 91.2 id,  0.0 wa,  0.2 hi,  0.2 si,  0.0 st
MiB Mem :   1774.8 total,   1419.5 free,    207.4 used,    147.9 buff/cache
MiB Swap:      0.0 total,      0.0 free,      0.0 used.   1416.2 avail Mem

 PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
 761 root      20   0  340412  41416  17888 S   0.0   2.3   0:00.44 firewalld
 780 root      20   0  474344  30704  13508 S   0.0   1.7   0:00.62 tuned
 736 polkitd   20   0 2577132  24592  18320 S   0.0   1.4   0:00.07 polkitd
 767 root      20   0  471864  18992  16416 S   0.0   1.0   0:00.15 NetworkManager
   1 root      20   0  105972  17592  10292 S   0.0   1.0   0:01.30 systemd
...output omitted...
1161 student   20   0  222652   3888   3432 S  12.3   0.2   0:54.81 process101
...output omitted...
```
>NOTE:
When the top utility switches into memory mode, the process101 process is no longer the first process. You can press Shift+p to return to CPU usage.
Press m to display more memory details.
```
top - 17:16:14 up 56 min,  2 users,  load average: 0.20, 0.12, 0.04
Tasks: 118 total,   1 running, 117 sleeping,   0 stopped,   0 zombie
%Cpu(s):  7.5 us,  0.8 sy,  0.0 ni, 91.5 id,  0.0 wa,  0.2 hi,  0.0 si,  0.0 st
MiB Mem : 19.9/1774.8   [||||||||||                                           ]
MiB Swap:  0.0/0.0      [                                                     ]


 PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
 761 root      20   0  340412  41416  17888 S   0.0   2.3   0:00.44 firewalld
 780 root      20   0  474344  30704  13508 S   0.0   1.7   0:00.66 tuned
 736 polkitd   20   0 2577132  24592  18320 S   0.0   1.4   0:00.07 polkitd
 767 root      20   0  471864  18992  16416 S   0.0   1.0   0:00.15 NetworkManager
   1 root      20   0  105972  17592  10292 S   0.0   1.0   0:01.30 systemd
1068 student   20   0   21652  13144  10128 S   0.0   0.7   0:00.08 systemd
1114 root      20   0   19332  11928   9648 S   0.0   0.7   0:00.02 sshd
...output omitted...
1161 student   20   0  222652   3888   3432 S  11.0   0.2   1:35.17 process101
...output omitted...
```
>Press t.
```
top - 17:21:43 up  1:01,  2 users,  load average: 0.23, 0.18, 0.09
Tasks: 121 total,   1 running, 120 sleeping,   0 stopped,   0 zombie
%Cpu(s):   7.5/1.0     8[|||||                                                ]
MiB Mem : 20.1/1774.8   [||||||||||||                                         ]
MiB Swap:  0.0/0.0      [                                                     ]

 PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
 761 root      20   0  340412  41416  17888 S   0.0   2.3   0:00.44 firewalld
 780 root      20   0  474344  30704  13508 S   0.0   1.7   0:00.70 tuned
 736 polkitd   20   0 2577132  24592  18320 S   0.0   1.4   0:00.07 polkitd
 767 root      20   0  471864  18992  16416 S   0.0   1.0   0:00.17 NetworkManager
   1 root      20   0  105972  17592  10292 S   0.0   1.0   0:01.31 systemd
1068 student   20   0   21652  13144  10128 S   0.0   0.7   0:00.08 systemd
1114 root      20   0   19332  11928   9648 S   0.0   0.7   0:00.02 sshd
 668 root      20   0   33656  11892   8728 S   0.0   0.7   0:00.10 systemd-udevd
1064 root      20   0   19328  11780   9504 S   0.0   0.6   0:00.03 sshd
...output omitted...
1155 student   20   0  225976   4400   3656 R   0.0   0.2   0:01.31 top
...output omitted...
```
>Press Shift+p to switch to CPU usage.
```bash
top - 17:23:33 up  1:03,  2 users,  load average: 0.17, 0.17, 0.09
Tasks: 121 total,   1 running, 120 sleeping,   0 stopped,   0 zombie
%Cpu(s):   7.3/0.8     8[||||||                                               ]
MiB Mem : 20.2/1774.8   [|||||||||||||                                        ]
MiB Swap:  0.0/0.0      [                                                     ]


 PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
1161 student   20   0  222652   3888   3432 S  15.6   0.2   2:09.61 process101
   1 root      20   0  105972  17592  10292 S   0.0   1.0   0:01.31 systemd
...output omitted...
```
Turn off the use of bold in the display. Save this configuration for reuse when top is restarted. Confirm that the changes are saved.
```
Press Shift+b to switch off the use of bold.
top - 17:29:12 up  1:09,  2 users,  load average: 0.17, 0.15, 0.10
Tasks: 117 total,   2 running, 115 sleeping,   0 stopped,   0 zombie
%Cpu(s):   5.6/0.7     6[||||                                                 ]
MiB Mem : 20.4/1774.8   [||||||||||||||                                       ]
MiB Swap:  0.0/0.0      [                                                     ]

 PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
1161 student   20   0  222652   3888   3432 R  12.0   0.2   2:57.18 process101
   1 root      20   0  105972  17592  10292 S   0.0   1.0   0:01.31 systemd
...output omitted...
```
Press *Shift+w* to save this configuration. The default configuration is stored in the toprc file in the /home/student/.config/procps directory. In the left terminal shell, confirm that the toprc file exists.
```
[student@serverb bin]$ ls -l /home/student/.config/procps/toprc
-rw-rw-r--. 1 student student 966 Feb 18 19:45 /home/student/.config/procps/toprc
```
In the right terminal shell, exit top, and then restart it. Confirm that the new display uses the saved configuration.
```bash
top - 17:51:48 up  1:31,  2 users,  load average: 0.09, 0.12, 0.09
Tasks: 119 total,   1 running, 118 sleeping,   0 stopped,   0 zombie
%Cpu(s):   5.0/0.5     5[|||                                                  ]
MiB Mem : 20.0/1774.8   [|||||||||||||                                        ]
MiB Swap:  0.0/0.0      [                                                     ]

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
   1161 student   20   0  222652   3888   3432 S  10.6   0.2   6:08.76 process101
      1 root      20   0  105972  17592  10292 S   0.0   1.0   0:01.33 systemd
...output omitted...
```
Copy the process101 script to a new process102 file, and increase the artificial CPU load to one hundred thousand in the new script. Start the process102 process in the background.
In the left terminal shell, copy process101 to process102.
```
[student@serverb bin]$ cp process101 process102
```
Edit the process102 script and increase the addition calculations from fifty thousand to one hundred thousand. Enter interactive mode by using i. Type :wq to save the file and quit.
```
[student@serverb bin]$ vim process102
```
```bash
#!/bin/bash
while true; do
  var=1
    while [[ var -lt 100000 ]]; do
      var=$(($var+1))
  done
  sleep 1
done
```
Start the process102 process in the background.
```bash
[student@serverb bin]$ process102 &
[2] 4023
```
Verify that both processes are running in the background.
```bash
[student@serverb bin]$ jobs
[1]-  Running                 process101 &
[2]+  Running                 process102 &
```
In the right terminal shell, verify that the process is running and uses the most CPU resources. The load should hover between 25% to 35%.
In the right terminal shell, verify that the process is running. The load should hover between 25% to 35%.
```bash
top - 18:04:54 up  1:44,  2 users,  load average: 0.37, 0.24, 0.13
Tasks: 120 total,   1 running, 119 sleeping,   0 stopped,   0 zombie
%Cpu(s): 18.1 us,  2.0 sy,  0.0 ni, 79.7 id,  0.0 wa,  0.2 hi,  0.0 si,  0.0 st
MiB Mem :   1774.8 total,   1374.3 free,    210.1 used,    190.4 buff/cache
MiB Swap:      0.0 total,      0.0 free,      0.0 used.   1410.7 avail Mem

 PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
4023 student   20   0  222652   3980   3524 S  22.3   0.2   0:32.94 process102
1161 student   20   0  222652   3888   3432 S  17.7   0.2   7:59.52 process101
   1 root      20   0  105972  17592  10292 S   0.0   1.0   0:01.33 systemd
...output omitted...
```
>NOTE
If you do not see the process101 and process102 processes at the top of the process list, then press Shift+p to ensure that the top utility sorts the output by CPU usage.
Notice that the load average is below 1. Copy the process101 script to a new script called process103. Increase the addition count to eight hundred thousand. Start process103 in the background. Confirm that the load average is above 1. It might take a few minutes for the load average to change.

In the right terminal shell, verify that the load average is below 1.
```bash
top - 18:12:49 up  1:52,  2 users,  load average: 0.45, 0.38, 0.24
...output omitted...
```
In the left terminal shell, copy process101 to a new process103 script.
```
[student@serverb bin]$ cp process101 process103
```
In the left terminal shell, edit the process103 script. Increase the addition count to eight hundred thousand. Enter interactive mode with the i key. Type :wq to save the file and quit.
```
[student@serverb bin]$ vim process103
```
```bash
#!/bin/bash
while true; do
  var=1
    while [[ var -lt 800000 ]]; do
      var=$(($var+1))
    done
    sleep 1
done
```
Start the process103 process in the background. The CPU usage hovers between 60% to 85%.
```bash
[student@serverb bin]$ process103 &
[3] 5172
```
Verify that all three jobs are running in the background.
```bash
[student@serverb bin]$ jobs
[1]   Running                 process101 &
[2]-  Running                 process102 &
[3]+  Running                 process103 &
```
In the right terminal shell, verify that the load average is above 1. It might take a few minutes for the load to increase.
```bash
top - 18:16:07 up  1:56,  2 users,  load average: 1.11, 0.77, 0.45
...output omitted...
```
In the left terminal shell, switch to the root user. Suspend the process101 process. List the remaining jobs. Observe that the process state for process101 is now in the T state.
Switch to the root user.
```bash
[student@serverb bin]$ su -
Password: redhat
```
Suspend the process101 process.
```bash
[root@serverb ~]# pkill -SIGSTOP process101
```
In the right terminal shell, confirm that the process101 process is no longer running.
```bash
top - 18:19:17 up  1:59,  2 users,  load average: 0.92, 0.83, 0.50
Tasks: 123 total,   3 running, 118 sleeping,   1 stopped,   1 zombie
%Cpu(s): 42.9 us,  4.0 sy,  0.0 ni, 52.8 id,  0.0 wa,  0.3 hi,  0.0 si,  0.0 st
MiB Mem :   1774.8 total,   1368.4 free,    215.5 used,    190.8 buff/cache
MiB Swap:      0.0 total,      0.0 free,      0.0 used.   1405.2 avail Mem

 PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
5172 student   20   0  222652   3900   3448 R  66.4   0.2   3:25.81 process103
4023 student   20   0  222652   3980   3524 R  26.9   0.2   4:07.89 process102
   1 root      20   0  105972  17592  10292 S   0.0   1.0   0:01.34 systemd
   2 root      20   0       0      0      0 S   0.0   0.0   0:00.00 kthreadd
...output omitted...
```
In the left terminal shell, view the remaining jobs.
```bash
[root@serverb ~]# ps jT
...output omitted...
PPID PID  PGID  SID  TTY    TPGID STAT UID   TIME COMMAND
1117 1118 1118  1118 pts/1  5778  Ss   1000   0:00 -bash
1118 1161 1161  1118 pts/1  5778  T    1000  10:00 /bin/bash /home/student/bin/process101
1118 4023 4023  1118 pts/1  5778  S    1000   4:19 /bin/bash /home/student/bin/process102
1118 5172 5172  1118 pts/1  5778  S    1000   3:59 /bin/bash /home/student/bin/process103
...output omitted...
```
>Note that process101 has a status of T. It means that the process is currently suspended.

Resume the process101 process.

In the left terminal shell, resume the process101 process.
```bash
[root@serverb ~]# pkill -SIGCONT process101
```
In the right terminal shell, verify that the process is running again.
```bash
top - 18:24:18 up  2:04,  2 users,  load average: 1.06, 0.96, 0.65
Tasks: 125 total,   2 running, 123 sleeping,   0 stopped,   0 zombie
%Cpu(s): 48.3 us,  4.3 sy,  0.0 ni, 47.2 id,  0.0 wa,  0.2 hi,  0.0 si,  0.0 st
MiB Mem :   1774.8 total,   1368.6 free,    215.2 used,    191.0 buff/cache
MiB Swap:      0.0 total,      0.0 free,      0.0 used.   1405.5 avail Mem

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
   5172 student   20   0  222652   3900   3448 R  72.0   0.2   7:02.30 process103
   4023 student   20   0  222652   3980   3524 S  22.0   0.2   5:23.52 process102
   1161 student   20   0  222652   3888   3432 S  11.0   0.2  10:00.92 process101
...output omitted...
```
Terminate process101, process102, and process103 from the command line. Verify that the processes are no longer displayed in top.
In the left terminal shell, terminate process101, process102, and process103.
```
[root@serverb ~]# pkill process101
[root@serverb ~]# pkill process102
[root@serverb ~]# pkill process103
```
In the right terminal shell, verify that the processes no longer appear in top.
```bash
top - 18:25:12 up  2:05,  2 users,  load average: 0.93, 0.95, 0.67
Tasks: 117 total,   1 running, 116 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.2 us,  0.0 sy,  0.0 ni, 99.8 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
MiB Mem :   1774.8 total,   1369.8 free,    214.0 used,    191.0 buff/cache
MiB Swap:      0.0 total,      0.0 free,      0.0 used.   1406.7 avail Mem

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
    767 root      20   0  471864  18992  16416 S   0.3   1.0   0:00.26 NetworkManager
      1 root      20   0  105972  17592  10292 S   0.0   1.0   0:01.34 systemd
      2 root      20   0       0      0      0 S   0.0   0.0   0:00.00 kthreadd
      3 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 rcu_gp
...output omitted...
```
Stop the processes and return to the workstation machine.
Log out from the root user and close the terminal.
```bash
[root@serverb ~]# exit
logout
[1]   Terminated              process101
[2]   Terminated              process102
[3]-  Terminated              process103
```
In the right terminal shell, press q to quit top. Return to the workstation system as the student user.
```bash
[student@serverb ~]$ exit
logout
Connection to serverb closed.
[student@workstation ~]$
```
### Evaluation
As the student user on the workstation machine, use the lab command to grade your work. Correct any reported failures and rerun the command until successful.
```
[student@workstation ~]$ lab grade processes-review
Finish
```
On the workstation machine, change to the student user home directory and use the lab command to complete this exercise. This step is important to ensure that resources from previous exercises do not impact upcoming exercises.
```
[student@workstation ~]$ lab finish processes-review
```
