---

# OverTheWire Bandit CTF – Level 15

## 🏆 **Goal**  
The goal of Bandit Level 15 is to find the password for the next level by submitting the current level's password to **port 30001** on **localhost** using **SSL/TLS encryption**.

---

## 🚀 **Steps to Solve**

### 1. **Connect via SSH**  
Use the password obtained from Level 14 to log into **bandit15** using SSH:

```bash
ssh bandit15@bandit.labs.overthewire.org -p 2220
```

- **Username:** bandit15  
- **Hostname:** bandit.labs.overthewire.org  
- **Port:** 2220  

When prompted, enter the password from Level 14:

```
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
```

---

### 2. **Connect to Port 30001 Using SSL/TLS**  
Use the `openssl s_client` command to connect to **localhost** on **port 30001** using SSL/TLS:

```bash
openssl s_client -connect localhost:30001
```

---

### 3. **Submit the Password**  
Once connected, submit the password for **Level 15**:

```
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
```

Example output:
```
Correct!
The password for bandit16 is:
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
```

---

### 4. **Disconnect**  
Press **CTRL + D** or **CTRL + C** to close the connection.

---

## 📸 **Screenshot**  
![Level-15](https://github.com/user-attachments/assets/2a2af698-8e7c-4d9f-8d74-8479774df967)
![Level-15](https://github.com/user-attachments/assets/d6786fed-c455-443b-ac3a-ba46ff963982)


---

## 🔑 **Password for Next Level**  
The password for **Level 16** is:

```
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
```

---

## ✅ **Summary**  
✔️ Connected to the server using SSH.  
✔️ Used `openssl s_client` to connect to port 30001 on localhost.  
✔️ Submitted the password for Level 15.  
✔️ Retrieved the password for Level 16!  

---

**Next Step:** Proceed to [Level 16](https://overthewire.org/wargames/bandit/bandit16.html) to continue the challenge.  

---
