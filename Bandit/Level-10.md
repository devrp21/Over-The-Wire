
# OverTheWire Bandit CTF – Level 10

## 🏆 **Goal**  
The goal of Bandit Level 10 is to find the password for the next level stored in a file called `data.txt`. The file contains **base64 encoded data** that needs to be decoded.  

---

## 🚀 **Steps to Solve**

### 1. **Connect via SSH**  
Use the password obtained from Level 9 to log into **bandit10** using SSH:

```bash
ssh bandit10@bandit.labs.overthewire.org -p 2220
```

- **Username:** bandit10  
- **Hostname:** bandit.labs.overthewire.org  
- **Port:** 2220  

When prompted, enter the password from Level 9:

```
FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
```

---

### 2. **Locate the File**  
Once logged in, list the files in the current directory:

```bash
ls
```

Output:
```
data.txt
```

---

### 3. **View the Encoded Data**  
Use `cat` to display the contents of `data.txt`:

```bash
cat data.txt
```

Example output:
```
ZHRSMTczZlprYjBSUnNERlNHc2cyUlducE5WajNxUnI=
```

---

### 4. **Decode the Base64 Data**  
You can decode the base64 data using the `base64` command:

```bash
cat data.txt | base64 -d
```

Alternatively, you can use an online decoder like **https://www.base64decode.org/**.

Example output:
```
dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```

---

### 5. **Extract the Password**  
The decoded output is the password:

```
dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```

---

## 📸 **Screenshot**  
![Level-10](https://github.com/user-attachments/assets/b2a820a0-aade-4522-a986-427788df59b0)
![Level-10](https://github.com/user-attachments/assets/a3bee8ec-1d1d-4161-9ba3-e3a84df141d5)


---

## 🔑 **Password for Next Level**  
The password for **Level 11** is:

```
dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```

---

## ✅ **Summary**  
✔️ Connected to the server using SSH.  
✔️ Viewed the base64 encoded data using `cat`.  
✔️ Decoded the data using `base64` and retrieved the password for Level 11!  

---

**Next Step:** Proceed to [Level 11](https://overthewire.org/wargames/bandit/bandit11.html) to continue the challenge.  

---
