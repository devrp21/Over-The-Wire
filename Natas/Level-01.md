# Natas CTF Solutions  

## Natas Level 1  

### 🌐 **Challenge Description**  
Natas teaches the basics of server-side web security. Each level consists of a website located at:  
👉 `http://natasX.natas.labs.overthewire.org` (where **X** is the level number).  

---

### 🎯 **Goal**  
- Log in to the website.  
- Find the password for the next level.  
- The password might be hidden in the source code or elsewhere on the page.  

---

## 🚀 **Solution**  

### **Step 1: Open the URL**  
Open your browser and navigate to:  
```  
http://natas1.natas.labs.overthewire.org  
```  

---

### **Step 2: Enter Login Credentials**  
- **Username:** `natas1`  
- **Password:** Use the password from Natas Level 0:  
```
0nzCigAq7t2iALyvU9xcHlYN4MlkIwlq
```  

![image](https://github.com/user-attachments/assets/ba769b29-06b6-458f-982d-1f7d820cb2b7)
 

---

### **Step 3: Right-Click Disabled Issue**  
1. When you try to right-click on the page, you'll see a message that right-clicking has been disabled.  
2. To bypass this, open the browser developer tools using the shortcut:  
   ```
   Ctrl + Shift + I  
   ```  
3. Open the **Elements** or **Source** tab and inspect the HTML code.  

![image](https://github.com/user-attachments/assets/8c1d02f4-d7ff-4bd9-a051-72bbdcbb8100)
 

---

### **Step 4: Find the Password in Source Code**  
1. Look for comments or hidden data in the HTML.  
2. Example:  
```html
<!-- The password for natas2 is TguMNxKo1DSa1tujBLuZJnDUlCcUAPlI -->
```  

![image](https://github.com/user-attachments/assets/f51f8467-bee3-4a81-8b04-bd0329d203f4)


---

### **Step 5: Copy the Password**  
Copy the password from the comment:  
```
TguMNxKo1DSa1tujBLuZJnDUlCcUAPlI
```  

---

### **✅ Password for Natas Level 2**  
```
TguMNxKo1DSa1tujBLuZJnDUlCcUAPlI
```  

---

## 💡 **Lessons Learned**  
✔️ Websites can disable right-click using JavaScript, but developer tools can bypass this.  
✔️ Comments in HTML often reveal sensitive information.  
✔️ Knowing browser shortcuts makes finding hidden data easier.  

---

## 🖼️ **Screenshots**  
| Step | Screenshot |  
|-------|------------|  
| Step 2 – Natas1 | ![image](https://github.com/user-attachments/assets/fefc14ae-024d-4af9-a372-0bd6c33481c3)|  
| Step 3 – Right-Click Disabled | ![image](https://github.com/user-attachments/assets/b9b7bed2-76c1-4e79-8cae-d566553fb22a) |  
| Step 4 – Source Code |![image](https://github.com/user-attachments/assets/09248d99-76e6-452c-a151-42630a94ae5a)|  

---

## 🎯 **Next Level**  
Use the password to access **Natas Level 2**:  
👉 [http://natas2.natas.labs.overthewire.org](http://natas2.natas.labs.overthewire.org)  

---
