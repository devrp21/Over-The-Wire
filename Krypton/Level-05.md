# 🔒 OverTheWire Krypton CTF – Level 5

## 🌐 **Challenge Description**  
The password for the next level (Krypton 6) is stored in `/krypton/krypton5/krypton6` and is encrypted using a **Vigenère cipher** with an unknown key length.

---

## 🎯 **Goal**  
- Analyze the encrypted file.  
- Perform key length analysis.  
- Decrypt the ciphertext to retrieve the password.  

---

## 🚀 **Solution**  

### **Step 1: Connect to the Server**  
Use the following SSH command to connect to the server:

```bash
ssh krypton5@krypton.labs.overthewire.org -p 2231
```

- **Username:** `krypton5`  
- **Password:** `CLEARTEXT`  

---

### **Step 2: Locate the Password File**  
Navigate to the `krypton5` folder:

```bash
cd /krypton/krypton5
ls -la
```

**Output:**  
You will see the following files:
- `found1`  
- `found2`  
- `found3`  
- `krypton6`  
- `README`  

![ls-la](https://github.com/user-attachments/assets/dee6b693-bd00-4d99-a4f0-6f2c584f3d3e)

---

### **Step 3: Read the README File**  
The README file provides the following information:

```bash
cat README
```

![README](https://github.com/user-attachments/assets/7765748f-95ba-4ef6-8459-da7921926d20)


📌 **Key Insight:**  
- The file is encrypted using a **Vigenère cipher**.  
- The key length is **unknown**.  

Example from README:
```
Frequency analysis can break known key lengths as well.  
Let's try one last polyalphabetic cipher, but this time the key length is unknown.
```

---

### **Step 4: Analyze the Encrypted File**  
Check the contents of the encrypted file:

```bash
cat found1
```

**Example Output:**

![image](https://github.com/user-attachments/assets/0284cfb8-d5fc-4a10-bea6-eed9c9464de7)

---

### **Step 5: Perform Frequency Analysis and Key Length Detection**  
Use an online tool to crack the Vigenère cipher:  

👉 [https://www.dcode.fr/vigenere-cipher](https://www.dcode.fr/vigenere-cipher)  
👉 [http://f00l.de/hacking/vigenere.php](http://f00l.de/hacking/vigenere.php)  

1. Copy the contents of `found1` into the input box.  
2. Start testing key lengths one by one.  
3. At key length **9**, the tool outputs "xeylencth" (interpreted as **"keylength"**).  

✅ The Vigenère key is **"keylength"**.  

![key](https://github.com/user-attachments/assets/1b55f883-bc21-4a65-988a-439b0a611bd5)

---

### **Step 6: Decode the Password File**  
Now decode the `krypton6` file using the key:

1. Copy the contents of `krypton6` into the decoder.  
2. Set the key to **"keylength"**.  
3. Press **"Decrypt"**.  

**Output:**  
```bash
RANDOM
```

![Password](https://github.com/user-attachments/assets/72adae8b-d1b6-4a34-99c6-5e9c1c56e5b5)

---

## ✅ **Password for Krypton Level 6**  
```bash
RANDOM
```

---

## 🌟 **Key Points**  
✔️ Identified the Vigenère cipher.  
✔️ Used key length analysis to find the key.  
✔️ Decrypted the ciphertext using the key.  

---

## 🎯 **Next Level**  
Use the password to access **Krypton Level 6**.  

---
