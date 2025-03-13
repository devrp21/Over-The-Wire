# OverTheWire Bandit CTF – Level 29

## 🏆 **Goal**  
The goal of Bandit Level 29 is to clone a Git repository, explore its branches, and retrieve the password for **bandit30**.

---

## 🚀 **Steps to Solve**

### 1. **Connect via SSH**  
Use the password obtained from Level 28 to log into **bandit29** using SSH:

```bash
ssh bandit29@bandit.labs.overthewire.org -p 2220
```

- **Username:** bandit29  
- **Hostname:** bandit.labs.overthewire.org  
- **Port:** 2220  

When prompted, enter the password from Level 28:

```
4pT1t5DENaYuqnqvadYs1oE4QLCdjmJ7
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
Clone the repository hosted at **ssh://bandit29-git@localhost** using port **2220**:

```bash
git clone ssh://bandit29-git@localhost:2220/home/bandit29-git/repo
```

When prompted, use the **same password** as for bandit29.

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

Open the `README` file:

```bash
cat README
```

Example output:
```
There is no password here.
```

---

### 5. **Check Git Branches**  
Check for available branches:

```bash
git branch -a
```

Example output:
```
* main
  remotes/origin/dev
```

---

### 6. **Switch to the Development Branch**  
Checkout the `dev` branch:

```bash
git checkout dev
```

Example output:
```
Switched to branch 'dev'
```

---

### 7. **Find the Password**  
List the files:

```bash
ls -la
```

Example output:
```
README.md
```

Open the `README.md` file:

```bash
cat README.md
```

Example output:
```
The password for bandit30 is: qp30ex3VLz5MDG1n91YowTv4Q8l7CDZL
```

---

## 🔑 **Password for Next Level**  
The password for **Level 30** is:

```
qp30ex3VLz5MDG1n91YowTv4Q8l7CDZL
```

---

## ✅ **Summary**  
✔️ Connected to the server using SSH.  
✔️ Cloned the Git repository.  
✔️ Checked the branches and switched to `dev`.  
✔️ Found the password in the `README.md` file.  

---

## 📸 **Screenshot**  
![Level-29](https://github.com/user-attachments/assets/cf827339-5f9a-4bdc-a947-64ef1179b185)
![Level-29](https://github.com/user-attachments/assets/dd44bbe5-a7fe-4f38-b0d1-8c1e87c9a34e)
![Level-29](https://github.com/user-attachments/assets/9c29a6f2-67e5-48fe-8b22-65865ca01b8f)


---

**Next Step:** Proceed to [Level 30](https://overthewire.org/wargames/bandit/bandit30.html) to continue the challenge.  

---
