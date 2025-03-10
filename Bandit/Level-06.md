
# OverTheWire Bandit CTF – Level 6

## 🏆 **Goal**  
The goal of Bandit Level 6 is to find the password for the next level stored somewhere on the server that meets the following criteria:  
✔️ Owned by user **bandit7**  
✔️ Owned by group **bandit6**  
✔️ Exactly **33 bytes** in size  

---

## 🚀 **Steps to Solve**

### 1. **Connect via SSH**  
Use the password obtained from Level 5 to log into **bandit6** using SSH:

```bash
ssh bandit6@bandit.labs.overthewire.org -p 2220
```

- **Username:** bandit6  
- **Hostname:** bandit.labs.overthewire.org  
- **Port:** 2220  

When prompted, enter the password from Level 5:

```
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```

---

### 2. **Find the Correct File**  
To find the file that matches all the specified criteria, use the `find` command:

```bash
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

Explanation:
- `/` → Search from the root directory  
- `-type f` → Search for files  
- `-user bandit7` → Owned by user bandit7  
- `-group bandit6` → Owned by group bandit6  
- `-size 33c` → Exactly 33 bytes  
- `2>/dev/null` → Suppress permission denied errors  

Example output:
```
/var/lib/dpkg/info/bandit7.password
```

---

### 3. **Read the Password**  
Use `cat` to read the contents of the file:

```bash
cat /var/lib/dpkg/info/bandit7.password
```

Output:
```
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
```

---

## 📸 **Screenshot**  
![Level-6](https://github.com/user-attachments/assets/8de8c708-1b74-4c32-95d1-b37d2659530a)


---

## 🔑 **Password for Next Level**  
The password for **Level 7** is:

```
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
```

---

## ✅ **Summary**  
✔️ Connected to the server using SSH.  
✔️ Used `find` to search for the file matching the specific size, user, and group criteria.  
✔️ Retrieved the password for Level 7!  

---

**Next Step:** Proceed to [Level 7](https://overthewire.org/wargames/bandit/bandit7.html) to continue the challenge.  

---
