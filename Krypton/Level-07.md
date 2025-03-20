# 🔒 OverTheWire Krypton CTF – Level 7

## 🌐 **Challenge Description**  
The password for Krypton Level 7 was extracted using key analysis and LFSR-based decryption in Level 6.  
Now, let's use the password to log in and verify the solution.

---

## 🎯 **Goal**  
- Use the password to connect to Krypton Level 7.  
- Verify completion of the Krypton series.  

---

## 🚀 **Solution**  

### **Step 1: Connect to Krypton Level 7**  
Use the following SSH command:

```bash
ssh krypton7@krypton.labs.overthewire.org -p 2231
```

- **Username:** `krypton7`  
- **Password:** `LFSRISNOTRANDOM`  

---

### **Step 2: Navigate to the Krypton 7 Folder**  
Navigate to the folder:

```bash
cd /krypton/krypton7
ls -la
```

**Output:**  
```
total 12
drwxr-xr-x 2 root     root     4096 Sep 19 07:10 .
drwxr-xr-x 9 root     root     4096 Sep 19 07:10 ..
-rw-r----- 1 krypton7 krypton7   36 Sep 19 07:10 README
```

![image](https://github.com/user-attachments/assets/8c5cc60d-6ac9-433c-9edf-55d2663c02fd)

---

### **Step 3: Read the Final Message**  
Read the `README` file:

```bash
cat README
```

**Output:**  
```bash
Congratulations on beating Krypton!
```
![image](https://github.com/user-attachments/assets/a4ac7348-a3fc-4cb2-9a06-e34e47be624d)

---

## ✅ **Completion Status**  
🎉 You've successfully completed the **Krypton CTF**!  
- Broke various encryption ciphers.  
- Mastered polyalphabetic, Caesar, and XOR ciphers.  
- Cracked LFSR-based encryption through pattern analysis.  

---

## 🌟 **Achievement Unlocked**  
🏆 **Krypton Master** – Well done! 😎  

---
