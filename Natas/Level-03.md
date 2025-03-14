# Natas CTF Solutions  

## Natas Level 3  

### 🌐 **Challenge Description**  
Natas teaches the basics of server-side web security. Each level consists of a website located at:  
👉 `http://natasX.natas.labs.overthewire.org` (where **X** is the level number).  

---

### 🎯 **Goal**  
- Log in to the website.  
- Find the password for the next level.  
- The password might be hidden in the source code, headers, or server files.  

---

## 🚀 **Solution**  

### **Step 1: Open the URL**  
Open your browser and navigate to:  
```  
http://natas3.natas.labs.overthewire.org  
```  

---

### **Step 2: Enter Login Credentials**  
- **Username:** `natas3`  
- **Password:** Use the password from Natas Level 2:  
```
3gqisGdR0pjm6tpkDKdIWO2hSvchLeYH
```  

---

### **Step 3: Inspect the Page Source**  
1. Open the developer tools using:  
   ```
   Ctrl + Shift + I  
   ```  
2. Check the HTML code — no useful information is visible.  
3. A comment in the code mentions that **Google won't find it**, hinting at a `robots.txt` file.  

![Page Source](https://github.com/user-attachments/assets/9b8fe9a5-fa28-4845-944a-8bc1e0f8fd56)

---

### **Step 4: Check `robots.txt`**  
1. Visit the `robots.txt` file by adding `/robots.txt` to the URL:  
```  
http://natas3.natas.labs.overthewire.org/robots.txt  
```  
2. The `robots.txt` file shows that the `/s3cr3t/` directory is disallowed.  

![robots.txt](https://github.com/user-attachments/assets/bec4fcf9-223d-48da-bdaa-6ddf0518c39a)

---

### **Step 5: Access the Hidden Folder**  
1. Navigate to the hidden directory:  
```  
http://natas3.natas.labs.overthewire.org/s3cr3t/  
```  
2. The directory contains an `index` with a `users.txt` file.  

![Directory Listing](https://github.com/user-attachments/assets/9cd61d3a-f61f-48bb-aba9-fabcc8adc393)

---

### **Step 6: Open `users.txt`**  
1. Open `users.txt` to reveal the password:  
```  
http://natas3.natas.labs.overthewire.org/s3cr3t/users.txt  
```  
2. The password for the next level is shown in the file.  

![Users.txt](https://github.com/user-attachments/assets/4ba164ce-feb9-440c-a399-a5b59508ad2f)

---

### **✅ Password for Natas Level 4**  
```
QryZXc2e0zahULdHrtHxzyYkj59kUxLQ
```  

---

## 💡 **Lessons Learned**  
✔️ `robots.txt` can reveal hidden files and folders.  
✔️ Directory traversal is a common way to expose sensitive data.  
✔️ Hidden comments in source code can give useful hints.  

---

## 🖼️ **Screenshots**  
| Step | Screenshot |  
|-------|------------| 
| Step 2 - Home Page | ![Home_Page](https://github.com/user-attachments/assets/688a7334-0479-4445-a2d3-3987af9f1430) |
| Step 3 – Inspect Page Source | ![Page Source](https://github.com/user-attachments/assets/9b8fe9a5-fa28-4845-944a-8bc1e0f8fd56) |  
| Step 4 – robots.txt | ![robots.txt](https://github.com/user-attachments/assets/bec4fcf9-223d-48da-bdaa-6ddf0518c39a) |  
| Step 5 – Directory Listing | ![Directory Listing](https://github.com/user-attachments/assets/9cd61d3a-f61f-48bb-aba9-fabcc8adc393) |  
| Step 6 – Users.txt Content | ![Users.txt](https://github.com/user-attachments/assets/4ba164ce-feb9-440c-a399-a5b59508ad2f) |  

---

## 🎯 **Next Level**  
Use the password to access **Natas Level 4**:  
👉 [http://natas4.natas.labs.overthewire.org](http://natas4.natas.labs.overthewire.org)  

---
