# 🔐 Crackk It

> **Challenge Description:**  
> In this challenge, your task is to crack multiple layers of encryption to retrieve the hidden flag. The challenge consists of a password-protected ZIP file and a locked PDF document, requiring a combination of brute-force techniques and strategic decryption methods.

---

## 🧩 Step 1: Cracking the ZIP File with Kali Linux

We were provided with:

- `flag.zip` (password-protected ZIP file)
- `file1.txt and file2.txt` (list of possible passwords)

### 🔍 Analysis

On inspecting `file1.txt`, it became apparent that it was a password list. Many of the entries contained a repeated pattern, such as:

1337h4x0r 1337h4x0r10 1337h4x0r25 ...



This suggested a likely candidate for the ZIP password. On Kali Linux, we used a simple Python script to automate the brute-force:

### 🐍 Python Script

```python
from zipfile import ZipFile

with open("file1.txt", "r") as f:
    passwords = [line.strip() for line in f]

for pwd in passwords:
    try:
        with ZipFile("flag.zip") as zf:
            zf.extractall(pwd=bytes(pwd, 'utf-8'))
            print(f"[+] Password found: {pwd}")
            break
    except:
        continue
```

✅ Result

## [+] Password found: 
```1337h4x0r```

## 📄 Step 2: Cracking the Locked PDF using pdfcrack
The flag.pdf was still encrypted. This time, we used another Kali Linux tool — pdfcrack — which is designed specifically for PDF password brute-forcing.

We examined file2.txt, which contained hundreds of permutations of usernames such as:

noobmaster
noobmast96
noobmast31
noobmaster98
...


## 🛠️ Command Used 
pdfcrack -f flag.pdf -w file2.txt


## PDF Password Found:
Found user-password: ```noobmast96```


## Flag
```LakshyaCTF{n00bz{CR4CK3D_4ND_CR4CK3D_1a4d2e5f}}```


![Screenshot 2025-04-21 000217](https://github.com/user-attachments/assets/8f8b0223-9af7-4a00-a994-8d5a625f559f)
