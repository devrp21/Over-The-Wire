# 🐉 OverTheWire Leviathan CTF – Level 2  

## 🌐 **Challenge Description**  
Leviathan is a Linux-based wargame focused on basic Unix commands and privilege escalation.  
👉 Levels can be accessed via SSH on port **2223**.  

---

## 🎯 **Goal**  
- Analyze a binary using **ltrace** to extract the password for the next level.  

---

## 🌊 **Level 2 Details**  
| **Level** | **Username** | **Password** | **Command to Login** |
|:---------|:-------------|:------------|---------------------|
| Level 2  | leviathan1   | 3QJ3TgzHDq   | `ssh leviathan1@leviathan.labs.overthewire.org -p 2223` |

---

## 🚀 **Solution**  

### **Step 1: Connect to the Server**  
Use SSH to connect to the Leviathan server:  

```bash
ssh leviathan1@leviathan.labs.overthewire.org -p 2223
```

- **Username:** `leviathan1`  
- **Password:** `3QJ3TgzHDq`  

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

![ls-la](https://github.com/user-attachments/assets/c4700783-395c-4f95-8baf-c9589154bca9)

We can see a file named **check** — this is most likely the key to solving the challenge.  

---

### **Step 3: Execute the Binary**  
Try running the `check` file:  

```bash
./check
```
It asks for a password — but we don’t have it yet.  

---

### **Step 4: Analyze the Binary Using `ltrace`**  
Use `ltrace` to trace the library calls made by the binary:  

```bash
ltrace ./check
```

👉 `ltrace` allows us to monitor dynamic library calls made by the program.  

**Output Example:**

![ltrace](https://github.com/user-attachments/assets/50c4b921-8838-4dab-a476-a1803221c869)


✅ **Explanation:**  
- The `strcmp()` function compares two strings.  
- We can see that the password being checked is `"sex"`.  

---

### **Step 5: Run the Binary with the Discovered Password**  
Execute the `check` binary again and input the password:  

```bash
./check
```

Input:
```
Password: sex
```

**Output Example:**

You now have shell access as **leviathan2**!  

---

### **Step 6: Read the Password**  
Switch to the `leviathan2` user and read the password:  

```bash
cat /etc/leviathan_pass/leviathan2
```

**Output Example:**
```
NsN1HwFoyN
```

![Password](https://github.com/user-attachments/assets/6850f561-1d4a-49ea-91b9-23476e8ea434)

---

## ✅ **Password for Leviathan Level 2**  
```
NsN1HwFoyN
```

---

## 🖼️ **Screenshots**  
| Step | Screenshot |  
|------|------------|  
| Step 4 – Using `ltrace` | ![ltrace](https://github.com/user-attachments/assets/50c4b921-8838-4dab-a476-a1803221c869) |  
| Step 5 – Shell Access | ![Password](https://github.com/user-attachments/assets/6850f561-1d4a-49ea-91b9-23476e8ea434) |  

---

## 💡 **Lessons Learned**  
✔️ **Library Tracing:** `ltrace` reveals function calls and arguments.  
✔️ **String Comparison:** `strcmp()` is a common way to check passwords.  
✔️ **Binary Exploitation:** Running and analyzing binaries can reveal hidden passwords.  

---

## 🎯 **Next Level**  
Use the password to access **Leviathan Level 3**:  
👉 [http://leviathan.labs.overthewire.org](http://leviathan.labs.overthewire.org)  

---
