### Lab: Control Access to Files  
In this lab, you will configure file permissions and set up a shared directory that allows collaborative file management for a specific group.  

---

### Outcomes  
1. Create a directory for group collaboration.  
2. Automatically assign group ownership to created files.  
3. Restrict access to files outside the group.  

### Preparation  
Log in to the workstation as the **student** user. Use the following command to set up your environment:  
```bash
[student@workstation ~]$ lab start perms-review
```

---

### Instructions  

#### 1. Access the server  
Log in to `serverb` as the **student** user and escalate privileges to root:  
```bash
[student@workstation ~]$ ssh student@serverb
...output omitted...
[student@serverb ~]$ sudo -i
[sudo] password for student: student
[root@serverb ~]#
```

#### 2. Create the shared directory  
Use the `mkdir` command to create the `/home/techdocs` directory:  
```bash
[root@serverb ~]# mkdir /home/techdocs
```

#### 3. Set group ownership  
Assign the `techdocs` group as the owner of the directory:  
```bash
[root@serverb ~]# chown :techdocs /home/techdocs
```

#### 4. Test file creation  
Switch to the **tech1** user and try creating a file. This step should fail as the group lacks write permissions:  
```bash
[root@serverb ~]# su - tech1
[tech1@serverb ~]$ touch /home/techdocs/techdoc1.txt
touch: cannot touch '/home/techdocs/techdoc1.txt': Permission denied
[tech1@serverb ~]$ ls -ld /home/techdocs/
drwxr-xr-x. 2 root techdocs 6 Feb  5 16:05 /home/techdocs/
```

#### 5. Adjust directory permissions  
Set permissions to allow group members to create and edit files:  
```bash
[root@serverb ~]$ chmod 2770 /home/techdocs
[root@serverb ~]$ ls -ld /home/techdocs
drwxrws---. 2 root techdocs 6 Feb 4 18:12 /home/techdocs/
```

#### 6. Verify group access  
Switch between group users to confirm they can create files while others cannot.  

- **tech1 user:**  
```bash
[root@serverb ~]# su - tech1
[tech1@serverb ~]$ touch /home/techdocs/techdoc1.txt
[tech1@serverb ~]$ echo "This is the first tech doc." > /home/techdocs/techdoc1.txt
[tech1@serverb ~]$ exit
```

- **tech2 user:**  
```bash
[root@serverb ~]# su - tech2
[tech2@serverb ~]$ cat /home/techdocs/techdoc1.txt
This is the first tech doc.
[tech2@serverb ~]$ touch /home/techdocs/techdoc2.txt
[tech2@serverb ~]$ exit
```

- **database1 user:**  
```bash
[root@serverb ~]# su - database1
[database1@serverb ~]$ cat /home/techdocs/techdoc1.txt
cat: /home/techdocs/techdoc1.txt: Permission denied
[database1@serverb ~]$ exit
```

#### 7. Update the default `umask`  
Modify `/etc/login.defs` to set the global `umask` to `007`:  
```bash
[root@serverb ~]# vi /etc/login.defs
...output omitted...
UMASK           007
...output omitted...
```
Verify the change:  
```bash
[root@serverb ~]# su - student
[student@serverb ~]$ umask
0007
[student@serverb ~]$ exit
```

---

### Evaluation  
Use the lab grading command to check your work and address any failures:  
```bash
[student@workstation ~]$ lab grade perms-review
```

Complete the lab to clean up resources:  
```bash
[student@workstation ~]$ lab finish perms-review
```
