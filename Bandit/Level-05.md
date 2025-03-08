Here's the updated README for **Level 5**:

---

# OverTheWire Bandit CTF – Level 5

## 🏆 **Goal**  
The goal of Bandit Level 5 is to find the password for the next level stored in a file somewhere under the `inhere` directory that meets the following criteria:  
✔️ Human-readable  
✔️ 1033 bytes in size  
✔️ Not executable  

---

## 🚀 **Steps to Solve**

### 1. **Connect via SSH**  
Use the password obtained from Level 4 to log into **bandit5** using SSH:

```bash
ssh bandit5@bandit.labs.overthewire.org -p 2220
```

- **Username:** bandit5  
- **Hostname:** bandit.labs.overthewire.org  
- **Port:** 2220  

When prompted, enter the password from Level 4:

```
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
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

### 3. **Find the Correct File**  
Since manually searching for the file is inefficient, use the `du` command to find a file that matches the exact size of **1033 bytes**:

```bash
du -b -a | grep 1033
```

Example output:
```
1033    ./maybehere07/.file2
```

---

### 4. **Read the Password**  
Use `cat` to read the contents of the file:

```bash
cat ./maybehere07/.file2
```

Output:
```
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```

---

## 📸 **Screenshot**  
*Add screenshot here:*  
![Screenshot](path/to/screenshot.png)

---

## 🔑 **Password for Next Level**  
The password for **Level 6** is:

```
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```

---

## ✅ **Summary**  
✔️ Connected to the server using SSH.  
✔️ Used `du` and `grep` to quickly identify the file with the correct size.  
✔️ Retrieved the password for Level 6!  

---

**Next Step:** Proceed to [Level 6](https://overthewire.org/wargames/bandit/bandit6.html) to continue the challenge.  

---
