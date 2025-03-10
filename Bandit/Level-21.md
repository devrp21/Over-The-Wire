# OverTheWire Bandit CTF – Level 21

## 🏆 **Goal**  
The goal of Bandit Level 21 is to find the password for the next level by analyzing a cron job that runs at regular intervals. The configuration for the cron job is located in `/etc/cron.d/`.  

---

## 🚀 **Steps to Solve**

### 1. **Connect via SSH**  
Use the password obtained from Level 20 to log into **bandit21** using SSH:

```bash
ssh bandit21@bandit.labs.overthewire.org -p 2220
```

- **Username:** bandit21  
- **Hostname:** bandit.labs.overthewire.org  
- **Port:** 2220  

When prompted, enter the password from Level 20:

```
EeoULMCra2q0dSkYj561DX7s1CpBuOBt
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
cronjob_bandit22
```

Read the contents of the cron job file:

```bash
cat cronjob_bandit22
```

Example output:
```bash
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
```

This shows that the script `/usr/bin/cronjob_bandit22.sh` runs every minute.

---

### 3. **Check the Cron Script**  
Read the script to understand what it does:

```bash
cat /usr/bin/cronjob_bandit22.sh
```

Example output:
```bash
#!/bin/bash
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

The script writes the password for **bandit22** into a temporary file.

---

### 4. **Read the Password**  
Use `cat` to read the temporary file:

```bash
cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

Example output:
```
tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q
```

---

## 📸 **Screenshot**  
![Level-21](https://github.com/user-attachments/assets/9de3672b-8f6b-4a1c-9c69-ecfdd00f5aed)

---

## 🔑 **Password for Next Level**  
The password for **Level 22** is:

```
tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q
```

---

## ✅ **Summary**  
✔️ Connected to the server using SSH.  
✔️ Located the cron job configuration in `/etc/cron.d/`.  
✔️ Found the cron job script and analyzed its function.  
✔️ Retrieved the password for Level 22!  

---

**Next Step:** Proceed to [Level 22](https://overthewire.org/wargames/bandit/bandit22.html) to continue the challenge.  

---
