
# OverTheWire Bandit CTF – Level 19

## 🏆 **Goal**  
The goal of Bandit Level 19 is to find the password for the next level, which is stored in **/etc/bandit_pass/bandit20**.  
You must use a **setuid binary** in the home directory to read the password, since you don’t have direct access to the file.  

---

## 🚀 **Steps to Solve**

### 1. **Connect via SSH**  
Use the password obtained from Level 18 to log into **bandit19** using SSH:

```bash
ssh bandit19@bandit.labs.overthewire.org -p 2220
```

- **Username:** bandit19  
- **Hostname:** bandit.labs.overthewire.org  
- **Port:** 2220  

When prompted, enter the password from Level 18:

```
cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8
```

---

### 2. **List the Files**  
After logging in, list the files in the home directory:

```bash
ls
```

Example output:
```
bandit20-do
```

---

### 3. **Execute the SetUID Binary**  
To gain access to the password file, execute the **setuid binary** using `./bandit20-do`.  
Since you don’t have direct permission to access the file, this binary will allow you to execute the command with elevated privileges:

```bash
./bandit20-do cat /etc/bandit_pass/bandit20
```

Example output:
```
0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
```

---

## 📸 **Screenshot**  
![Level-19](https://github.com/user-attachments/assets/5e4108ac-ab09-44d4-84b7-37e55d0015b2)


---

## 🔑 **Password for Next Level**  
The password for **Level 20** is:

```
0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
```

---

## ✅ **Summary**  
✔️ Connected to the server using SSH.  
✔️ Identified the setuid binary in the home directory.  
✔️ Used the binary to execute a privileged command and read the password file.  
✔️ Retrieved the password for Level 20!  

---

**Next Step:** Proceed to [Level 20](https://overthewire.org/wargames/bandit/bandit20.html) to continue the challenge.  

---
