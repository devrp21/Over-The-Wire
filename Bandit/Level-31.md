# OverTheWire Bandit CTF – Level 31

## 🏆 **Goal**  
The goal of Bandit Level 31 is to clone a Git repository, bypass a `.gitignore` rule, and retrieve the password for **bandit32**.

---

## 🚀 **Steps to Solve**

### 1. **Connect via SSH**  
Use the password obtained from Level 30 to log into **bandit31** using SSH:

```bash
ssh bandit31@bandit.labs.overthewire.org -p 2220
```

- **Username:** bandit31  
- **Hostname:** bandit.labs.overthewire.org  
- **Port:** 2220  

When prompted, enter the password from Level 30:

```
fb5S2xb7bRyFmAvQYQGEqsbhVyJqhnDy
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
Clone the repository hosted at **ssh://bandit31-git@localhost** using port **2220**:

```bash
git clone ssh://bandit31-git@localhost:2220/home/bandit31-git/repo
```

When prompted, use the **same password** as for bandit31.

---

### 4. **Explore the Repository**  
Change into the cloned repository:

```bash
cd repo
```

List the contents:

```bash
ls -la
```

Example output:
```
total 12
drwxr-xr-x 3 root root 4096 Mar 8 12:34 .
drwxr-xr-x 3 root root 4096 Mar 8 12:34 ..
drwxr-xr-x 8 root root 4096 Mar 8 12:34 .git
-rw-r--r-- 1 root root   36 Mar 8 12:34 README
```

Open the `README` file:

```bash
cat README
```

Example output:
```
There is nothing here.
```

---

### 5. **Create a New File**  
Create a new file named `key.txt` with the content:

```bash
echo 'May I come in?' > key.txt
```

---

### 6. **Check the .gitignore File**  
There is a `.gitignore` file preventing `*.txt` files from being committed.  
You can override it by using the `-f` flag with `git add`:

```bash
git add -f key.txt
```

---

### 7. **Commit the Changes**  
Commit the changes:

```bash
git commit -a -m "Adding key.txt"
```

---

### 8. **Push the Changes**  
Push the changes to the repository:

```bash
git push -u origin master
```

When prompted, enter the **password** for bandit31.

Example output:
```
Counting objects: 3, done.
Writing objects: 100% (3/3), 264 bytes | 264.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
remote: Congratulations! The password for the next level is:
remote: 3O9RfhqyAlVBEZpVb6LYStshZoqoSx5K
```

---

## 🔑 **Password for Next Level**  
The password for **Level 32** is:

```
3O9RfhqyAlVBEZpVb6LYStshZoqoSx5K
```

---

## ✅ **Summary**  
✔️ Connected to the server using SSH.  
✔️ Cloned the Git repository.  
✔️ Overrode `.gitignore` to commit a `.txt` file.  
✔️ Pushed changes to the repository and retrieved the password.  

---

## 📸 **Screenshot**  
![Level-31](https://github.com/user-attachments/assets/04f09280-509a-40e6-9cce-c7cfb642227e)
![Level-31](https://github.com/user-attachments/assets/c849ca12-4126-4ea2-89b3-18036f69465d)
![Level-31](https://github.com/user-attachments/assets/b7afe069-d583-451a-99d2-c67a482d71af)
![Level-31](https://github.com/user-attachments/assets/97fb0fef-d6fe-4cbd-85a4-f3bf1795f927)

---

**Next Step:** Proceed to [Level 32](https://overthewire.org/wargames/bandit/bandit32.html) to continue the challenge.  
