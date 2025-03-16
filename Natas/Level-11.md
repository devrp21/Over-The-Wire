# Natas CTF Solutions  

## Natas Level 11  

### 🌐 **Challenge Description**  
Natas teaches the basics of server-side web security. Each level consists of a website located at:  
👉 `http://natasX.natas.labs.overthewire.org` (where **X** is the level number).  

---

### 🎯 **Goal**  
- Decode the **XOR-encrypted cookie** to bypass authentication.  
- Retrieve the password for the next level.  

---

## 🚀 **Solution**  

### **Step 1: Open the URL**  
Visit:  
```  
http://natas11.natas.labs.overthewire.org  
```  

---

### **Step 2: Enter Login Credentials**  
- **Username:** `natas11`  
- **Password:** Use the password from Natas Level 10:  
```
UJdqkK1pTu6VLt9UHWAgRZz6sVUZ3lEk
```  
![Home_Page](https://github.com/user-attachments/assets/a9853f8f-ebbb-4f86-9e94-0d1c43ebdad0)

---

### **Step 3: Analyze the Webpage**  
- The page contains an input box.  
- A **source code link** is available, revealing that the site uses **XOR encryption** for cookies.  

![Page Source](https://github.com/user-attachments/assets/720a2496-0bd0-46ba-9657-84e6ea1a8a32)

---

### **Step 4: Extract the Cookie**  
1. Open **Developer Tools** (`Ctrl + Shift + I`) → **Application** tab → **Storage** → **Cookies**  
2. You will find a cookie value similar to this:  
```
HmYkBwozJw4WNyAAFyB1VUcqOE1JZjUIBis7ABdmbU1GIjEJAyJnTRg%3D
```  
3. URL decode the cookie using a tool like [CyberChef](https://gchq.github.io/CyberChef/):  
```
HmYkBwozJw4WNyAAFyB1VUcqOE1JZjUIBis7ABdmbU1GIjEJAyJnTRg=
```  

---

### **Step 5: Decode XOR Encryption**  
- According to the source code, the encryption uses XOR and Base64 encoding.  
- Use CyberChef to decode it:  
  - First, **Base64 Decode**  
  - Then, **XOR Decode** (key can be guessed from patterns or trial and error)  
- You will get an output like this:  
```
eDWo...
```  
![Decoded_XOR](https://github.com/user-attachments/assets/4532f06f-0795-40ee-accf-8e2fede8c760)

---

### **Step 6: Modify the Cookie**  
- Take the decoded value.  
- Reverse the XOR and Base64 process to generate a valid modified cookie.  
- Replace the cookie value in storage.  
![Cookie_Value](https://github.com/user-attachments/assets/e72cee83-e691-4962-92f2-e54515eb5702)

---

### **Step 7: Refresh the Page**  
- After replacing the cookie, refresh the page.  
- The password for the next level will be revealed!  
![Password](https://github.com/user-attachments/assets/f8432faf-2a20-420e-9cb0-0c04265b1da0)

---

### **✅ Password for Natas Level 12**  
```
yZdkjAYZRd3R7tq7T5kXMjMJlOIkzDeB
```  

---

## 💡 **Lessons Learned**  
✔️ **XOR Encoding**: XOR-based encryption can be decoded if the key or pattern is known.  
✔️ **Base64 Encoding**: Understanding Base64 encoding/decoding is essential for breaking web-based security challenges.  
✔️ **Cookie Manipulation**: Accessing and modifying cookies can bypass authentication or gain privileged access.  

---

## 🖼️ **Screenshots**  
| Step | Screenshot |  
|------|------------|  
| Step 3 – Source Code with XOR Logic | ![Page Source](https://github.com/user-attachments/assets/720a2496-0bd0-46ba-9657-84e6ea1a8a32) |  
| Step 5 – CyberChef Decoding | ![Decoded_XOR](https://github.com/user-attachments/assets/4532f06f-0795-40ee-accf-8e2fede8c760) |  

---

## 🎯 **Next Level**  
Use the password to access **Natas Level 12**:  
👉 [http://natas12.natas.labs.overthewire.org](http://natas12.natas.labs.overthewire.org)  
