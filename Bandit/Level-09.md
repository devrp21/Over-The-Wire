Here's the updated README for **Level 9**:

---

# OverTheWire Bandit CTF – Level 9

## 🏆 **Goal**  
The goal of Bandit Level 9 is to find the password for the next level stored in a file called `data.txt`. The password is located within one of the few human-readable strings, **preceded by several `=` characters**.  

---

## 🚀 **Steps to Solve**

### 1. **Connect via SSH**  
Use the password obtained from Level 8 to log into **bandit9** using SSH:

```bash
ssh bandit9@bandit.labs.overthewire.org -p 2220
```

- **Username:** bandit9  
- **Hostname:** bandit.labs.overthewire.org  
- **Port:** 2220  

When prompted, enter the password from Level 8:

```
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
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

### 3. **Find the Password**  
Use `grep` to search for the string preceded by `=` characters:

```bash
grep -sai "==.*" data.txt
```

Explanation:
- `-s` → Suppress error messages  
- `-a` → Treat the file as text (even if it contains binary data)  
- `-i` → Ignore case  
- `"==.*"` → Match any string starting with `==` followed by any characters  

Example output:
```
==========FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
```

---

### 4. **Extract the Password**  
The password is the readable string following the `=` characters:

```
FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
```

---

## 📸 **Screenshot**  
![Level-9](https://github.com/user-attachments/assets/dc021037-7caa-45d2-972f-aeac52cb9b7a)


---

## 🔑 **Password for Next Level**  
The password for **Level 10** is:

```
FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
```

---

## ✅ **Summary**  
✔️ Connected to the server using SSH.  
✔️ Used `grep` to search for human-readable strings preceded by `=` characters.  
✔️ Retrieved the password for Level 10!  

---

**Next Step:** Proceed to [Level 10](https://overthewire.org/wargames/bandit/bandit10.html) to continue the challenge.  

---
