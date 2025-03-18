# 🐉 OverTheWire Leviathan CTF – Level 1  

## 🌐 **Challenge Description**  
Leviathan is a Linux-based wargame focused on basic Unix commands and privilege escalation.  
👉 Levels can be accessed via SSH on port **2223**.  

---

## 🎯 **Goal**  
- Find the password for **Leviathan Level 2** using Unix commands and logical thinking.  

---

## 🌊 **Level 1 Details**  
| **Level** | **Username** | **Password** | **Command to Login** |
|:---------|:-------------|:------------|---------------------|
| Level 1  | leviathan0   | leviathan0   | `ssh leviathan0@leviathan.labs.overthewire.org -p 2223` |

---

## 🚀 **Solution**  

### **Step 1: Connect to the Server**  
Use SSH to connect to the Leviathan server:  

```bash
ssh leviathan0@leviathan.labs.overthewire.org -p 2223
```

- **Username:** `leviathan0`  
- **Password:** `leviathan0`  

👉 SSH allows us to securely connect to the server using port **2223**.  

---

### **Step 2: List All Files**  
Once logged in, list all files (including hidden ones):  

```bash
ls -la
```

👉 The `-la` flag:  
- `l` – Displays file permissions, ownership, and size.  
- `a` – Shows hidden files starting with `.`.  

We see a hidden folder `.backup` — this might contain useful information.  

---

### **Step 3: Enter the `.backup` Folder**  
Navigate to the `.backup` folder using:  

```bash
cd .backup
```

![Directory](https://github.com/user-attachments/assets/e4bd0ead-80b9-4161-8a2d-7999771d707d)

👉 The `cd` command changes the working directory.  

---

### **Step 4: List Files in `.backup`**  
Check the contents of the `.backup` folder:  

```bash
ls
```

**Output Example:**
```
bookmarks.html
```

We have a file named `bookmarks.html` — let's examine its contents!  

---

### **Step 5: Search for the Password**  
Instead of opening the entire file, use `grep` to search for the keyword **"leviathan"**:  

```bash
cat bookmarks.html | grep leviathan
```
![Password](https://github.com/user-attachments/assets/f0649775-bda2-4472-9f28-b2b8f8864cba)


✅ **Explanation:**  
- `cat` → Outputs the contents of the file.  
- `|` → Pipes the output to the next command.  
- `grep` → Filters lines containing the specified keyword.  

**Output Example:**
```
<!-- Password for leviathan1: 3QJ3TgzHDq -->
```

---

### **Step 6: Copy the Password**  
The password for **Leviathan Level 1** is:  

```
3QJ3TgzHDq
```

---

### **Step 7: Exit and Login to Level 1**  
Exit the session using:  

```bash
exit
```

Login to Level 1 using the discovered password:  

```bash
ssh leviathan1@leviathan.labs.overthewire.org -p 2223
```

---

## ✅ **Password for Leviathan Level 1**  
```
3QJ3TgzHDq
```

---

## 🖼️ **Screenshots**  
| Step | Screenshot |  
|------|------------|  
| Step 2 – Listing Files | ![Directory](https://github.com/user-attachments/assets/e4bd0ead-80b9-4161-8a2d-7999771d707d) |  
| Step 5 – Finding the Password | ![Password](https://github.com/user-attachments/assets/f0649775-bda2-4472-9f28-b2b8f8864cba) |  

---

## 💡 **Lessons Learned**  
✔️ **Hidden Files:** Use `ls -la` to reveal hidden files.  
✔️ **Grep Command:** Useful for searching text inside files.  
✔️ **Logical Thinking:** Following logical clues helps solve the challenge.  

---

## 🎯 **Next Level**  
Use the password to access **Leviathan Level 2**:  
👉 [http://leviathan.labs.overthewire.org](http://leviathan.labs.overthewire.org)  

---
