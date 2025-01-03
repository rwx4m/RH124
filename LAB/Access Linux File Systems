```markdown
# Lab: Access Linux File Systems

In this lab, you will learn how to mount a local file system and locate specific files within that file system.

## Outcomes
- Mount a file system.
- Generate a disk usage report.
- Locate files in the local file system.

### Preparation

```bash
[student@workstation ~]$ lab start fs-review
```

---

### Instructions

#### 1. Mount a File System by UUID
- **Step 1**: Log in to the `serverb` machine as the `student` user and switch to the `root` user:
  ```bash
  [student@workstation ~]$ ssh student@serverb
  [student@serverb ~]$ sudo -i
  ```

- **Step 2**: Query the UUID of the `/dev/vdb1` device:
  ```bash
  [root@serverb ~]# lsblk -fp /dev/vdb
  ```

- **Step 3**: Create the `/mnt/freespace` directory:
  ```bash
  [root@serverb ~]# mkdir /mnt/freespace
  ```

- **Step 4**: Mount the `/dev/vdb1` device by UUID:
  ```bash
  [root@serverb ~]# mount UUID="44bfb7c8-970c-4d0b-b53d-90ae31cb27ca" /mnt/freespace
  ```

- **Step 5**: Verify the mount:
  ```bash
  [root@serverb ~]# lsblk -fp /dev/vdb1
  ```

---

#### 2. Generate a Disk Usage Report
Generate a disk usage report for the `/usr/share` directory and save it to `/mnt/freespace/results.txt`:
```bash
[root@serverb ~]# du /usr/share > /mnt/freespace/results.txt
```

---

#### 3. Locate Files by Name
- **Update the locate database**:
  ```bash
  [root@serverb ~]# updatedb
  ```

- **Find files matching `rsyslog.conf` and save the results**:
  ```bash
  [root@serverb ~]# locate rsyslog.conf > /mnt/freespace/search1.txt
  ```

---

#### 4. Find Files by Size
Find files in `/usr/share` that are greater than 50 MB and less than 100 MB, and save the results to `/mnt/freespace/search2.txt`:
```bash
[root@serverb ~]# find /usr/share -size +50M -size -100M > /mnt/freespace/search2.txt
```

---

#### 5. Return to Workstation
Exit the `serverb` machine:
```bash
[root@serverb ~]# exit
[student@serverb ~]$ exit
```

---

### Evaluation
Grade your work and correct any reported issues:
```bash
[student@workstation ~]$ lab grade fs-review
```

---

### Finish
Complete the lab exercise:
```bash
[student@workstation ~]$ lab finish fs-review
```
