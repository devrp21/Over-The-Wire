# 🔒 OverTheWire Krypton CTF – Level 3

## 🌐 **Challenge Description**  
The password for the next level (Krypton 4) is stored in `/krypton/krypton3/krypton4` and is encrypted using a **substitution cipher**.

---

## 🎯 **Goal**  
- Perform frequency analysis on the encrypted files.  
- Break the substitution cipher to decode the password.  

---

## 🚀 **Solution**  

### **Step 1: Connect to the Server**  
Use the following SSH command to connect to the server:

```bash
ssh krypton3@krypton.labs.overthewire.org -p 2231
```

- **Username:** `krypton3`  
- **Password:** `CAESARISEASY`  

---

### **Step 2: Locate the Password File**  
Navigate to the `krypton3` folder:

```bash
cd /krypton/krypton3
ls -la
```

**Output:**  
You will see the following files:
- `found1`  
- `found2`  
- `found3`  
- `krypton4`  
- `README`  

![ls-la](https://github.com/user-attachments/assets/b881a3ec-081f-43ff-86f0-7fcc2d3473a1)

---

### **Step 3: Read the README File**  
The README file states that the cipher is a **substitution cipher**:

```bash
cat README
```

![Readme](https://github.com/user-attachments/assets/0fce5541-da37-465a-99c7-bb2eef6837b0)

📌 **Key Insight:**  
- A substitution cipher replaces each letter with another fixed letter based on a key.  
- The key is consistent across all intercepted messages (`found1`, `found2`, `found3`).  

---

### **Step 4: Perform Frequency Analysis**  
Since the messages are in English, we can apply **frequency analysis**:

1. Count the frequency of each letter in the encrypted files:

```bash
for i in {A..Z}; do printf $i; cat found1 found2 found3 | tr -cd $i | wc -c; done
```

**Output Example:**
```
A 55  
B 246  
C 227  
...
```
![image](https://github.com/user-attachments/assets/d8fabf12-40ae-4d0b-85cc-a625e9b067e0)


2. Sort the frequency from highest to lowest:

```bash
for i in {A..Z}; do cat found1 found2 found3 | tr -cd $i | wc -c | tr -d '\n'; printf " $i \n"; done | sort -nr
```

**Output Example:**
```
456 S  
340 Q  
227 C  
...
```

![sorted](https://github.com/user-attachments/assets/0ee8c96c-2044-4592-877d-938d0afb158f)


📌 **Key Insight:**  
- The most frequent letter in English is **E**.  
- The most frequent letter in the ciphertext is **S** → Likely that **S = E**.  

---

### **Step 5: Build a Frequency Mapping**  
Use the standard English letter frequency:

```
ETAOINSHRDLCUMFWYGPBVKXQJZ
```

Match the highest frequency cipher letters to this order:

| Cipher | English |  
|--------|---------|  
| S      | E       |  
| Q      | T       |  
| J      | A       |  
| ...    | ...     |  

---

### **Step 6: Decode the Password**  
Use the `tr` command to substitute the characters:

1. Initial attempt:

```bash
cat krypton4 | tr 'SQJUBNGCDZVWMYTXKELAFIORHP' 'ETAOINSRHDLUCMFYWGPBVKXQJZ'
```

**Output:**  
```bash
WELLI ELSA ELLEE LYICN MTOOW INURO BNCAE
```

![output1](https://github.com/user-attachments/assets/1ed82cb5-2a57-434d-ad5e-6d70e1894748)


📌 **Insight:**  
- This didn't fully work — frequency analysis is an approximation.  

2. After adjusting some characters based on context:

```bash
cat krypton4 | tr 'SQJUBNGCDZVWMYTXKELAFIORHP' 'EATSORNIHCLDUPYFWGMBKVXQJZ'
```

**Output:**  
```bash
WELL DONE ELEVEN LFOUR PASSW ORDIS BRUTE
```

✅ The decoded password is:

```bash
BRUTE
```

![Password](https://github.com/user-attachments/assets/30b1ee92-4807-4747-b3a3-676f3156b358)

---

## ✅ **Password for Krypton Level 4**  
```bash
BRUTE
```

---

## 🌟 **Key Points**  
✔️ Used frequency analysis to determine the most common letters.  
✔️ Matched the cipher frequency to the English frequency order.  
✔️ Adjusted the mapping manually based on context.  

---

## 🎯 **Next Level**  
Use the password to access **Krypton Level 4**.  

---
