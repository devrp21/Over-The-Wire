Here's the updated README for **Level 8**:

---

# OverTheWire Bandit CTF – Level 8

## 🏆 **Goal**  
The goal of Bandit Level 8 is to find the password for the next level stored in the file called `data.txt` that is the only line of text that occurs **only once**.  

---

## 🚀 **Steps to Solve**

### 1. **Connect via SSH**  
Use the password obtained from Level 7 to log into **bandit8** using SSH:

```bash
ssh bandit8@bandit.labs.overthewire.org -p 2220
```

- **Username:** bandit8  
- **Hostname:** bandit.labs.overthewire.org  
- **Port:** 2220  

When prompted, enter the password from Level 7:

```
dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
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

### 3. **Find the Unique Line**  
Use `sort` and `uniq` to find the only line that occurs once:

```bash
sort data.txt | uniq -u
```

Explanation:
- `sort` → Sorts the file lines alphabetically  
- `uniq -u` → Displays only the lines that appear once  

Example output:
```
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```

---

### 4. **Extract the Password**  
The password is the unique line:

```
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```

---

## 📸 **Screenshot**  
*Add screenshot here:*  
![Screenshot](path/to/screenshot.png)

---

## 🔑 **Password for Next Level**  
The password for **Level 9** is:

```
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```

---

## ✅ **Summary**  
✔️ Connected to the server using SSH.  
✔️ Used `sort` and `uniq` to filter out the unique line.  
✔️ Retrieved the password for Level 9!  

---

**Next Step:** Proceed to [Level 9](https://overthewire.org/wargames/bandit/bandit9.html) to continue the challenge.  

---
