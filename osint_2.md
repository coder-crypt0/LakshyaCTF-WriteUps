# OSINT Challenge 2 - The Internet Coffee Machine

## Challenge Description

You are given a photo of an object. Your task is to identify where this object is currently located and on which floor.

Flag format: LakshyaCTF{place_name_floorNumber}
(All lowercase, replace spaces with underscores — e.g., LakshyaCTF{uffizi_galleries_8})

![osint_2](https://github.com/user-attachments/assets/16d7f1b7-8c6a-4f1b-b2d8-e41133420163)


## Analysis

### Initial Observation
The challenge provided an image of what appeared to be an old coffee machine. At first glance, it seemed like an ordinary appliance, but there must have been something special about it for it to be the subject of an OSINT challenge.

### Research Process
Upon examining the image more carefully and conducting some initial Google searches, I discovered that this wasn't just any coffee machine - it was the famous "Trojan Room Coffee Pot" from Cambridge University.

This coffee machine has historical significance as it was the subject of what is considered the world's first webcam. In 1991, researchers at Cambridge University Computer Laboratory set up a camera pointed at the coffee pot so that people working in various parts of the building could check if there was coffee available without making a wasted trip to the coffee room.

### Tracking Down Its Current Location
After identifying the coffee machine, the next step was to determine its current location. Through further research, I learned that after being decommissioned in 2001, the historic coffee machine was sold on eBay.

The machine was purchased by the Heinz Nixdorf MuseumsForum (HNF) in Paderborn, Germany - the world's largest computer museum. The coffee machine is now on permanent display there as an important artifact in the history of the internet.

### Finding the Floor Number
The final piece of information needed was the specific floor where the coffee machine is displayed. After searching through the museum's website and various online resources about the exhibition layout, I confirmed that the Trojan Room Coffee Pot is displayed on the 2nd floor of the Heinz Nixdorf MuseumsForum.

## The Flag

Combining all this information and formatting it according to the challenge requirements:
- Place: heinz_nixdorf_museumsforum
- Floor: 2

Therefore, the flag is:
```
LakshyaCTF{heinz_nixdorf_museumsforum_2}
```

## Learning Outcomes

This challenge demonstrates key aspects of OSINT (Open Source Intelligence) investigation:

1. **Object Identification**: Recognizing historical technology items based on visual cues
2. **Historical Research**: Understanding the significance and provenance of artifacts
3. **Location Tracking**: Following the trail of an item from its origin to its current location
4. **Detail Verification**: Finding specific information like floor numbers through multiple sources

The challenge also highlights how seemingly ordinary objects can have extraordinary stories behind them, and how these stories are preserved in museums as part of our technological heritage.
