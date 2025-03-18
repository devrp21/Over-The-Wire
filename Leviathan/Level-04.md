# 🐉 OverTheWire Leviathan CTF – Level 4  

## 🌐 **Challenge Description**  
Leviathan is a Linux-based wargame focused on basic Unix commands and privilege escalation.  
👉 Levels can be accessed via SSH on port **2223**.  

---

## 🎯 **Goal**  
- Exploit format string vulnerability to get a shell and extract the password for the next level.  

---

## 🌊 **Level 4 Details**  
| **Level** | **Username** | **Password** | **Command to Login** |
|:---------|:-------------|:------------|---------------------|
| Level 4  | leviathan3   | f0n8h2iWLP   | `ssh leviathan3@leviathan.labs.overthewire.org -p 2223` |

---

## 🚀 **Solution**  

### **Step 1: Connect to the Server**  
Use SSH to connect to the Leviathan server:  

```bash
ssh leviathan3@leviathan.labs.overthewire.org -p 2223
```

- **Username:** `leviathan3`  
- **Password:** `f0n8h2iWLP`  

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

**Output Example:**

![ls-la](https://github.com/user-attachments/assets/35ca124d-8e17-4f7b-9005-ba0201a8f096)

✅ **Findings:**  
- The file **level3** has **SetUID** permissions, which means it runs with the permissions of the owner (`leviathan4`).  

---

### **Step 3: Try Executing the Binary**  
Try running the binary directly:  

```bash
./level3
```

It’s asking for a password — but we don’t have it yet.  

---

### **Step 4: Analyze the Binary Using `ltrace`**  
Use `ltrace` to see which system calls are being used:  

```bash
ltrace ./level3
```

**Output Example:**

![ltrace](https://github.com/user-attachments/assets/fc2d31a2-0f28-49d4-bd7d-127215cac602)


✅ **Key Findings:**  
- The program is calling `snprintf()` with the string **"snlprintf"**.  
- If we enter **"snlprintf"** as the password, the binary will execute `/bin/sh`, giving us a shell with the privileges of `leviathan4`.  

---

### **Step 5: Execute the Binary with the Password**  
Run the binary and enter the correct password:  

```bash
./level3
```

Enter the password:
```
snlprintf
```

**Output Example:**
```bash
$
```

✅ **Shell Access Obtained!**  
- The shell runs with the permissions of `leviathan4`.  

---

### **Step 6: Read the Next Level Password**  
Use `cat` to read the next level’s password:  

```bash
cat /etc/leviathan_pass/leviathan4
```

**Output Example:**

![Password](https://github.com/user-attachments/assets/8d308712-a273-4a60-9462-d54050ca9957)

---

## ✅ **Password for Leviathan Level 4**  
```bash
WG1egElCvO
```

---

## 🖼️ **Screenshots**  
| Step | Screenshot |  
|------|------------|  
| Step 4 – Using `ltrace` | ![ltrace](https://github.com/user-attachments/assets/fc2d31a2-0f28-49d4-bd7d-127215cac602) |  
| Step 5 – Getting a Shell | ![Password](https://github.com/user-attachments/assets/8d308712-a273-4a60-9462-d54050ca9957) |  

---

## 💡 **Lessons Learned**  
✔️ **Format String Vulnerability:**  
- The program was comparing the password using `snprintf()` with a hardcoded value.  
- If you input the correct string, it executes `/bin/sh` with elevated permissions.  

✔️ **SetUID Exploit:**  
- The binary’s SetUID bit allows privilege escalation to the `leviathan4` user.  

---

## 🎯 **Next Level**  
Use the password to access **Leviathan Level 4**:  
👉 [http://leviathan.labs.overthewire.org](http://leviathan.labs.overthewire.org)  

---
