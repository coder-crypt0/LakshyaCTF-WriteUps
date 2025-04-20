# **Hidden Layers 'Macbeth' – Miscellaneous**


### Challenge Description:
An image named peacee.jpeg was provided. The title hinted at something hidden beneath the surface, possibly alluding to layered information or hidden text.

### Approach:
Given the category (Misc) and the title "Hidden Layers", the first instinct was to look for any hidden metadata or embedded text within the image. The simplest and quickest way to do that was to run the strings command on the file:

strings peacee.jpeg
### Solution:
Running the above command revealed a variety of readable strings extracted from the file. Among them was the flag:

`LakshyaCTF{Nothing_iS_F@ir}`
