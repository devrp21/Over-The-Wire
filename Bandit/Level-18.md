
# OverTheWire Bandit CTF – Level 18

## 🏆 **Goal**  
The goal of Bandit Level 18 is to find the password for the next level stored in a file called **readme** in the home directory. However, someone has modified the `.bashrc` file to log you out immediately upon logging in via SSH.  

---

## 🚀 **Steps to Solve**

### 1. **Connect via SSH**  
If you try to log in normally, you will be logged out immediately with a "Bye Bye!" message:

```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220
```

Output:
```
Bye Bye!
```

---

### 2. **Bypass Logout Using a Command**  
To bypass the `.bashrc` logout, execute a command directly in the SSH connection. Use the `ls` command to list the files:

```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220 ls
```

Example output:
```
readme
```

---

### 3. **Read the Password**  
Use the `cat` command to display the contents of the `readme` file directly via SSH:

```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme
```

Example output:
```
cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8
```

---

## 📸 **Screenshot**  
![Level-18](https://github.com/user-attachments/assets/2b981b32-dc62-4db6-8416-5c4c498285af)
![Level-18](https://github.com/user-attachments/assets/791b7d46-5c07-46d7-9b9d-f8cf15c73e2e)
![Level-18](https://github.com/user-attachments/assets/d7f9816e-939c-4bf5-83a7-37d8c6f50006)


---

## 🔑 **Password for Next Level**  
The password for **Level 19** is:

```
cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8
```

---

## ✅ **Summary**  
✔️ Connected to the server using SSH.  
✔️ Bypassed the `.bashrc` logout using direct command execution.  
✔️ Retrieved the password for Level 19!  

---

**Next Step:** Proceed to [Level 19](https://overthewire.org/wargames/bandit/bandit19.html) to continue the challenge.  

---
