# Hello World - Reverse Engineering

## Challenge Name: Hello World

## Description
Jaisa dikhta hai waisa hota hai nahi.
Ek compiled binary diya gaya hai jisme ek certain string form mein memory mein embedded hai—lekin direct-readable format mein nahi. Program khud ek standard output call use karta hai jo is constant ko runtime pe reveal karta hai.
Dekhte hain aap kitne ache se binary ki antar-atma tak pahunch paate ho. Bas dhyaan rahe: kuch cheezein encoded mein chipki hui hain, aur shabd kuch aise hain jo turant samajh nahi aayenge... unless you know where to look

(hello.exe)

## Tools Used
- IDA Pro (Interactive Disassembler)

## Analysis Process

### Initial Reconnaissance
Upon receiving the challenge file, I started by examining the binary using IDA Pro, which allowed me to decompile and analyze the executable's code structure.

### Finding the Hidden Flag
After loading the binary in IDA Pro, I began exploring different functions and sections of the code. During my analysis, I came across a particularly interesting function called `_hiddenflag`.

In this function, I discovered a series of `mov` instructions that were initializing a buffer in memory. These instructions were sequentially adding ASCII values to adjacent memory locations:

```assembly
mov     [ebp+var_25], 4Ch ; 'L'
mov     [ebp+var_24], 61h ; 'a'
mov     [ebp+var_23], 6Bh ; 'k'
mov     [ebp+var_22], 73h ; 's'
mov     [ebp+var_21], 68h ; 'h'
mov     [ebp+var_20], 79h ; 'y'
mov     [ebp+var_1F], 61h ; 'a'
mov     [ebp+var_1E], 43h ; 'C'
mov     [ebp+var_1D], 54h ; 'T'
mov     [ebp+var_1C], 46h ; 'F'
mov     [ebp+var_1B], 7Bh ; '{'
mov     [ebp+var_1A], 68h ; 'h'
mov     [ebp+var_19], 69h ; 'i'
mov     [ebp+var_18], 64h ; 'd'
mov     [ebp+var_17], 64h ; 'd'
mov     [ebp+var_16], 65h ; 'e'
mov     [ebp+var_15], 6Eh ; 'n'
mov     [ebp+var_14], 5Fh ; '_'
mov     [ebp+var_13], 66h ; 'f'
mov     [ebp+var_12], 6Ch ; 'l'
mov     [ebp+var_11], 61h ; 'a'
mov     [ebp+var_10], 67h ; 'g'
mov     [ebp+var_F], 5Fh ; '_'
mov     [ebp+var_E], 68h ; 'h'
mov     [ebp+var_D], 65h ; 'e'
mov     [ebp+var_C], 72h ; 'r'
mov     [ebp+var_B], 65h ; 'e'
mov     [ebp+var_A], 7Dh ; '}'
```

### Decoding the Flag

Looking at the hex values and their corresponding ASCII characters (conveniently commented by IDA), I could see that this was building a string character by character. By assembling the characters in sequence, the hidden flag is revealed:

Hex | ASCII
--- | -----
4Ch | L
61h | a
6Bh | k
73h | s
68h | h
79h | y
61h | a
43h | C
54h | T
46h | F
7Bh | {
68h | h
69h | i
64h | d
64h | d
65h | e
6Eh | n
5Fh | _
66h | f
6Ch | l
61h | a
67h | g
5Fh | _
68h | h
65h | e
72h | r
65h | e
7Dh | }

## The Flag

Putting all these characters together reveals the flag:

```
LakshyaCTF{hidden_flag_here}
```
