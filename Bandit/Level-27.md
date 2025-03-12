# OverTheWire Bandit CTF – Level 27

## 🏆 **Goal**  
The goal of Bandit Level 27 is to clone a Git repository, explore its contents, and retrieve the password for **bandit28**.

---

## 🚀 **Steps to Solve**

### 1. **Connect via SSH**  
Use the password obtained from Level 26 to log into **bandit27** using SSH:

```bash
ssh bandit27@bandit.labs.overthewire.org -p 2220
```

- **Username:** bandit27  
- **Hostname:** bandit.labs.overthewire.org  
- **Port:** 2220  

When prompted, enter the password from Level 26:

```
upsNCc7vzaRDx6oZC6GiR6ERwe1MowGB
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
Clone the repository hosted at **ssh://bandit27-git@localhost** using port **2220**:

```bash
git clone ssh://bandit27-git@localhost:2220/home/bandit27-git/repo
```

When prompted, use the **same password** as for bandit27.

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

### 5. **Read the Password**  
Open the `README` file to reveal the password for **bandit28**:

```bash
cat README
```

Example output:
```
Yz9IpL0sBcCeuG7m9uQFt8ZNpS4HZRcN
```

---

## 🔑 **Password for Next Level**  
The password for **Level 28** is:

```
Yz9IpL0sBcCeuG7m9uQFt8ZNpS4HZRcN
```

---

## ✅ **Summary**  
✔️ Connected to the server using SSH.  
✔️ Cloned the Git repository.  
✔️ Retrieved the password from the README file.  

---

## 📸 **Screenshot**  
![Level-27](https://github.com/user-attachments/assets/254cf702-7646-43b4-9066-c80df8fdeb20)
![Level-27](https://github.com/user-attachments/assets/4bb09589-58d6-4139-88a6-a77c63a4490d)

---

**Next Step:** Proceed to [Level 28](https://overthewire.org/wargames/bandit/bandit28.html) to continue the challenge.  

---
