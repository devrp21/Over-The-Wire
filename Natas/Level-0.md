# Natas CTF Solutions  

## Natas Level 0  

### 🌐 **Challenge Description**  
Natas teaches the basics of server-side web security. Each level consists of a website located at:  
👉 `http://natasX.natas.labs.overthewire.org` (where **X** is the level number).  

### 🎯 **Goal**  
- Log in to the website.  
- Find the password for the next level.  
- The password might be hidden in the source code or elsewhere on the page.  

---

## 🚀 **Solution**  

### **Step 1: Open the URL**  
Open your browser and navigate to:  
```  
http://natas0.natas.labs.overthewire.org  
```  

---

### **Step 2: Enter Login Credentials**  
- **Username:** `natas0`  
- **Password:** `natas0`  

![Login](https://github.com/user-attachments/assets/ef93a3b2-7c3c-49df-b9e3-80913d7d0d5d)

---

### **Step 3: Inspect the Page Source**  
1. After logging in, right-click on the page and select **"Inspect"** (or press `Ctrl + Shift + I`).  
2. Open the **Elements** or **Source** tab.  
3. Look for any comments or hidden text within the HTML.  

📌 **Hint:** Sensitive information is often left in HTML comments or metadata.  

Example:  
```html
<!-- The password for natas1 is 0nzCigAq7t2iALyvU9xcHlYN4MlkIwlq -->
```  

---

### **Step 4: Copy the Password**  
Copy the password from the comment:  
```
0nzCigAq7t2iALyvU9xcHlYN4MlkIwlq
```  

---

### **✅ Password for Natas Level 1**  
```
0nzCigAq7t2iALyvU9xcHlYN4MlkIwlq
```  

---

## 💡 **Lessons Learned**  
✔️ Always inspect the source code — hidden comments can reveal important information.  
✔️ Developer tools (like browser Inspect) are powerful for finding hidden data.  
✔️ Look for patterns like comments, metadata, or JavaScript variables.  

---
fff
## 🖼️ **Screenshots**  
| Step | Screenshot |  
|-------|------------|  
| Step 2 – Login Page |  ![image](https://github.com/user-attachments/assets/358cc95c-09fd-415c-b814-e0f5f8629d80)|  
| Step 3 – Source Code | ![image](https://github.com/user-attachments/assets/0788fcb4-e5b9-42c1-be8a-b8fbf817a242) |  

---

## 🎯 **Next Level**  
Use the password to access **Natas Level 1**:  
👉 [http://natas1.natas.labs.overthewire.org](http://natas1.natas.labs.overthewire.org)  

---
