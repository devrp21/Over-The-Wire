# OverTheWire Bandit CTF – Level 28

## 🏆 **Goal**  
The goal of Bandit Level 28 is to clone a Git repository, explore its history, and retrieve the password for **bandit29**.

---

## 🚀 **Steps to Solve**

### 1. **Connect via SSH**  
Use the password obtained from Level 27 to log into **bandit28** using SSH:

```bash
ssh bandit28@bandit.labs.overthewire.org -p 2220
```

- **Username:** bandit28  
- **Hostname:** bandit.labs.overthewire.org  
- **Port:** 2220  

When prompted, enter the password from Level 27:

```
Yz9IpL0sBcCeuG7m9uQFt8ZNpS4HZRcN
```

---

### 2. **Create a Temporary Working Directory**  
Create a temporary directory to keep your workspace clean:

```bash
mktemp -d
```

Change into the newly created directory:

```bash
cd /tmp/<your-temp-dir>
```

---

### 3. **Clone the Git Repository**  
Clone the repository hosted at **ssh://bandit28-git@localhost** using port **2220**:

```bash
git clone ssh://bandit28-git@localhost:2220/home/bandit28-git/repo
```

When prompted, use the **same password** as for bandit28.

---

### 4. **Explore the Repository**  
Change into the cloned repository:

```bash
cd repo
```

List the contents:

```bash
ls
```

Example output:
```
README
```

---

### 5. **Read the README File**  
Open the `README` file:

```bash
cat README
```

Example output:
```
The password for the next level is hidden in the git log.
```

---

### 6. **Check Git Logs**  
Check the commit history:

```bash
git log
```

Example output:
```
commit 817e303aa6c2b207ea043c7bba1bb7575dc4ea73 (HEAD -> main)
Author: OverTheWire <overthewire@example.com>
Date:   Mon Jan 1 00:00:00 2025 +0000

    Fixed password leak
```

---

### 7. **Reveal the Hidden Password**  
Show the details of the commit where the password was leaked:

```bash
git show 817e303aa6c2b207ea043c7bba1bb7575dc4ea73
```

Example output:
```bash
+Password: 4pT1t5DENaYuqnqvadYs1oE4QLCdjmJ7
```

---

## 🔑 **Password for Next Level**  
The password for **Level 29** is:

```
4pT1t5DENaYuqnqvadYs1oE4QLCdjmJ7
```

---

## ✅ **Summary**  
✔️ Connected to the server using SSH.  
✔️ Cloned the Git repository.  
✔️ Checked the Git logs and retrieved the leaked password.  

---

## 📸 **Screenshot**  
![Level-28](https://github.com/user-attachments/assets/0ef15d65-45f1-4439-8da0-4fadb00c3257)
![Level-28](https://github.com/user-attachments/assets/94a27439-0624-4df1-972a-ca545d8ebdc2)
![Level-28](https://github.com/user-attachments/assets/78b82647-c2b6-4867-9648-ce57fda68fd2)


---

**Next Step:** Proceed to [Level 29](https://overthewire.org/wargames/bandit/bandit29.html) to continue the challenge.  

---
