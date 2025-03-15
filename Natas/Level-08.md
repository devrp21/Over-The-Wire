## **Natas Level 8**

### 🌐 **Challenge Details**
- **URL**: [http://natas8.natas.labs.overthewire.org](http://natas8.natas.labs.overthewire.org)
- **Username**: `natas8`
- **Password**: Use the password retrieved from **Natas Level 7**.
```
xcoXLmzMkoIP9D7hlgPlh9XD7OgLAe5Q
``` 
---

## 🚀 **Solution Approach**

### **Step 1: Analyze the Page Source**
- The page contains a **single input field**.
![Home_Page](https://github.com/user-attachments/assets/48a15a48-a91c-464f-9c65-fae3a14b970c)

- Viewing the page source reveals a **PHP code snippet** that encodes a secret value.
![Page_Source](https://github.com/user-attachments/assets/76fc7808-79f6-44b5-ab87-3925e5ece98f)

---

### **Step 2: Understanding the Encoding Logic**
The source code includes this PHP snippet:

```php
echo base64_decode(strrev(hex2bin("3d3d516343746d4d6d6c315669563362")));
```

To **decode this secret**, we must reverse the process:
1. **Convert Hex to Binary**
2. **Reverse the String**
3. **Decode from Base64**

---

### **Step 3: Decoding the Secret**
We can use the following Python script:

```python
import binascii
import base64

encoded_secret = "3d3d516343746d4d6d6c315669563362"
step1 = binascii.unhexlify(encoded_secret)  # Hex to Binary
step2 = step1[::-1]  # Reverse String
decoded_secret = base64.b64decode(step2)  # Base64 Decode

print(decoded_secret.decode())
```

Running this gives us the **decoded secret**:
```
oubWYf2kBq
```

---

### **Step 4: Submitting the Secret**
- Enter `oubWYf2kBq` into the **input field**.
- Click **Submit** to reveal the password for the next level.

![Password](https://github.com/user-attachments/assets/a866c549-3283-4bb5-8f44-7b2409e67c1a)

---

### **✅ Password for Natas Level 9**
```
ZE1ck82lmdGIoErlhQgWND6j2Wzz6b6t
```

---

## 💡 **Key Takeaways**
✔️ **Encoding and Decoding Techniques**  
- **Hex Encoding**: Converts data into hexadecimal representation.  
- **String Reversal**: Simply flips a string.  
- **Base64 Encoding**: Encodes binary data into a printable ASCII format.

✔️ **Reverse Engineering in CTFs**  
- Understanding how **data transformations** work is crucial for breaking encoding schemes.  
- Always **look at the source code** to identify how data is processed.

---

## 🖼️ **Screenshots Section**
| Step | Screenshot |
|------|------------|
| Step 1 – Viewing Page Source | ![Page_Source](https://github.com/user-attachments/assets/76fc7808-79f6-44b5-ab87-3925e5ece98f) |
| Step 4 – Submitting Secret | ![Password](https://github.com/user-attachments/assets/a866c549-3283-4bb5-8f44-7b2409e67c1a) |

---

## 🎯 **Next Level**
Use the password to access **Natas Level 9**:  
👉 [http://natas9.natas.labs.overthewire.org](http://natas9.natas.labs.overthewire.org)

---
