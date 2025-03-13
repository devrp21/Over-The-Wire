# OverTheWire Bandit CTF – Level 32

## 🏆 **Goal**  
The goal of Bandit Level 32 is to break out of a restricted shell environment and retrieve the password for **bandit33**.

---

## 🚀 **Steps to Solve**

### 1. **Connect via SSH**  
Use the password obtained from Level 31 to log into **bandit32** using SSH:

```bash
ssh bandit32@bandit.labs.overthewire.org -p 2220
```

- **Username:** bandit32  
- **Hostname:** bandit.labs.overthewire.org  
- **Port:** 2220  

When prompted, enter the password from Level 31:

```
3O9RfhqyAlVBEZpVb6LYStshZoqoSx5K
```

---

### 2. **Restricted Shell Detected**  
When you log in, you'll notice that **normal commands** like `ls`, `cat`, and `whoami` may not work. This indicates that you're in a restricted shell environment.  

Trying common commands like:

```bash
ls
help
```

Results in output like:

```
-bash: ls: command not found
```

---

### 3. **Escape the Restricted Shell**  
You can try to escape the restricted shell using the `$0` variable, which holds the reference to the shell:

```bash
$0
```

This should drop you into a normal shell environment.

---

### 4. **Check Permissions and Files**  
Now that you're in a normal shell, list the contents of the home directory:

```bash
ls -la
```

Example output:
```
total 12
drwxr-xr-x 3 root root 4096 Mar 8 12:34 .
drwxr-xr-x 3 root root 4096 Mar 8 12:34 ..
-rw-r--r-- 1 root root   36 Mar 8 12:34 README
```

---

### 5. **Find the Password File**  
Use `whoami` to confirm your user:

```bash
whoami
```

Navigate to the `/etc/bandit_pass` directory:

```bash
cat /etc/bandit_pass/bandit33
```

Example output:
```
tQdtbs5D5i2vJwkO8mEyYEyTL8izoeJ0
```

---

## 🔑 **Password for Next Level**  
The password for **Level 33** is:

```
tQdtbs5D5i2vJwkO8mEyYEyTL8izoeJ0
```

---

## ✅ **Summary**  
✔️ Connected to the server using SSH.  
✔️ Bypassed restricted shell using `$0`.  
✔️ Retrieved the password for the next level.  

---

## 📸 **Screenshot**  
![Level-32](https://github.com/user-attachments/assets/61f2395f-87e6-42d1-878a-0902b7d9dc35)<br/>
![Level-32](https://github.com/user-attachments/assets/8c44f126-d1c9-4b0f-a698-0d0fa9d4debb)<br/>
![Level-32](https://github.com/user-attachments/assets/fb3174a0-1211-40b0-9884-154fe3a23172)

---

**Next Step:** Proceed to [Level 33](https://overthewire.org/wargames/bandit/bandit33.html) to continue the challenge.  

---
