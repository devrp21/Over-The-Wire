# OverTheWire Bandit CTF – Level 30

## 🏆 **Goal**  
The goal of Bandit Level 30 is to clone a Git repository, investigate Git tags, and retrieve the password for **bandit31**.

---

## 🚀 **Steps to Solve**

### 1. **Connect via SSH**  
Use the password obtained from Level 29 to log into **bandit30** using SSH:

```bash
ssh bandit30@bandit.labs.overthewire.org -p 2220
```

- **Username:** bandit30  
- **Hostname:** bandit.labs.overthewire.org  
- **Port:** 2220  

When prompted, enter the password from Level 29:

```
qp30ex3VLz5MDG1n91YowTv4Q8l7CDZL
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
Clone the repository hosted at **ssh://bandit30-git@localhost** using port **2220**:

```bash
git clone ssh://bandit30-git@localhost:2220/home/bandit30-git/repo
```

When prompted, use the **same password** as for bandit30.

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

### 5. **Check Git Tags**  
Check for existing tags:

```bash
git tag
```

Example output:
```
secret
```

---

### 6. **Inspect the Tag**  
Show the contents of the `secret` tag:

```bash
git show secret
```

Example output:
```
The password for bandit31 is: fb5S2xb7bRyFmAvQYQGEqsbhVyJqhnDy
```

---

## 🔑 **Password for Next Level**  
The password for **Level 31** is:

```
fb5S2xb7bRyFmAvQYQGEqsbhVyJqhnDy
```

---

## ✅ **Summary**  
✔️ Connected to the server using SSH.  
✔️ Cloned the Git repository.  
✔️ Checked for Git tags.  
✔️ Found the password in the `secret` tag.  

---

## 📸 **Screenshot**  
![Level-30](https://github.com/user-attachments/assets/3404a9c3-df5f-449a-bdd4-9db4697dde7f)<br/>
![Level-30](https://github.com/user-attachments/assets/cdec92e0-8e95-43e9-b7f8-da5fb52fcc8f)<br/>
![Level-30](https://github.com/user-attachments/assets/b2edc801-8285-437f-aabe-582955859a51)


---

**Next Step:** Proceed to [Level 31](https://overthewire.org/wargames/bandit/bandit31.html) to continue the challenge.  

