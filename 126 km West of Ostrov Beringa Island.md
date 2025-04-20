## Challenge: 126 km West of Ostrov Beringa Island 
![wow](https://github.com/user-attachments/assets/29580e4e-951e-4487-8e99-cdbf7bb00394)


### Description:
This challenge, titled **"126 km West of Ostrov Beringa Island"**, involved analyzing a file named `wow.jpg`. Initially, the image seemed like an ordinary JPEG, but a closer look revealed that there was hidden data embedded within it. The challenge was centered around **Steganography**, where the objective was to extract a hidden message or flag from the image.

### Step 1: Extracting the Password
Upon using the `stegseek` tool, I was able to uncover a password embedded in the image, which was **seismograph**. This password was essential to unlocking further data concealed within the image file.

### Step 2: Retrieving the Hidden Flag File
Using the extracted password, I accessed a hidden file named `flag.txt` from the image. Inside the file, I found the following encoded string: 
[flag.txt](https://github.com/user-attachments/files/19826609/flag.txt)


```4HE1o6T_Ev8]k#!X5f$HsB+R(@FciA]]-?QEO>a:#1Ez&pZZ5'[_o9T_F!8]AN!X6*$Hjv+EDLH.$naI-?s{O>+1#5i@```

This string was not immediately readable, so I proceeded to decode it to uncover the flag.

### Step 3: Base92 Decoding
The first step in decoding the string was to convert it from Base92 encoding. After running the string through a Base92 decoder, I obtained the following HEX-encoded output:

```4c 61 6b 73 68 79 61 43 54 46 7b 53 74 65 67 6f 5f 69 73 5f 68 61 72 64 7d```


### Step 4: HEX Decoding
Next, I applied HEX decoding to the output. This revealed the original flag hidden within the encoded string:
![Screenshot 2025-04-21 002150](https://github.com/user-attachments/assets/b74bafea-9dea-4916-b764-06021483a8e0)

## Flag
<prev>```LakshyaCTF{Stego_is_hard}```</prev>
