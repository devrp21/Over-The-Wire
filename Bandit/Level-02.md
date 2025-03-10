---

# OverTheWire Bandit CTF – Level 2

## 🏆 **Goal**  
The goal of Bandit Level 2 is to find the password for the next level stored in a file called `spaces in this filename` located in the home directory.

---

## 🚀 **Steps to Solve**

### 1. **Connect via SSH**  
Use the password obtained from Level 1 to log into **bandit2** using SSH:

```bash
ssh bandit2@bandit.labs.overthewire.org -p 2220
```

- **Username:** bandit2  
- **Hostname:** bandit.labs.overthewire.org  
- **Port:** 2220  

When prompted, enter the password from Level 1:

```
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```

---

### 2. **List Files in the Directory**  
Once logged in, list the files in the current directory using:

```bash
ls
```

Output:
```
spaces in this filename
```

---

### 3. **Read the Password**  
Since the file name contains spaces, you need to escape the spaces or wrap the filename in quotes to read it:

```bash
cat "spaces in this filename"
```

OR

```bash
cat spaces\ in\ this\ filename
```

Output:
```
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
```

---

## 📸 **Screenshot**    
![Level-2](https://github.com/user-attachments/assets/7058c086-4430-4b2f-a8da-eae3ebe48819)

---

## 🔑 **Password for Next Level**  
The password for **Level 3** is:

```
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
```

---

## ✅ **Summary**  
✔️ Connected to the server using SSH.  
✔️ Listed files using `ls`.  
✔️ Handled the file with spaces using quotes or escape characters.  
✔️ Successfully retrieved the password for Level 3!  

---

**Next Step:** Proceed to [Level 3](https://overthewire.org/wargames/bandit/bandit3.html) to continue the challenge.  

---
