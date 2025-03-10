
# OverTheWire Bandit CTF – Level 17

## 🏆 **Goal**  
The goal of Bandit Level 17 is to find the password for the next level by comparing two files: `passwords.old` and `passwords.new`, and identifying the difference between them.  

---

## 🚀 **Steps to Solve**

### 1. **Connect via SSH**  
Use the private key obtained from Level 16 to log into **bandit17** using SSH:

```bash
ssh -i sshkey17.private bandit17@bandit.labs.overthewire.org -p 2220
```

- **Username:** bandit17  
- **Hostname:** bandit.labs.overthewire.org  
- **Port:** 2220  

---

### 2. **Locate the Files**  
List the files in the home directory:

```bash
ls
```

Output:
```
passwords.old  passwords.new
```

---

### 3. **Find the Difference**  
Use the `diff` command to compare the two files and identify the difference:

```bash
diff passwords.new passwords.old
```

Example output:
```
1c1
< x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
---
> oldpasswordhere
```

---

### 4. **Retrieve the Password**  
The line prefixed with `<` in the output is the password for the next level:

```
x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
```

---

## 📸 **Screenshot**  
![Level-17](https://github.com/user-attachments/assets/2c6a75c6-664c-42fe-981d-984667eece17)


---

## 🔑 **Password for Next Level**  
The password for **Level 18** is:

```
x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
```

---

## ✅ **Summary**  
✔️ Connected to the server using SSH and private key.  
✔️ Used `diff` to compare the files.  
✔️ Identified the changed line containing the password.  
✔️ Retrieved the password for Level 18!  

---

**Next Step:** Proceed to [Level 18](https://overthewire.org/wargames/bandit/bandit18.html) to continue the challenge.  

