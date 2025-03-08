Here's the solution for **Bandit Level 13 → Level 14** following the updated format:

---

# OverTheWire Bandit CTF – Level 13

## 🏆 **Goal**  
The goal of Bandit Level 13 is to find the password for the next level stored in `/etc/bandit_pass/bandit14`. However, you are not directly given the password — instead, you are provided with a **private SSH key** that can be used to log into the next level.

---

## 🚀 **Steps to Solve**

### 1. **Connect via SSH**  
Use the password obtained from Level 12 to log into **bandit13** using SSH:

```bash
ssh bandit13@bandit.labs.overthewire.org -p 2220
```

- **Username:** bandit13  
- **Hostname:** bandit.labs.overthewire.org  
- **Port:** 2220  

When prompted, enter the password from Level 12:

```
FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn
```

---

### 2. **Locate the Private Key**  
Once logged in, list the files in the current directory:

```bash
ls
```

Output:
```
sshkey.private
```

---

### 3. **Copy the Private Key to Local Machine**  
Use `scp` to securely copy the private key to your local machine:

```bash
scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private .
```

---

### 4. **Set Permissions on the Private Key**  
To avoid SSH permission errors, set the correct permissions on the private key:

```bash
chmod 600 sshkey.private
```

---

### 5. **Log Into the Next Level Using the Private Key**  
Use the private key to log into **bandit14**:

```bash
ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
```

---

### 6. **Extract the Password**  
Read the password for the next level from `/etc/bandit_pass/bandit14`:

```bash
cat /etc/bandit_pass/bandit14
```

Example output:
```
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
```

---

## 📸 **Screenshot**  
*Add screenshot here:*  
![Screenshot](path/to/screenshot.png)

---

## 🔑 **Password for Next Level**  
The password for **Level 14** is:

```
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
```

---

## ✅ **Summary**  
✔️ Connected to the server using SSH.  
✔️ Located the private SSH key.  
✔️ Copied the key using `scp`.  
✔️ Set secure permissions on the key.  
✔️ Used the key to log into the next level.  
✔️ Retrieved the password for Level 14!  

---

**Next Step:** Proceed to [Level 14](https://overthewire.org/wargames/bandit/bandit14.html) to continue the challenge.  

---
