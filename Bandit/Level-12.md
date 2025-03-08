---

## **Task**  
The password for the next level is stored in the file `data.txt`, which is a hexdump of a file that has been repeatedly compressed. Your goal is to extract the password by reversing the hexdump and decompressing the file multiple times until you can read the password.

---

## **Step 1: Create a Working Directory and Copy the Data**  
1. Start by creating a temporary working directory in `/tmp` using `mktemp -d`.  
2. Copy `data.txt` from the home directory (`~`) to the working directory.  
3. Rename it to `hexdump_data` for easier reference.

### **Commands:**
```bash
cd /tmp
mktemp -d
cd /tmp/tmp.XXXXXXXX
cp ~/data.txt .
mv data.txt hexdump_data
ls
```

---

## **Step 2: Reverse the Hexdump**  
1. Use `xxd -r` to convert the hexdump back to binary format.  
2. Save the output as `compressed_data`.

### **Commands:**
```bash
xxd -r hexdump_data compressed_data
ls
```

---

## **Step 3: Identify and Decompress the File**  
Use the `file` command or look at the file signature using `xxd` to identify the file type.

---

### ✅ **First Compression Type → GZIP**  
- GZIP files start with the magic number `1F 8B`.  
- Rename the file to `compressed_data.gz` and use `gzip -d` to decompress it.

**Commands:**
```bash
mv compressed_data compressed_data.gz
gzip -d compressed_data.gz
ls
```

---

### ✅ **Second Compression Type → BZIP2**  
- BZIP2 files start with the magic number `42 5A`.  
- Rename the file to `compressed_data.bz2` and use `bzip2 -d` to decompress it.

**Commands:**
```bash
mv compressed_data compressed_data.bz2
bzip2 -d compressed_data.bz2
ls
```

---

### ✅ **Third Compression Type → GZIP**  
- After decompression, it's still GZIP-compressed.  
- Rename and decompress again.

**Commands:**
```bash
mv compressed_data compressed_data.gz
gzip -d compressed_data.gz
ls
```

---

### ✅ **Fourth Compression Type → TAR Archive**  
- If you see file names inside the output (like `data5.bin`), it's likely a TAR archive.  
- Rename it and extract it using `tar -xf`.

**Commands:**
```bash
mv compressed_data compressed_data.tar
tar -xf compressed_data.tar
ls
```

---

### ✅ **Fifth Compression Type → TAR Archive**  
- The extracted `data5.bin` is another TAR archive.  
- Extract it using `tar`.

**Commands:**
```bash
tar -xf data5.bin
ls
```

---

### ✅ **Sixth Compression Type → BZIP2**  
- The extracted `data6.bin` is BZIP2-compressed.  
- Decompress it.

**Commands:**
```bash
bzip2 -d data6.bin
ls
```

---

### ✅ **Seventh Compression Type → TAR Archive**  
- The extracted `data6.bin.out` is another TAR archive.  
- Extract it using `tar`.

**Commands:**
```bash
tar -xf data6.bin.out
ls
```

---

### ✅ **Eighth Compression Type → GZIP**  
- The extracted file is GZIP-compressed.  
- Rename and decompress it.

**Commands:**
```bash
mv data7.bin data7.gz
gzip -d data7.gz
ls
```

---

### ✅ **Final Step → Read the Password**  
After the final decompression, the password should be visible in the extracted file. Use `cat` to display the password:

**Command:**
```bash
cat final_file
```

---

## ✅ **Summary of Commands**  
```bash
cd /tmp
mktemp -d
cd /tmp/tmp.XXXXXXXX
cp ~/data.txt .
mv data.txt hexdump_data
xxd -r hexdump_data compressed_data

mv compressed_data compressed_data.gz
gzip -d compressed_data.gz

mv compressed_data compressed_data.bz2
bzip2 -d compressed_data.bz2

mv compressed_data compressed_data.gz
gzip -d compressed_data.gz

mv compressed_data compressed_data.tar
tar -xf compressed_data.tar

tar -xf data5.bin

bzip2 -d data6.bin

tar -xf data6.bin.out

mv data7.bin data7.gz
gzip -d data7.gz

cat final_file
```

---

## 📸 **Screenshot**  
![Level-12](https://github.com/user-attachments/assets/4c3fe9f8-4fc9-4557-ac34-77d7362cd901)


---

## 🔑 **Password for Next Level**  
The password for **Level 13** is:

```
7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```

--- 

**Next Step:** Proceed to [Level 13](https://overthewire.org/wargames/bandit/bandit13.html) to continue the challenge.  

---
