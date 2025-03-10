# OverTheWire Bandit CTF – Level 16

## 🏆 **Goal**  
The goal of Bandit Level 16 is to find the password for the next level by connecting to an open port on **localhost** using SSL/TLS encryption.  

---

## 🚀 **Steps to Solve**

### 1. **Connect via SSH**  
Use the password obtained from Level 15 to log into **bandit16** using SSH:

```bash
ssh bandit16@bandit.labs.overthewire.org -p 2220
```

- **Username:** bandit16  
- **Hostname:** bandit.labs.overthewire.org  
- **Port:** 2220  

When prompted, enter the password from Level 15:

```
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
```

---

### 2. **Find Open Ports**  
Use `nmap` to scan for open ports between **31000–32000** on localhost:

```bash
nmap -p31000-32000 --open -sV localhost
```

Example output:
```
31790/tcp open  ssl/unknown
```

---

### 3. **Connect to the SSL Port**  
Use `openssl` to connect to the open SSL port:

```bash
openssl s_client -connect localhost:31790 -quiet
```

When prompted, enter the password from Level 15.

---

### 4. **Retrieve the Private Key**  
After submitting the password, you will receive an SSH private key. Save this key to a file named `sshkey17.private`:

```bash
nano sshkey17.private
```

Paste the private key into the file, then save and exit.  

Set the correct permissions for the private key:

```bash
chmod 600 sshkey17.private
```

---

### 5. **Use the Private Key to Log into the Next Level**  
Use the private key to connect to **bandit17**:

```bash
ssh -i sshkey17.private bandit17@bandit.labs.overthewire.org -p 2220
```

---

## 📸 **Screenshot**  
![Level-16](https://github.com/user-attachments/assets/83d8437f-df82-4056-ab84-123e68074bf7)
![Level-16](https://github.com/user-attachments/assets/5fa47a5b-a926-4aa3-afd1-b636c79ac4ba)


---

## 🔑 **Password for Next Level**  
The private key will allow you to log into **Level 17**.

---

## ✅ **Summary**  
✔️ Connected to the server using SSH.  
✔️ Scanned ports with `nmap` to identify the correct SSL port.  
✔️ Used `openssl` to retrieve the private key.  
✔️ Saved the key and set correct permissions.  
✔️ Successfully logged into Level 17 using the private key!  

---

**Next Step:** Proceed to [Level 17](https://overthewire.org/wargames/bandit/bandit17.html) to continue the challenge.  

---

This should work perfectly! Let me know if you need to adjust anything. 😎
