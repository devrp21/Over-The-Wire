# Natas CTF Solutions  

## Natas Level 10  

### 🌐 **Challenge Description**  
Natas teaches the basics of server-side web security. Each level consists of a website located at:  
👉 `http://natasX.natas.labs.overthewire.org` (where **X** is the level number).  

---

### 🎯 **Goal**  
- Bypass **blacklisted characters** in the command execution.
- Retrieve the password for the next level.  

---

## 🚀 **Solution**  

### **Step 1: Open the URL**  
Visit:  
```  
http://natas10.natas.labs.overthewire.org  
```  

---

### **Step 2: Enter Login Credentials**  
- **Username:** `natas10`  
- **Password:** Use the password from Natas Level 9:  
```
t7I5VHvpa14sJTUGV0cbEsbYfFP2dmOu
```  
![Home_Page](https://github.com/user-attachments/assets/5d5a2b71-1e3f-4c05-99c5-13d5cd7f9796)

---

### **Step 3: Analyze the Webpage**  
- The page contains an **input box** where we can submit queries.
- A **view source code** link is available to analyze the backend logic.  
- Checking the **source code**, we see the input goes through a **blacklist filter** that blocks characters like `;`, `|`, and `&` to prevent command execution.  

![Source Code](https://github.com/user-attachments/assets/0ff67672-712e-4165-acc0-e91ed01066df)


---

### **Step 4: Exploit the Input Field**  
Since we know that passwords are stored in `/etc/natas_webpass/natasX`, we can try a command that **bypasses the blacklist**:  

```  
-v xxx /etc/natas_webpass/natas11  
```

This works because `-v` lists matching files while avoiding restricted characters.

---

### **Step 5: Retrieve the Password**  
- After submitting the command, the password for **Natas Level 11** appears on the page.  
![Password](https://github.com/user-attachments/assets/4ac4b930-7c28-482f-b437-8b0f158f6f9e)

---

### **✅ Password for Natas Level 11**  
```
UJdqkK1pTu6VLt9UHWAgRZz6sVUZ3lEk
```  

---

## 💡 **Lessons Learned**  
✔️ **Command Injection Filtering**: Some challenges block special characters to prevent command execution.
✔️ **Bypassing Input Restrictions**: Using alternate command options (`-v`, `--help`) can still access restricted data.
✔️ **Source Code Analysis**: Reviewing the backend code can reveal how inputs are processed and filtered.

---

## 🎨 **Screenshots**  
| Step | Screenshot |  
|------|------------|  
| Step 3 – Source Code | ![Source Code](https://github.com/user-attachments/assets/0ff67672-712e-4165-acc0-e91ed01066df) |  
| Step 5 – Extracted Password | ![Password](https://github.com/user-attachments/assets/4ac4b930-7c28-482f-b437-8b0f158f6f9e) |  

---

## 🎯 **Next Level**  
Use the password to access **Natas Level 11**:  
👉 [http://natas11.natas.labs.overthewire.org](http://natas11.natas.labs.overthewire.org)  

---
