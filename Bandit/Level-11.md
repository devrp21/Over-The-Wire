Here's the updated README for **Level 11**:

---

# OverTheWire Bandit CTF – Level 11

## 🏆 **Goal**  
The goal of Bandit Level 11 is to find the password for the next level stored in a file called `data.txt`. The contents of the file are encoded using **ROT13** (Caesar cipher with a shift of 13).  

---

## 🚀 **Steps to Solve**

### 1. **Connect via SSH**  
Use the password obtained from Level 10 to log into **bandit11** using SSH:

```bash
ssh bandit11@bandit.labs.overthewire.org -p 2220
```

- **Username:** bandit11  
- **Hostname:** bandit.labs.overthewire.org  
- **Port:** 2220  

When prompted, enter the password from Level 10:

```
dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
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
7k16JArUVv5LxVxJfsSVdbbtaHGtl6D4
```

---

### 4. **Decode Using ROT13**  
Create an alias for the `ROT13` cipher using the `tr` command:

```bash
alias rot13="tr 'a-zA-Z' 'n-za-mN-ZA-M'"
```

Now, decode the file:

```bash
cat data.txt | rot13
```

Example output:
```
7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```

Explanation:
- `tr 'a-zA-Z' 'n-za-mN-ZA-M'` → Translates each letter by rotating it 13 characters forward  

---

### 5. **Extract the Password**  
The decoded output is the password:

```
7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```

---

## 📸 **Screenshot**  
*Add screenshot here:*  
![Screenshot](path/to/screenshot.png)

---

## 🔑 **Password for Next Level**  
The password for **Level 12** is:

```
7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```

---

## ✅ **Summary**  
✔️ Connected to the server using SSH.  
✔️ Viewed the ROT13 encoded data using `cat`.  
✔️ Created an alias for ROT13 and decoded the file using `tr`.  
✔️ Retrieved the password for Level 12!  

---

**Next Step:** Proceed to [Level 12](https://overthewire.org/wargames/bandit/bandit12.html) to continue the challenge.  

---
