# Natas CTF Solutions  

## Natas Level 2  

### 🌐 **Challenge Description**  
Natas teaches the basics of server-side web security. Each level consists of a website located at:  
👉 `http://natasX.natas.labs.overthewire.org` (where **X** is the level number).  

---

### 🎯 **Goal**  
- Log in to the website.  
- Find the password for the next level.  
- The password might be hidden in the source code or accessible through directory traversal.  

---

## 🚀 **Solution**  

### **Step 1: Open the URL**  
Open your browser and navigate to:  
```  
http://natas2.natas.labs.overthewire.org  
```  

---

### **Step 2: Enter Login Credentials**  
- **Username:** `natas2`  
- **Password:** Use the password from Natas Level 1:  
```
TguMNxKo1DSa1tujBLuZJnDUlCcUAPlI
```  

---

### **Step 3: Inspect the Page Source**  
1. Open the developer tools using:  
   ```
   Ctrl + Shift + I  
   ```  
2. Open the **Elements** tab and inspect the HTML code.  
3. You’ll notice a `<div>` tag with a reference to a folder named **/files**.  

![Inspect Page](https://github.com/user-attachments/assets/44b5db2d-fda6-4cbd-ab76-ad435b47a423)
  

---

### **Step 4: Directory Traversal**  
1. Since the `/files` folder is accessible, modify the URL to explore the folder:  
```  
http://natas2.natas.labs.overthewire.org/files  
```  
2. You’ll see a list of available files.  

![Directory Listing](https://github.com/user-attachments/assets/7b714a39-bc5d-463b-8ef0-d8468f4816a4)

---

### **Step 5: Open `users.txt`**  
1. Open the `users.txt` file directly by visiting:  
```  
http://natas2.natas.labs.overthewire.org/files/users.txt  
```  
2. The file contains the password for the next level.  

![Users.txt](https://github.com/user-attachments/assets/b6b9d752-a526-4961-85e0-8431ca9dc3d0)


---

### **✅ Password for Natas Level 3**  
```
3gqisGdR0pjm6tpkDKdIWO2hSvchLeYH
```  

---

## 💡 **Lessons Learned**  
✔️ Directory traversal can expose sensitive files.  
✔️ Browsing accessible folders often leads to critical information.  
✔️ Always inspect hidden folders and file paths.  

---

## 🖼️ **Screenshots**  
| Step | Screenshot |  
|-------|------------| 
| Step 2 - Natas2 Page | ![Natas2](https://github.com/user-attachments/assets/9ccd09eb-1c82-4624-a389-a23c52f9f429)|
| Step 3 – Inspect Page Source | ![Inspect Page](https://github.com/user-attachments/assets/44b5db2d-fda6-4cbd-ab76-ad435b47a423) |  
| Step 4 – Directory Listing | ![Directory Listing](https://github.com/user-attachments/assets/7b714a39-bc5d-463b-8ef0-d8468f4816a4) |  
| Step 5 – Users.txt Content | ![Users.txt](https://github.com/user-attachments/assets/b6b9d752-a526-4961-85e0-8431ca9dc3d0)|  

---

## 🎯 **Next Level**  
Use the password to access **Natas Level 3**:  
👉 [http://natas3.natas.labs.overthewire.org](http://natas3.natas.labs.overthewire.org)  

---
