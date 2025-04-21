# Get the Info - OSINT Challenge Writeup

## Challenge Description

I recently took a trip to Washington, D.C., to meet Donald Trump at his residence. After the meeting, we had lunch at a famous Indian restaurant known for its Indian and Nepali cuisine — the kind of place locals rave about. From there, we walked to a nearby art gallery, all within a 0.3 mile radius. That's where I saw a ceramic sculpture that completely captivated me. The artist, known for her ceramic work and she also told me that she is having an exhibition there on March 26. I really wanted to contact her to inquire about purchasing the piece, but I lost her details. Can you help me find the email address of the artist?

Flag Format: LakshyaCTF{email@gmail.com}

## Solution Approach

### Step 1: Identifying the Restaurant

The first key element in this OSINT challenge was identifying the Indian restaurant mentioned in the description. We needed to find a restaurant in Washington, D.C. that:
- Serves both Indian and Nepali cuisine
- Is popular among locals
- Is located near Donald Trump's residence in D.C.

A Google search for "famous Indian and Nepali restaurant Washington DC" led me to **Himalayan Doko**, a well-known restaurant serving authentic Indian and Nepali cuisine in the D.C. area.

### Step 2: Finding the Art Gallery

According to the challenge description, the art gallery is within a 0.3-mile radius of the restaurant. Using Google Maps, I searched for art galleries near Himalayan Doko and found **Touchstone Gallery** to be the most prominent art gallery within the specified distance.

### Step 3: Researching Current Exhibitions

Since the challenge mentioned that the artist was having an exhibition starting on March 26, I visited the Touchstone Gallery's website to check their exhibition schedule. The gallery indeed had a ceramic art exhibition that began on March 26, confirming this was the right location.

### Step 4: Identifying the Artist

On the gallery's website, I found information about the ceramic exhibition and learned that the featured artist was **Elena Tchernomazova**, who specializes in ceramic sculptures - matching the description in the challenge.

### Step 5: Finding the Artist's Email

To find Elena Tchernomazova's email address, I conducted further research:
- Checked the gallery's website for artist contact information
- Searched social media platforms where artists typically promote their work
- Looked for the artist's personal website or portfolio

Through this research, I discovered that Elena Tchernomazova had two possible email addresses:
- elena.tchernomazova@gmail.com
- elenatchernomazova@gmail.com

### Step 6: Verifying the Correct Email

To determine which email was correct for the flag, I tested both in the flag format. The correct email turned out to be the second one, with no period between the first and last name.

## The Flag

```
LakshyaCTF{elenatchernomazova@gmail.com}
```
