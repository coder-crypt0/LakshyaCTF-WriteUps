# Hall of Echos - Miscellaneous

**Level: Easy**

## Challenge Description:

In the hall of echoes, eight pillars stand tall, The first whispers “16” as the ancient call. Next, “98” glimmers on the second in line, Then “89” follows, a secret sign. “15” the fourth, then “35” in the lore, “75” echoes next from the old stone door. The last two, “17” and “17”, complete the thrall, Combine them to yield a product, a product of prime. This open testament, known far and wide, Guides many seekers on the cryptic ride.

High above in a celestial dance, Seven stars conceal a code at a glance. Begin with “62”, then “78” appears bright, A “04” then “06” in the shimmering night. Follow with “667”, then “94” in sight, Ending with “81” – the exponent of light. Together these values openly impart A dual key’s face that many may chart.

Yet whispers linger of an unseen art— A secret mirror that sets the truth apart. For those who dare invert what’s on display, A hidden key awaits to show the way. Unlock that private cipher, subtle yet prime, And inscribe its secret as your flag in time:

LakshyaCTF{key}

## Solution
From this we got two numbers:
- 1698891535751717 (A)
- 627804066679481 (B)

### Factorization
Since the challenge mentioned "Combine them to yield a product, a product of prime", we found 2 factors of this number from factors calculator http://www.socr.ucla.edu/Applets.dir/SOCR_PrimeNumberDecomposition.html

Those 2 numbers were:
- 23285137 (C)
- 72960341 (D)

On checking, we found that both of them were prime numbers which was what the challenge was stating.

From the statements:
> "Together these values openly impart A dual key’s face that many may chart"
> 
> "Unlock that private cipher, subtle yet prime"

We instantly got to know that this is related to cryptography.

### Identifying the algorithm used
While trying to find which encryption algorithm this might be using and trying many, we found that in RSA:

`n = p × q` (product of two primes)

`e` is the public exponent

`d` is the private exponent

We already had found the prime factors (C and D) and from the second stanza, we got the public exponent (B):

```
p = 23285137 (C)
q = 72960341 (D)
n = p × q = 1698891535751717 (A)
e = 627804066679481 (B)
```

### Calculating the Private Exponent

To find the private key d, we use the modular inverse of e with respect to φ(n), where:
```
φ(n) = (p - 1)(q - 1)
```

Script:

```python
from sympy import mod_inverse

p = 23285137
q = 72960341
e = 627804066679481
phi = (p-1) * (q-1)
d = mod_inverse(e, phi)
print(d)
```

Output:
```1216997203097801```

Since the flag format was `LakshyaCTF{key}`, substituting the key it we get `LakshyaCTF{1216997203097801}`

## The Flag
```LakshyaCTF{1216997203097801}```

