# Natas CTF Solutions  

## Natas Level 6  

### 🌐 **Challenge Description**  
Natas teaches the basics of server-side web security. Each level consists of a website located at:  
👉 `http://natasX.natas.labs.overthewire.org` (where **X** is the level number).  

---

### 🎯 **Goal**  
- Find the **secret key** required for authentication.  
- Retrieve the password for the next level.  

---

## 🚀 **Solution**  

### **Step 1: Open the URL**  
Visit:  
```  
http://natas6.natas.labs.overthewire.org  
```  

---

### **Step 2: Enter Login Credentials**  
- **Username:** `natas6`  
- **Password:** Use the password from Natas Level 5:  
```
0RoJwHdSKWFTYR5WuiAewauSuNaBXned
```  

---

### **Step 3: Analyze the Webpage**  
- The page contains an **input field** requesting a secret value.  
- There’s also a **View Source Code** link.  

![Challenge Page](https://github.com/user-attachments/assets/13e5ae42-6ed7-4e5f-a6dc-fa81d4bc35ad) 

---

### **Step 4: Inspect the Source Code**  
- Click on **"View sourcecode"** or go directly to:  
  ```
  http://natas6.natas.labs.overthewire.org/index-source.html
  ```
- The PHP code reveals an **includes/secret.inc** file.  

![Source_Code](https://github.com/user-attachments/assets/2970c78c-7e6a-4262-8406-f31f53af1d0e)

---

### **Step 5: Find the Secret Key**  
- The **secret key** is stored in `includes/secret.inc`.  
- Try accessing the file in the browser:  
  ```
  http://natas6.natas.labs.overthewire.org/includes/secret.inc
  ```
- The page appears blank.  
- **View the page source (Ctrl + U)** to reveal:  

```php
<?php
$secret = "FOEIUWGHFEEUHOFUOIU";
?>
```

![Secret Key](https://github.com/user-attachments/assets/a694f23f-53a0-46a7-ab8d-0059153b06ba)

---

### **Step 6: Use the Secret Key**  
- Enter **FOEIUWGHFEEUHOFUOIU** in the input field and submit.  
- The password for **Natas Level 7** is displayed.  

![Password](https://github.com/user-attachments/assets/102d1460-195b-4f9c-9f88-07996dbf2583)

---

### **✅ Password for Natas Level 7**  
```
bmg8SvU1LizuWjx3y7xkNERkHxGre0GS
```  

---

## 💡 **Lessons Learned**  
✔️ **Code disclosure vulnerabilities**: Viewing the source code can reveal sensitive information.  
✔️ **File inclusion flaws**: Including files (`secret.inc`) can expose confidential data if not properly restricted.  
✔️ **Hidden values in source code**: Always check **page source (Ctrl + U)** for hidden data.  

---

## 🖼️ **Screenshots**  
| Step | Screenshot |  
|------|------------|  
| Step 3 – Challenge Page | ![Challenge Page](https://github.com/user-attachments/assets/13e5ae42-6ed7-4e5f-a6dc-fa81d4bc35ad) |  
| Step 5 – Secret Key Found | ![Secret Key](https://github.com/user-attachments/assets/a694f23f-53a0-46a7-ab8d-0059153b06ba) | 
| Step 6 - Displayed Password | ![Password](https://github.com/user-attachments/assets/102d1460-195b-4f9c-9f88-07996dbf2583) |

---

## 🎯 **Next Level**  
Use the password to access **Natas Level 7**:  
👉 [http://natas7.natas.labs.overthewire.org](http://natas7.natas.labs.overthewire.org)  

---
