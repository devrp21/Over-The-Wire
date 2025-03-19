# 🔒 OverTheWire Krypton CTF – Level 1

## 🌐 **Challenge Description**  
Now that you've logged into Krypton, the passwords for the next levels are stored in the `/krypton` folder.

---

## 🎯 **Goal**  
- Find the password for Krypton Level 2.  

---

## 🚀 **Solution**  

### **Step 1: Connect to the Server**  
Use the following SSH command to connect to the server:

```bash
ssh krypton1@krypton.labs.overthewire.org -p 2231
```

- **Username:** `krypton1`  
- **Password:** `KRYPTONISGREAT`  

---

### **Step 2: Locate the Password File**  
List the contents of the `/krypton` folder:

```bash
ls -la /krypton
```

![ls-la](https://github.com/user-attachments/assets/94408ca5-f5d4-4068-bb4c-835ce550a964)


Navigate to the `krypton1` folder:

```bash
cd /krypton/krypton1
ls -la
```

![image](https://github.com/user-attachments/assets/60b98aaa-1b99-48f6-97ff-17d48270120c)

---

### **Step 3: Read the Password File**  
Read the file `krypton2`:

```bash
cat krypton2
```

Output:
```bash
YRIRY GJB CNFFJBEQ EBGGRA
```

![Crypted_Password](https://github.com/user-attachments/assets/035aad3d-99b4-4f66-9707-044fdf823b7e)

---

### **Step 4: Decode ROT13**  
The README file mentions that the text is encoded with ROT13. Decode it using CyberChef or a ROT13 decoder:

Decoded Output:
```bash
LEVEL TWO PASSWORD ROTTEN
```

![Password](https://github.com/user-attachments/assets/a2f18626-ea34-4a1e-8d5b-b1a0f3d09c4a)

---

## ✅ **Password for Krypton Level 2**  
```bash
ROTTEN
```

---

## 🎯 **Next Level**  
Use the password to access **Krypton Level 2**.  

---
