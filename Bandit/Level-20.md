
# OverTheWire Bandit CTF – Level 20

## 🏆 **Goal**  
The goal of Bandit Level 20 is to find the password for the next level by using a **setuid binary** that connects to localhost on a specified port.  
If the correct password from Level 19 is provided via the connection, the program will return the password for Level 21.  

---

## 🚀 **Steps to Solve**

### 1. **Connect via SSH**  
Use the password obtained from Level 19 to log into **bandit20** using SSH:

```bash
ssh bandit20@bandit.labs.overthewire.org -p 2220
```

- **Username:** bandit20  
- **Hostname:** bandit.labs.overthewire.org  
- **Port:** 2220  

When prompted, enter the password from Level 19:

```
0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
```

---

### 2. **List the Files**  
After logging in, list the files in the home directory:

```bash
ls
```

Example output:
```
suconnect
```

---

### 3. **Set Up a Listening Server**  
Set up a listening server on **port 1234** and pass the current level's password to it using `nc` (Netcat):  

```bash
echo -n '0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO' | nc -l -p 1234 &
```

- `-n` – Ensures no trailing newline is sent.  
- `-l` – Listen mode.  
- `-p` – Specifies the port number.  
- `&` – Runs the command in the background.  

---

### 4. **Execute the SetUID Binary**  
Run the `suconnect` binary and provide the port number where the server is listening:

```bash
./suconnect 1234
```

Example output:
```
EeoULMCra2q0dSkYj561DX7s1CpBuOBt
```

---

## 📸 **Screenshot**  
![Level-20](https://github.com/user-attachments/assets/155e30c4-4fd1-4903-bc15-8a6b5ca287b9)


---

## 🔑 **Password for Next Level**  
The password for **Level 21** is:

```
EeoULMCra2q0dSkYj561DX7s1CpBuOBt
```

---

## ✅ **Summary**  
✔️ Connected to the server using SSH.  
✔️ Set up a listening server using `nc` on port 1234.  
✔️ Provided the correct password from Level 19 via the connection.  
✔️ Retrieved the password for Level 21!  

---

**Next Step:** Proceed to [Level 21](https://overthewire.org/wargames/bandit/bandit21.html) to continue the challenge.  
