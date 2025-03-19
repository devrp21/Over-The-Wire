# 🔒 OverTheWire Krypton CTF – Level 0

## 🌐 **Challenge Description**  
Welcome to Krypton! The first level is easy. The following string encodes the password using Base64:

```bash
S1JZUFRPTklTR1JFQVQ=
```

Use this password to log in to `krypton.labs.overthewire.org` with username `krypton1` using SSH on port **2231**. You can find the files for other levels in `/krypton/`.

---

## 🎯 **Goal**  
- Decode the Base64 string to find the password.  

---

## 🚀 **Solution**  

### **Step 1: Decode the String**  
Decode the string using a Base64 decoder (e.g., CyberChef):  

![Password](https://github.com/user-attachments/assets/929cd68b-983c-457f-84a5-7a49b57a43eb)


```bash
KRYPTONISGREAT
```

---

### **Step 2: Connect to the Server**  
Use SSH to connect to the Krypton server:  

```bash
ssh krypton1@krypton.labs.overthewire.org -p 2231
```

- **Username:** `krypton1`  
- **Password:** `KRYPTONISGREAT`  

---

## ✅ **Password for Krypton Level 0**  
```bash
KRYPTONISGREAT
```

---

## 🎯 **Next Level**  
Use the password to access **Krypton Level 1**.  

---
