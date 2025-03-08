Here's the updated README treating the flag as the password for the next level:

---

# OverTheWire Bandit CTF – Level 0

## 🏆 **Goal**
The goal of Bandit Level 0 is to log into the game using SSH and retrieve the password for the next level stored in a file named `readme`.

---

## 🚀 **Steps to Solve**

### 1. **Connect via SSH**
To connect to the Bandit server, use the following command:

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

- `bandit0` – Username  
- `bandit.labs.overthewire.org` – Hostname  
- `-p 2220` – Port number  

When prompted, enter the password:  
**Password:** `bandit0`

---

### 2. **List Files in the Directory**
Once logged in, list the files in the current directory using:

```bash
ls
```

Output:
```
readme
```

---

### 3. **Read the Password**
Use the `cat` command to display the contents of the `readme` file:

```bash
cat readme
```

Output:
```
ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
```

---

## 🔑 **Password for Next Level**
The password for **Level 1** is:

```
ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
```

---

## ✅ **Summary**
- Connected to the server using SSH.  
- Listed files using `ls`.  
- Retrieved the password using `cat`.  
- Successfully completed Level 0 and obtained the password for Level 1!  

---

**Next Step:** Proceed to [Level 1](https://overthewire.org/wargames/bandit/bandit1.html) to continue the challenge.  

---

Let me know if this works! 😎