# 🐉 OverTheWire Leviathan CTF – Level 5  

## 🌐 **Challenge Description**  
Leviathan is a Linux-based wargame focused on basic Unix commands and privilege escalation.  
👉 Levels can be accessed via SSH on port **2223**.  

---

## 🎯 **Goal**  
- Discover a hidden file, extract binary data, and decode it to retrieve the next password.  

---

## 🌊 **Level 5 Details**  
| **Level** | **Username** | **Password** | **Command to Login** |
|:---------|:-------------|:------------|---------------------|
| Level 5  | leviathan4   | WG1egElCvO   | `ssh leviathan4@leviathan.labs.overthewire.org -p 2223` |

---

## 🚀 **Solution**  

### **Step 1: Connect to the Server**  
Use SSH to connect to the Leviathan server:  

```bash
ssh leviathan4@leviathan.labs.overthewire.org -p 2223
```

- **Username:** `leviathan4`  
- **Password:** `WG1egElCvO`  

👉 SSH allows us to securely connect to the server using port **2223**.  

---

### **Step 2: List All Files**  
Once logged in, list all files (including hidden ones):  

```bash
ls -la
```

**Output Example:**

![ls-la](https://github.com/user-attachments/assets/65fd1b16-64ad-443d-a62c-7a05c99634e7)


✅ **Findings:**  
- There’s a hidden folder named **`.trash`**.  

---

### **Step 3: Navigate to the Hidden Folder**  
Change directory to the hidden folder:  

```bash
cd ./.trash
```

List the files inside:  

```bash
ls -la
```

**Output Example:**

![trash](https://github.com/user-attachments/assets/f4286fd2-8a1e-4bf9-83c5-1327f0dbdb9a)


✅ **Findings:**  
- A binary file named **`bin`** is present.  
- It has **SetUID** permissions for `leviathan5`, meaning it could execute with elevated privileges.  

---

### **Step 4: Analyze the Binary Using `ltrace`**  
Use `ltrace` to analyze system calls:  

```bash
ltrace ./bin
```

✅ **Key Findings:**  
- The program attempts to read the file `/etc/leviathan_pass/leviathan5`.  
- The output is likely encoded or binary data.  

---

### **Step 5: Execute the Binary**  
Run the binary:  

```bash
./bin
```

**Output Example:**

![ltrace](https://github.com/user-attachments/assets/cb1b7995-7657-4108-b0d6-469d88c80dba)

✅ **Findings:**  
- The output is binary data.  

---

### **Step 6: Decode the Binary Data**  
- Copy the binary data.  
- Go to [CyberChef](https://gchq.github.io/CyberChef/).  
- Use the **"From Binary"** operation to decode it.  

**Decoded Output Example:**  

![Cyberchef](https://github.com/user-attachments/assets/a56b8b56-c77b-490b-8619-57fd85187993)


✅ **Decoded Password:**  
- The binary data decodes to the password for the next level.  

---

### **Step 7: Read the Next Level Password**  
The decoded string is the password for **Leviathan Level 5**.  

---

## ✅ **Password for Leviathan Level 5**  
```
0dyxT7F4QD
```

---

## 🖼️ **Screenshots**  
| Step | Screenshot |  
|------|------------|  
| Step 4 – Using `ltrace` | ![ltrace](https://github.com/user-attachments/assets/cb1b7995-7657-4108-b0d6-469d88c80dba) |  
| Step 6 – Decoding Binary Data | ![Cyberchef](https://github.com/user-attachments/assets/a56b8b56-c77b-490b-8619-57fd85187993) |  

---

## 💡 **Lessons Learned**  
✔️ **SetUID Exploit:**  
- The binary was able to open and read the next level’s password file due to SetUID permissions.  

✔️ **Binary Encoding:**  
- The password was encoded in binary format to obscure it.  
- Tools like **CyberChef** are helpful for quick decoding.  

---

## 🎯 **Next Level**  
Use the password to access **Leviathan Level 5**:  
👉 [http://leviathan.labs.overthewire.org](http://leviathan.labs.overthewire.org)  

---
