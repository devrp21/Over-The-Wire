---

# OverTheWire Bandit CTF – Level 1

## 🏆 **Goal**  
The goal of Bandit Level 1 is to find the password for the next level stored in a file called `-` located in the home directory.

---

## 🚀 **Steps to Solve**

### 1. **Connect via SSH**  
Use the password obtained from Level 0 to log into **bandit1** using SSH:

```bash
ssh bandit1@bandit.labs.overthewire.org -p 2220
```

- **Username:** bandit1  
- **Hostname:** bandit.labs.overthewire.org  
- **Port:** 2220  

When prompted, enter the password from Level 0:

```
ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
```

---

### 2. **List Files in the Directory**  
Once logged in, list the files in the current directory using:

```bash
ls
```

Output:
```
-
```

---

### 3. **Read the Password**  
Since the file is named `-`, using `cat -` would normally read from standard input instead of the file.  
To avoid this issue, use `./` to reference the file directly:

```bash
cat ./-
```

Output:
```
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```

---

## 📸 **Screenshot**   
![Level-1](https://github.com/user-attachments/assets/5ec0c441-2280-4a3d-8d11-fbfeba2613f5)


---

## 🔑 **Password for Next Level**  
The password for **Level 2** is:

```
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```

---

## ✅ **Summary**  
✔️ Connected to the server using SSH.  
✔️ Listed files using `ls`.  
✔️ Handled the tricky filename using `./`.  
✔️ Successfully retrieved the password for Level 2!  

---

**Next Step:** Proceed to [Level 2](https://overthewire.org/wargames/bandit/bandit2.html) to continue the challenge.  

---
