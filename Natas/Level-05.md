# Natas CTF Solutions  

## Natas Level 5  

### 🌐 **Challenge Description**  
Natas teaches the basics of server-side web security. Each level consists of a website located at:  
👉 `http://natasX.natas.labs.overthewire.org` (where **X** is the level number).  

---

### 🎯 **Goal**  
- Log in to the website.  
- Find the password for the next level.  
- The password might be hidden in cookies or session data.  

---

## 🚀 **Solution**  

### **Step 1: Open the URL**  
Open your browser and navigate to:  
```  
http://natas5.natas.labs.overthewire.org  
```  

---

### **Step 2: Enter Login Credentials**  
- **Username:** `natas5`  
- **Password:** Use the password from Natas Level 4:  
```
0n35PkggAPm2zbEpOU802c0x0Msn1ToK
```  

---

### **Step 3: Analyze the Message**  
- After logging in, you’ll see a message:  
   ```
   Access disallowed. You are not logged in.
   ```  

![Error Message](https://github.com/user-attachments/assets/377d13a1-94cd-4c43-bf36-93d0bb525ff6)

---

### **Step 4: Check Browser Cookies**  
1. Open **Developer Tools** using **Ctrl + Shift + I**.  
2. Go to the **Application** tab.  
3. Under **Storage → Cookies**, you’ll find a cookie named `loggedin` with a value of `0`.  

![Cookie Storage](https://github.com/user-attachments/assets/7e48e396-1e64-42c4-b9de-fb8c5ecb9bb1)
 
---

### **Step 5: Modify the Cookie Value**  
1. Double-click on the `loggedin` value.  
2. Change it from `0` to `1`.  

```
loggedin=1
```  
---

### **Step 6: Refresh the Page**  
- After modifying the cookie, refresh the page.  
- You should now be logged in!  
- The password for the next level will appear on the page.  

![Success](https://github.com/user-attachments/assets/4ba6a5a2-8b87-44a9-b0da-2375de622a73)

---

### **✅ Password for Natas Level 6**  
```
0RoJwHdSKWFTYR5WuiAewauSuNaBXned
```  

---

## 💡 **Lessons Learned**  
✔️ Cookies are often used to store session data.  
✔️ Modifying cookie values can bypass access control mechanisms.  
✔️ Browser developer tools provide powerful access to session and storage data.  

---

## 🖼️ **Screenshots**  
| Step | Screenshot |  
|-------|------------|  
| Step 3 – Error Message | ![Error Message](https://github.com/user-attachments/assets/377d13a1-94cd-4c43-bf36-93d0bb525ff6) |  
| Step 4 – Cookies Storage | ![Cookie Storage](https://github.com/user-attachments/assets/7e48e396-1e64-42c4-b9de-fb8c5ecb9bb1) |  
| Step 6 – Success Page | ![Success](https://github.com/user-attachments/assets/4ba6a5a2-8b87-44a9-b0da-2375de622a73) |  

---

## 🎯 **Next Level**  
Use the password to access **Natas Level 6**:  
👉 [http://natas6.natas.labs.overthewire.org](http://natas6.natas.labs.overthewire.org)  

---
