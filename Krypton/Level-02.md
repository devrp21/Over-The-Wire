# 🔒 OverTheWire Krypton CTF – Level 2

## 🌐 **Challenge Description**  
The password for the next level (Krypton 3) is stored in `/krypton/krypton2/krypton3` and is encoded using a Caesar Cipher.

---

## 🎯 **Goal**  
- Discover the Caesar Cipher shift.  
- Decrypt the encoded password.  

---

## 🚀 **Solution**  

### **Step 1: Connect to the Server**  
Use the following SSH command to connect to the server:

```bash
ssh krypton2@krypton.labs.overthewire.org -p 2231
```

- **Username:** `krypton2`  
- **Password:** `ROTTEN`  

---

### **Step 2: Locate the Password File**  
Navigate to the `krypton2` folder:

```bash
cd /krypton/krypton2
ls -la
```

![ls-la](https://github.com/user-attachments/assets/5aef3bde-274c-4e34-be70-4264d4fbbd62)

---

### **Step 3: Read the README File**  
The README file provides a hint that the file is encrypted using a Caesar Cipher:

```bash
cat README
```

![Readme](https://github.com/user-attachments/assets/c2245a6e-505c-42f8-bed2-62388130980b)


📌 **Key Insight:**  
- A Caesar Cipher shifts the alphabet by a fixed number of positions.  
- Our goal is to figure out the shift value.  

---

### **Step 4: Find the Caesar Cipher Shift**  
We’ll determine the shift by comparing encrypted and plain text.

#### ✅ Create a Temporary Directory:
```bash
mktemp -d
```

This creates a temporary working directory.  

#### ✅ Create a Symlink to the Keyfile:
```bash
ln -s /krypton/krypton2/keyfile.dat
```

This links the keyfile to our working directory so the encryption tool can use it.

#### ✅ Set Permissions:
```bash
chmod 777 .
```

This sets full permissions to avoid access issues.

#### ✅ Create a Test File for Encryption:
```bash
echo "AAAAA" > encrypt.txt
```

#### ✅ Encrypt the Test File:
```bash
/krypton/krypton2/encrypt encrypt.txt
```

#### ✅ View the Output:
```bash
cat ciphertext
```

**Output:**  
`MMMMM`  

![Cipher](https://github.com/user-attachments/assets/cee0b4d8-c6df-4b45-b6d6-38386a66d503)

📌 **Key Insight:**  
- `A → M` means a shift of **12** places.  
- To decode, we need to reverse this shift by moving **14 characters** (26 - 12).  

---

### **Step 5: Decrypt the Password**  
The encrypted password is in `krypton3`. Decode it using the Caesar Cipher shift:

```bash
cat krypton3 | tr 'A-Za-z' 'O-ZA-No-za-n'
```

**Decoded Output:**  
```bash
CAESARISEASY
```

![Password](https://github.com/user-attachments/assets/65367997-c8c9-4cfd-b850-e8cab4ddcaa3)

---

## ✅ **Password for Krypton Level 3**  
```bash
CAESARISEASY
```

---

## 🌟 **Key Points**  
✔️ Used a temporary working directory to avoid permission issues.  
✔️ Created a symlink to the keyfile to enable encryption.  
✔️ Determined the Caesar shift using a controlled test.  
✔️ Applied the reverse shift to decode the password.  

---

## 🎯 **Next Level**  
Use the password to access **Krypton Level 3**.  

---
