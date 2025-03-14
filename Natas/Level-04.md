# Natas CTF Solutions  

## Natas Level 4  

### 🌐 **Challenge Description**  
Natas teaches the basics of server-side web security. Each level consists of a website located at:  
👉 `http://natasX.natas.labs.overthewire.org` (where **X** is the level number).  

---

### 🎯 **Goal**  
- Log in to the website.  
- Find the password for the next level.  
- The password might be hidden in the request headers or server response.  

---

## 🚀 **Solution**  

### **Step 1: Open the URL**  
Open your browser and navigate to:  
```  
http://natas4.natas.labs.overthewire.org  
```  

---

### **Step 2: Enter Login Credentials**  
- **Username:** `natas4`  
- **Password:** Use the password from Natas Level 3:  
```
QryZXc2e0zahULdHrtHxzyYkj59kUxLQ
```  

---

### **Step 3: Analyze the Error Message**  
- After logging in, you’ll see an error message:  
   ```
   Access denied. Your request should come from natas5.natas.labs.overthewire.org
   ```  
- This means the server is validating the `Referer` header in the HTTP request.  

![Error Message](https://github.com/user-attachments/assets/fb0f92f4-0c05-4912-8066-1c0b9a8631eb)
 
---

### **Step 4: Open Burp Suite**  
1. Open **Burp Suite** and turn on **Intercept Mode**.  
2. Refresh the page to capture the HTTP request.  

![Burp Suite Intercept](https://github.com/user-attachments/assets/9e9bf6ba-fbc3-459e-9798-9bfee29cab0e)

---

### **Step 5: Modify the `Referer` Header**  
1. In Burp Suite, locate the `Referer` header.  
2. Change it to:  
```
Referer: http://natas5.natas.labs.overthewire.org
```  
3. Forward the modified request.  

![Burp Suite Modify](https://github.com/user-attachments/assets/9f77fe79-e166-4d44-a6f1-32542029738a)

---

### **Step 6: Success!**  
- The page will now load successfully.  
- The password for the next level will be displayed on the page.  

![Success](https://github.com/user-attachments/assets/216e0078-4974-4097-949d-f6293128a189) 

---

### **✅ Password for Natas Level 5**  
```
0n35PkggAPm2zbEpOU802c0x0Msn1ToK
```  

---

## 💡 **Lessons Learned**  
✔️ HTTP headers, especially the `Referer` header, are often used for security checks.  
✔️ Burp Suite is a powerful tool for intercepting and modifying HTTP requests.  
✔️ Modifying headers can bypass basic security mechanisms.  

---

## 🖼️ **Screenshots**  
| Step | Screenshot |  
|-------|------------|  
| Step 3 – Error Message | ![Error Message](https://github.com/user-attachments/assets/fb0f92f4-0c05-4912-8066-1c0b9a8631eb) |  
| Step 4 – Burp Suite Intercept | ![Burp Suite Intercept](https://github.com/user-attachments/assets/9e9bf6ba-fbc3-459e-9798-9bfee29cab0e) |  
| Step 5 – Modify Header | ![Burp Suite Modify](https://github.com/user-attachments/assets/9f77fe79-e166-4d44-a6f1-32542029738a) |  
| Step 6 – Success Page | ![Success](https://github.com/user-attachments/assets/216e0078-4974-4097-949d-f6293128a189) |  

---

## 🎯 **Next Level**  
Use the password to access **Natas Level 5**:  
👉 [http://natas5.natas.labs.overthewire.org](http://natas5.natas.labs.overthewire.org)  

---
