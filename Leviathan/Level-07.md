# 🐉 OverTheWire Leviathan CTF – Level 7  

## 🌐 **Challenge Description**  
Leviathan is a Linux-based wargame focused on basic Unix commands and privilege escalation.  
👉 Levels can be accessed via SSH on port **2223**.  

---

## 🎯 **Goal**  
- Analyze the binary using GDB to bypass a password check and gain shell access.  

---

## 🌊 **Level 7 Details**  
| **Level** | **Username** | **Password** | **Command to Login** |
|:---------|:-------------|:------------|---------------------|
| Level 7  | leviathan6   | szo7HDB88w   | `ssh leviathan6@leviathan.labs.overthewire.org -p 2223` |

---

## 🚀 **Solution**  

### **Step 1: Connect to the Server**  
Use SSH to connect to the Leviathan server:  

```bash
ssh leviathan6@leviathan.labs.overthewire.org -p 2223
```

- **Username:** `leviathan6`  
- **Password:** `szo7HDB88w`  

👉 SSH allows us to securely connect to the server using port **2223**.  

---

### **Step 2: List All Files**  
Once logged in, list all files (including hidden ones):  

```bash
ls -la
```

**Output Example:**

![ls-la](https://github.com/user-attachments/assets/ca8096e8-c205-46be-b02e-c3906b27d883)


✅ **Findings:**  
- There’s an executable file named **`leviathan6`**.  
- It has **SetUID** permissions, meaning it runs with the privileges of the file owner (in this case, `leviathan7`).  

---

### **Step 3: Execute the Binary**  
Run the binary:  

```bash
./leviathan6
```

**Output Example:**
```bash
Please enter 4-digit password:
```

✅ **Findings:**  
- The binary expects a 4-digit password input.  

---

### **Step 4: Analyze the Binary Using `ltrace`**  
Try to analyze system calls using `ltrace`:  

```bash
ltrace ./leviathan6
```

❌ **Output:**  
- The program does **not** output useful information through `ltrace`.

![ltrace](https://github.com/user-attachments/assets/ed020d67-9d6b-4442-988a-709351fc36c1)

---

### **Step 5: Analyze Using `GDB`**  
Load the binary into `gdb`:  

```bash
gdb --args leviathan6 0000
```

Set a breakpoint to analyze the execution flow:  

```bash
disassemble main
```

![gdb](https://github.com/user-attachments/assets/fb742698-1cb2-447e-8988-6c645f8d9b8d)
![gdb2](https://github.com/user-attachments/assets/b55ce769-267b-4651-a670-2a0492f5b60d)


✅ **Findings:**  
- At offset **+84**, a comparison or validation is happening.  
- We can set a breakpoint there to investigate further.  

---

### **Step 6: Set a Breakpoint**  
Set a breakpoint at the specific memory address:  

```bash
break *0x04921a
```

![break](https://github.com/user-attachments/assets/b1f47e64-6c2d-40d3-ac0f-1e520cd72cfc)

---

### **Step 7: Check the Registers**  
Display register values to find where the password is being validated:  

```bash
info registers
```

![info](https://github.com/user-attachments/assets/29479786-12d7-46b8-ba64-21e64c0f9b87)

---

### **Step 8: Find the Password in Memory**  
Print the value at `$ebp-0xc`:  

```bash
print $ebp-0xc
```

**Output Example:**  
```bash
$1 = 0xffffd36c
```

Now inspect the value stored there:  

```bash
x 0xffffd36c
```

**Output Example:**  
```bash
0x00001bd3
```

Convert the value to decimal:  

```bash
print/d 0x00001bd3
```

**Output Example:**  
```bash
$2 = 7123
```

✅ **Findings:**  
- The password is **7123**.  

![gdb_password](https://github.com/user-attachments/assets/c93bd352-8f5d-4f30-8b98-4e6dcacf043d)

---

### **Step 9: Execute the Binary With the Password**  
Now run the binary with the correct password:  

```bash
./leviathan6 7123
```

✅ **Success:**  
- The binary opens a shell with **leviathan7** privileges.  

---

### **Step 10: Retrieve the Next Password**  
Read the password for the next level:  

```bash
cat /etc/leviathan_pass/leviathan7
```

**Output Example:**  

![Password](https://github.com/user-attachments/assets/26cfa62f-773e-47c6-be4d-28ba2cd7fac3)


---

## ✅ **Password for Leviathan Level 7**  
```bash
qEs5Io5yM8
```

---

## 🖼️ **Screenshots**  
| Step | Screenshot |  
|------|------------|  
| Step 6 – Setting Breakpoint | ![break](https://github.com/user-attachments/assets/b1f47e64-6c2d-40d3-ac0f-1e520cd72cfc) |  
| Step 8 – Finding the Password | ![gdb_password](https://github.com/user-attachments/assets/c93bd352-8f5d-4f30-8b98-4e6dcacf043d) |  

---

## 💡 **Lessons Learned**  
✔️ **Binary Exploitation:**  
- Used `gdb` to reverse-engineer the binary and extract the password.  

✔️ **Register and Stack Analysis:**  
- Analyzed the program state using `info registers` and memory inspection.  

✔️ **SetUID Exploit:**  
- The binary ran with elevated privileges, allowing us to read the password file.  

---

## 🎯 **Next Level**  
Use the password to access **Leviathan Level 7**:  
👉 [http://leviathan.labs.overthewire.org](http://leviathan.labs.overthewire.org)  

---
