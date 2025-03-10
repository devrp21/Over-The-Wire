
# OverTheWire Bandit CTF – Level 7

## 🏆 **Goal**  
The goal of Bandit Level 7 is to find the password for the next level stored in a file called `data.txt` next to the word **"millionth."**  

---

## 🚀 **Steps to Solve**

### 1. **Connect via SSH**  
Use the password obtained from Level 6 to log into **bandit7** using SSH:

```bash
ssh bandit7@bandit.labs.overthewire.org -p 2220
```

- **Username:** bandit7  
- **Hostname:** bandit.labs.overthewire.org  
- **Port:** 2220  

When prompted, enter the password from Level 6:

```
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
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

### 3. **Search for the Password**  
Use `grep` to search for the word **"millionth"** in `data.txt`:

```bash
grep 'millionth' data.txt
```

Example output:
```
millionth:dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```

---

### 4. **Extract the Password**  
The password is the value next to the word **"millionth."**  
In this case:

```
dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```

---

## 📸 **Screenshot**  
![Level-7](https://github.com/user-attachments/assets/4ff0c719-7ee2-4824-8901-3e60a093f433)


---

## 🔑 **Password for Next Level**  
The password for **Level 8** is:

```
dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```

---

## ✅ **Summary**  
✔️ Connected to the server using SSH.  
✔️ Used `grep` to search for the word **"millionth."**  
✔️ Retrieved the password for Level 8!  

---

**Next Step:** Proceed to [Level 8](https://overthewire.org/wargames/bandit/bandit8.html) to continue the challenge.  

---
