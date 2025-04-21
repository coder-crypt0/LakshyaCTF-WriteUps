# Does **** Matter? - Steganography

**Level: Medium**

## Challenge Description: 

You got an image. It looks... normal. But someone swears the flag is hidden in the **** of it.

Whatever that means.

Maybe it's time to ask yourself: Does **** matters?

Flag Format: LakshyaCTF{}


## Files Provided:
_(Valorant Characters)_
- `Bhagoda.png`  
- `Chall_Hatt.png`  
- `Fade.png`  
- `I_Miss_Her.png`  
- `Monster.png`  
- `Reyna.png`

![image](https://github.com/user-attachments/assets/76c8ed00-3fe0-45d6-ad67-e919cb09acb5)


## Analysis:
Each image seemed fairly ordinary. A reverse image search and basic stego tools didn’t yield anything useful.

We ran `zsteg` to check if any hidden text was in the images.
Results:
  - Some images showed repeated letters like "E", "T", "5".
  - Others had weird file headers like GTA audio index data, or Photoshop color swatch.
  - A few had short strings like "K\`Zw!.4v"and"+))cehsI"`.

But could not get to anything useful like a flag. So we moved on to checking dimensions:

Then we looked into the image dimensions:

```bash
Image Size                      : 121x89
Image Size                      : 118x105
Image Size                      : 79x98
Image Size                      : 111x117
Image Size                      : 115x108
Image Size                      : 101x115
```

Collecting all dimension values and running the following script:

```python
# This script converts image size numbers into characters using `chr()` i.e. using the numbers as ASCII value.

for i in [121,89,118,105,79,98,111,117,115,108,101,115]:
    print(chr(i), end='')
```

Output:  
```
yYviObousles
```

At first, we thought this was the flag, but it didn’t work.

**What worked?**: Rearranging the characters manually we got something more readable - `ObviouslyYes`.

This seemed to be the answer to the question asked in the challenge name:  
- _"Does **** Matter?"_
→ _Obviously Yes!_


## Flag:
```
LakshyaCTF{ObviouslyYes}
```
