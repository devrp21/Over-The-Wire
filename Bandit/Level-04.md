Here's the updated README for **Level 4**:

---

# OverTheWire Bandit CTF – Level 4

## 🏆 **Goal**  
The goal of Bandit Level 4 is to find the password for the next level stored in the only human-readable file in the `inhere` directory.

---

## 🚀 **Steps to Solve**

### 1. **Connect via SSH**  
Use the password obtained from Level 3 to log into **bandit4** using SSH:

```bash
ssh bandit4@bandit.labs.overthewire.org -p 2220
```

- **Username:** bandit4  
- **Hostname:** bandit.labs.overthewire.org  
- **Port:** 2220  

When prompted, enter the password from Level 3:

```
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
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

### 3. **Find the Human-Readable File**  
To identify the human-readable file, use the `file` command:

```bash
file ./*
```

Example output:
```
./-file00: data
./-file01: data
./-file02: data
./-file03: ASCII text
./-file04: data
./-file05: data
```

From the output, `-file03` is identified as an **ASCII text** file, which is human-readable.

---

### 4. **Read the Password**  
Use `cat` to read the contents of the readable file:

```bash
cat ./-file03
```

Output:
```
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
```

---

## 📸 **Screenshot**  
*Add screenshot here:*  
![Screenshot](path/to/screenshot.png)

---

## 🔑 **Password for Next Level**  
The password for **Level 5** is:

```
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
```

---

## ✅ **Summary**  
✔️ Connected to the server using SSH.  
✔️ Listed files and directories using `ls`.  
✔️ Identified the human-readable file using the `file` command.  
✔️ Successfully retrieved the password for Level 5!  

---

**Next Step:** Proceed to [Level 5](https://overthewire.org/wargames/bandit/bandit5.html) to continue the challenge.  

---
