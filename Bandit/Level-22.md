# OverTheWire Bandit CTF – Level 22

## 🏆 **Goal**  
The goal of Bandit Level 22 is to find the password for the next level by analyzing a cron job that runs regularly. The cron job script creates a temporary file containing the password for the next level, but the filename is dynamically generated using an MD5 hash.

---

## 🚀 **Steps to Solve**

### 1. **Connect via SSH**  
Use the password obtained from Level 21 to log into **bandit22** using SSH:

```bash
ssh bandit22@bandit.labs.overthewire.org -p 2220
```

- **Username:** bandit22  
- **Hostname:** bandit.labs.overthewire.org  
- **Port:** 2220  

When prompted, enter the password from Level 21:

```
tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q
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
cronjob_bandit23
```

Read the contents of the cron job file:

```bash
cat cronjob_bandit23
```

Example output:
```bash
@reboot bandit23 /usr/bin/cronjob_bandit23.sh &> /dev/null
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh &> /dev/null
```

This shows that the script `/usr/bin/cronjob_bandit23.sh` runs every minute.

---

### 3. **Check the Cron Script**  
Read the script to understand what it does:

```bash
cat /usr/bin/cronjob_bandit23.sh
```

Example output:
```bash
#!/bin/bash
myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)
echo "Password for the next level is in /tmp/$mytarget"
```

This script:  
✅ Gets the current username using `whoami`  
✅ Generates an MD5 hash based on the string `"I am user bandit23"`  
✅ Writes the password into a file in `/tmp` using the hash as the filename  

---

### 4. **Generate the MD5 Hash**  
Since the script creates a temporary file based on the MD5 hash of `"I am user bandit23"`, generate the hash manually:

```bash
echo I am user bandit23 | md5sum | cut -d ' ' -f 1
```

Example output:
```
8ca319486bfbbc3663ea0fbe81326349
```

---

### 5. **Read the Password**  
Use `cat` to read the temporary file:

```bash
cat /tmp/8ca319486bfbbc3663ea0fbe81326349
```

Example output:
```
0Zf11ioIjMVN551jX3CmStKLYqjk54Ga
```

---

## 📸 **Screenshot**  
![Level-22](https://github.com/user-attachments/assets/61e8f08a-da6d-46ed-94a8-5accc3764135)
![Level-22](https://github.com/user-attachments/assets/0704a116-7bca-46da-89b5-96ee5eac30e2)

---

## 🔑 **Password for Next Level**  
The password for **Level 23** is:

```
0Zf11ioIjMVN551jX3CmStKLYqjk54Ga
```

---

## ✅ **Summary**  
✔️ Connected to the server using SSH.  
✔️ Located the cron job configuration in `/etc/cron.d/`.  
✔️ Found the cron job script and analyzed its function.  
✔️ Generated the MD5 hash and used it to locate the temporary file.  
✔️ Retrieved the password for Level 23!  

---

**Next Step:** Proceed to [Level 23](https://overthewire.org/wargames/bandit/bandit23.html) to continue the challenge.  

---
