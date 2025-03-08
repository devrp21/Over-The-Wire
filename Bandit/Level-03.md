Here's the updated README for **Level 3**:

---

# OverTheWire Bandit CTF – Level 3

## 🏆 **Goal**  
The goal of Bandit Level 3 is to find the password for the next level stored in a hidden file in the `inhere` directory.

---

## 🚀 **Steps to Solve**

### 1. **Connect via SSH**  
Use the password obtained from Level 2 to log into **bandit3** using SSH:

```bash
ssh bandit3@bandit.labs.overthewire.org -p 2220
```

- **Username:** bandit3  
- **Hostname:** bandit.labs.overthewire.org  
- **Port:** 2220  

When prompted, enter the password from Level 2:

```
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
```

---

### 2. **Navigate to the Directory**  
Once logged in, list the files and directories in the current directory:

```bash
ls
```

Output:
```
inhere
```

Change into the `inhere` directory:

```bash
cd inhere
```

---

### 3. **Find the Hidden File**  
To list hidden files, use the `-a` option with `ls`:

```bash
ls -a
```

Output:
```
.  ..  .hidden
```

---

### 4. **Read the Password**  
Use `cat` to read the hidden file:

```bash
cat .hidden
```

Output:
```
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
```

---

## 📸 **Screenshot**  
*Add screenshot here:*  
![Screenshot](path/to/screenshot.png)

---

## 🔑 **Password for Next Level**  
The password for **Level 4** is:

```
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
```

---

## ✅ **Summary**  
✔️ Connected to the server using SSH.  
✔️ Listed files and directories using `ls`.  
✔️ Found the hidden file using `ls -a`.  
✔️ Successfully retrieved the password for Level 4!  

---

**Next Step:** Proceed to [Level 4](https://overthewire.org/wargames/bandit/bandit4.html) to continue the challenge.  

---
