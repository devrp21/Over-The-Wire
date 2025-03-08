Here's the solution for **Bandit Level 14 → Level 15** following the updated format:

---

# OverTheWire Bandit CTF – Level 14

## 🏆 **Goal**  
The goal of Bandit Level 14 is to find the password for the next level by submitting the current level's password to **port 30000** on **localhost**.

---

## 🚀 **Steps to Solve**

### 1. **Connect via SSH**  
Use the password obtained from Level 13 to log into **bandit14** using SSH:

```bash
ssh bandit14@bandit.labs.overthewire.org -p 2220
```

- **Username:** bandit14  
- **Hostname:** bandit.labs.overthewire.org  
- **Port:** 2220  

When prompted, enter the password from Level 13:

```
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
```

---

### 2. **Connect to Port 30000**  
Use `nc` (Netcat) to connect to **localhost** on **port 30000**:

```bash
nc localhost 30000
```

---

### 3. **Submit the Password**  
Once connected, enter the password for **Level 14**:

```
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
```

Example output:
```
Correct! The password for bandit15 is:
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
```

---

### 4. **Disconnect**  
Press **CTRL + D** or **CTRL + C** to close the connection.

---

## 📸 **Screenshot**  
![Level-14](https://github.com/user-attachments/assets/e79317e4-6d9a-40be-9c01-5c13f4410e46)


---

## 🔑 **Password for Next Level**  
The password for **Level 15** is:

```
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
```

---

## ✅ **Summary**  
✔️ Connected to the server using SSH.  
✔️ Used `nc` to connect to port 30000 on localhost.  
✔️ Submitted the password for Level 14.  
✔️ Retrieved the password for Level 15!  

---

**Next Step:** Proceed to [Level 15](https://overthewire.org/wargames/bandit/bandit15.html) to continue the challenge.  

---
