# 🔒 OverTheWire Krypton CTF – Level 4

## 🌐 **Challenge Description**  
The password for the next level (Krypton 5) is stored in `/krypton/krypton4/krypton5` and is encrypted using a **Vigenère cipher**.

---

## 🎯 **Goal**  
- Analyze the encrypted files.  
- Break the Vigenère cipher using key length analysis and decryption.  

---

## 🚀 **Solution**  

### **Step 1: Connect to the Server**  
Use the following SSH command to connect to the server:

```bash
ssh krypton4@krypton.labs.overthewire.org -p 2231
```

- **Username:** `krypton4`  
- **Password:** `BRUTE`  

---

### **Step 2: Locate the Password File**  
Navigate to the `krypton4` folder:

```bash
cd /krypton/krypton4
ls -la
```

**Output:**  
You will see the following files:
- `found1`  
- `found2`  
- `found3`  
- `krypton5`  
- `HINT`  
- `README`  

![image](https://github.com/user-attachments/assets/55f2e93d-7c93-4717-9911-a046a7f46008)

---

### **Step 3: Read the README File**  
The README file provides the following information:

```bash
cat README
```

📌 **Key Insight:**  
- The file is encrypted using a **Vigenère cipher**.  
- The key length is **6 characters**.  

Example from README:
```
Key:   GOLD
Plain: PROCEEDMEETINGASAGREED
Ciphertext: VZFZKSOPKSETULVUQWHKR
```

![image](https://github.com/user-attachments/assets/5e38a66b-784f-49a5-a325-328e0e5f5cc5)

---

### **Step 4: Analyze the Encrypted File**  
Check the contents of the encrypted file:

```bash
cat found1
```

**Example Output:**
```bash
MKQNS PEEVZ FIOSX UNCPK SRRDX DFIQT QGEKF FVDLC KRPVA HXZKH SRMLV DQCFR EVKP
...
```

![image](https://github.com/user-attachments/assets/81e6ff4d-ee1a-42e6-8733-7c33a897946c)

---

### **Step 5: Perform Frequency Analysis and Key Length Detection**  
Use an online tool to crack the Vigenère cipher:  

👉 [https://www.dcode.fr/vigenere-cipher](https://www.dcode.fr/vigenere-cipher)  

1. Copy the contents of `found1` into the input box.  
2. Select **"Knowing the key length"** option and enter **6** as the key length.  
3. Press **"Decrypt"**.  

---

### **Step 6: Identify the Key**  
The tool outputs the key as:

```bash
FREKEY
```

✅ The Vigenère key is **"FREKEY"**.  

![image](https://github.com/user-attachments/assets/4573ca8a-59d7-499c-ac92-c42e71567a6d)

---

### **Step 7: Decode the Password File**  
Now decode the `krypton5` file using the key:

1. Copy the contents of `krypton5` into the decoder.  
2. Set the key to **"FREKEY"**.  
3. Press **"Decrypt"**.  

**Output:**  
```bash
CLEAR TEXT
```

![Password](https://github.com/user-attachments/assets/3c28158b-de15-41bd-85d6-bc0758df93c4)

---

## ✅ **Password for Krypton Level 5**  
```bash
CLEARTEXT
```

---

## 🌟 **Key Points**  
✔️ Identified the Vigenère cipher.  
✔️ Used key length analysis to find the key.  
✔️ Decrypted the ciphertext using the key.  

---

## 🎯 **Next Level**  
Use the password to access **Krypton Level 5**.  

---
