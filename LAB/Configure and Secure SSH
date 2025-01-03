In this lab, you will configure and secure SSH access on the server to enhance security by implementing key-based authentication, disabling direct root login, and preventing password-based authentication. Below are the essential steps and outcomes for completing the exercise:

---

### **Steps and Commands**

#### **Step 1: Prepare the Workstation**
1. Use the `lab` command to prepare the environment.
   ```bash
   [student@workstation ~]$ lab start ssh-review
   ```

#### **Step 2: Log in to the Server**
1. Log in to the `servera` machine as the `student` user:
   ```bash
   [student@workstation ~]$ ssh student@servera
   ```

2. Switch to the `production1` user:
   ```bash
   [student@servera ~]$ su - production1
   Password: redhat
   ```

#### **Step 3: Generate SSH Keys**
1. Create a passphrase-less SSH key pair:
   ```bash
   [production1@servera ~]$ ssh-keygen
   ```

#### **Step 4: Configure Key-Based Authentication**
1. Copy the public key to the `serverb` machine:
   ```bash
   [production1@servera ~]$ ssh-copy-id production1@serverb
   Password: redhat
   ```

2. Test the connection using the SSH keys:
   ```bash
   [production1@servera ~]$ ssh production1@serverb
   ```

#### **Step 5: Restrict Root Login**
1. On the `serverb` machine, switch to the root user:
   ```bash
   [production1@serverb ~]$ su -
   Password: redhat
   ```

2. Edit the `/etc/ssh/sshd_config` file to disable root login:
   ```bash
   PermitRootLogin no
   ```

3. Reload the SSH service:
   ```bash
   [root@serverb ~]# systemctl reload sshd.service
   ```

4. Verify that root login is disabled:
   ```bash
   [production1@servera ~]$ ssh root@serverb
   ```

#### **Step 6: Disable Password-Based Authentication**
1. Update the SSH configuration on `serverb` to disable password authentication:
   ```bash
   PasswordAuthentication no
   ```

2. Reload the SSH service:
   ```bash
   [root@serverb ~]# systemctl reload sshd.service
   ```

3. Test login for a user without SSH keys:
   ```bash
   [production1@servera ~]$ ssh production2@serverb
   ```

4. Verify that public key authentication is enabled (default setting):
   ```bash
   [root@serverb ~]$ cat /etc/ssh/sshd_config
   ```

#### **Step 7: Verify Configurations**
1. Confirm the `production1` user can still log in using SSH keys:
   ```bash
   [production1@servera ~]$ ssh production1@serverb
   ```

#### **Step 8: Cleanup**
1. Log out from all machines and return to the workstation:
   ```bash
   [production1@serverb ~]$ exit
   [production1@servera ~]$ exit
   [student@servera ~]$ exit
   ```

2. Grade the lab:
   ```bash
   [student@workstation ~]$ lab grade ssh-review
   ```

3. Complete the lab:
   ```bash
   [student@workstation ~]$ lab finish ssh-review
   ```

---

### **Expected Outcomes**
1. SSH keys enable secure authentication for `production1`.
2. Root login is disabled for SSH.
3. Password-based authentication is disabled.
4. Configuration changes are successfully tested and verified.

By following these steps, you ensure a more secure SSH configuration.
