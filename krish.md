# Krish Made It Easy - Writeup

## Challenge Description

**Challenge Name:** Krish Made It Easy  
**Difficulty:** Hard

> "Oh, my God, look at that face You look like my next mistake Love's a game, wanna play?"  
> 
> Hint: The flag may wave in silence, but the comments don't lie. Sometimes, the real message hides below the surface.
>
> Flag Format: LakshyaCTF{Text_number}

## Solution Path

### Step 1: Recognizing the Hidden Message

The challenge started with a quote from Taylor Swift's song "Blank Space." This was our first clue - the reference to "Blank Space" suggested we should focus on whitespace characters, which might not be immediately visible but could contain encoded information.

In the provided `question.txt` file, there appeared to be an abundance of whitespace characters. This confirmed our suspicion that we needed to decode a message hidden in the whitespaces.

### Step 2: Decoding the Whitespace

To decode the whitespace, I used an online tool specifically designed for this purpose: https://www.dcode.fr/whitespace-language

After processing the file through this decoder, we obtained the following riddle:

> In a foggy town where secrets linger, four in ten believe in whispers, while eight in ten hear distant echoes. Yet, among those who believe, three in ten claim to have heard them first. But in this haze of half-truths, tell me--if you hear the echoes, what are the chances you already believed?
> 
> on solving this proceed here -> https://drive.google.com/drive/folders/10q87CQTbXhmiXr__j6RGPK5Ll7Sxvbu5?usp=drive_link

### Step 3: Solving the Probability Riddle

The riddle presented a classic Bayes' Theorem probability problem:

- P(believe) = 0.4 (four in ten believe)
- P(hear) = 0.8 (eight in ten hear echoes)
- P(hear|believe) = 0.3 (among believers, three in ten heard them first)

We need to find P(believe|hear), which is the probability that someone believed given that they hear echoes.

Using Bayes' Theorem:
P(believe|hear) = [P(hear|believe) × P(believe)] / P(hear)
P(believe|hear) = [0.3 × 0.4] / 0.8
P(believe|hear) = 0.12 / 0.8
P(believe|hear) = 0.15 or 15%

### Step 4: Following the Trail to Google Drive

With the answer 0.15 (15%) in hand, I proceeded to the Google Drive link provided in the riddle.

The Google Drive contained a file with a base64 encoded string:
```
aHR0cHM6Ly9yLm10ZHYubWUvN3F2cDNkQzFzZg==
```

### Step 5: Decoding the Base64 String

Decoding this base64 string revealed another URL:
```
https://r.mtdv.me/7qvp3dC1sf
```

### Step 6: The Rickroll and Hidden Clue

Upon visiting this URL, I was presented with a Rickroll video. However, the description contained an important hint:
> Ever felt the urge to do the 'Hand Thing'? Dive into the surreal and let Shaye guide you.

### Step 7: Researching "Hand Thing"

Searching for "Hand Thing" on Google led me to a YouTube video titled "[HAND THING (Original Video)]" by Shaye Saint John - exactly matching our hint.

### Step 8: Finding Krish in the Comments

As suggested by the challenge hint "the comments don't lie," I scrolled through the video comments and found one from a user named KRISH who simply commented "i am here".

### Step 9: Investigating Krish's YouTube Channel

Visiting Krish's YouTube channel, I found a cryptic string in the account description:
```
68747470733a2f2f74696e7975726c2e636f6d2f626d6d6a76776835
```

### Step 10: Decoding the Hex String

This string was hex-encoded. After decoding, it revealed yet another URL:
```
https://tinyurl.com/bmmjvwh5
```

### Step 11: Protected Proton Drive File

This link led to a password-protected file on Proton Drive. After several unsuccessful guesses, I realized we hadn't used the answer to the probability riddle (0.15) yet.

Using 0.15 as the password successfully unlocked the file, which was an image named "InsideImage.jpg".

### Step 12: Analyzing the Image

Upon examining the image's metadata, I discovered its alternate name was "Cicada_3301_logo.jpg", referring to the infamous internet puzzle/recruitment challenge.

## The Flag

Formatting this finding according to the challenge requirements:

```
LakshyaCTF{Cicada_3301}
```
