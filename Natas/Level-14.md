# Natas CTF Solutions  

## Natas Level 14  

### 🌐 **Challenge Description**  
Natas teaches the basics of server-side web security. Each level consists of a website located at:  
👉 `http://natasX.natas.labs.overthewire.org` (where **X** is the level number).  

---

### 🎯 **Goal**  
- Exploit **SQL Injection** to bypass authentication.  
- Retrieve the password for the next level.  

---

## 🚀 **Solution**  

### **Step 1: Open the URL**  
Visit:  
```  
http://natas14.natas.labs.overthewire.org  
```  

---

### **Step 2: Enter Login Credentials**  
- **Username:** `natas14`  
- **Password:** Use the password from Natas Level 13:  
```
z3UYcr4v4uBpeX8f7EZbMHlzK4UR2XtQ
```  
![Home_Page](https://github.com/user-attachments/assets/0cb36efa-0549-4467-b2c9-2ba83a5d6d62)

---

### **Step 3: Analyze the Webpage**  
- The page contains a **login form** asking for a username and password.  
- Viewing the **page source** reveals that the login logic is processed by a **SQL query**.  

![Page Source](https://github.com/user-attachments/assets/2a3371b4-9644-4fe7-8a55-09ec94e57011)

---

### **Step 4: Exploit SQL Injection**  
The form is vulnerable to **SQL Injection**. We can try injecting various payloads to bypass the authentication.  

1. Use **Burp Suite** to intercept the login request:  
   - Open Burp Suite and enable **intercept mode**.  
   - Enter some test values and submit the form.  
   - Send the intercepted request to **Intruder**.  

2. Mark the **password field** as the attack target:  
![Burpsuite](https://github.com/user-attachments/assets/53b91866-a8ae-4e43-92b2-6cc0bef0f72b)

3. Load a list of common SQL Injection payloads (from resources like [securityidiots.com](http://www.securityidiots.com/Web-Pentest/SQL-Injection/bypass-login-using-sql-injection.html)):  
- Example payloads:  
```
' OR 1=1 --
' OR '1'='1' --
admin' --
```
![Payloads](https://github.com/user-attachments/assets/4beb65d5-32f8-4839-8dbd-e97dea7f56fc)

4. Start the attack:  
   - Run the attack in Burp Suite Intruder.  
   - Check the **response length** — the successful response will likely have a different length or content.
     
![Response](https://github.com/user-attachments/assets/3dd02652-31b2-4b31-a8c6-f9d43f88579a)

---

### **Step 5: Successful Payload**  
- After running the attack, the payload `"-"` in the password field successfully bypassed authentication:  
```
Username: admin  
Password: "-"  
```  
- The page displays the password for **Natas Level 15**.  
![Parameters](https://github.com/user-attachments/assets/52b268df-1631-460f-8260-769d7617f4b1)
![Password](https://github.com/user-attachments/assets/558c70f2-832c-4ad3-b714-1c9bc7a3348b)

---

### **✅ Password for Natas Level 15**  
```
SdqIqBsFcz3yotlNYErZSZwblkm0lrvx
```  

---

## 💡 **Lessons Learned**  
✔️ **SQL Injection Basics**: When user input is not properly sanitized, it can be injected into an SQL query.  
✔️ **Intruder Automation**: Burp Suite Intruder allows you to automate injection tests and identify vulnerabilities faster.  
✔️ **Bypass with Single Quotes**: Using `' OR 1=1 --` or `'-` often works when the server processes the input directly in an SQL query.  

---

## 🖼️ **Screenshots**  
| Step | Screenshot |  
|------|------------|  
| Step 3 – Source Code with Login Logic | ![Page Source](https://github.com/user-attachments/assets/2a3371b4-9644-4fe7-8a55-09ec94e57011) |  
| Step 4 – Burp Suite Intruder Setup | ![Burpsuite](https://github.com/user-attachments/assets/53b91866-a8ae-4e43-92b2-6cc0bef0f72b) |  
| Step 5 – Successful Payload Response | ![Response](https://github.com/user-attachments/assets/3dd02652-31b2-4b31-a8c6-f9d43f88579a) |  

---

## 🎯 **Next Level**  
Use the password to access **Natas Level 15**:  
👉 [http://natas15.natas.labs.overthewire.org](http://natas15.natas.labs.overthewire.org)  

---
