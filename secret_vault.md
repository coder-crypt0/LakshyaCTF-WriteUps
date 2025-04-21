# Secret Vault - Web Security Challenge Writeup

## Challenge Description

An internal system recently flagged unusual activity: a standard user was able to perform actions reserved for administrators. No credentials were leaked, and logs show no sign of direct tampering.

Investigate the incident and replicate the behavior to uncover the flag.

**URL**: https://ctf-question1.onrender.com

**Flag Format**: LakshyaCTF{...}

## Solution Approach

### Initial Reconnaissance

The challenge presented a web application with a login page. The first step was to understand how authentication worked in this application and identify potential vulnerabilities.

### Step 1: Testing Common Credentials

As is common in initial reconnaissance, I tried some default credentials:
```
username: admin
password: admin
```

Surprisingly, these credentials worked and the application returned an access token. This suggested the application was using some form of token-based authentication, most likely JSON Web Tokens (JWT).

### Step 2: Analyzing the JWT

After obtaining the access token, I examined its structure. JWTs typically consist of three parts:
1. Header (algorithm and token type)
2. Payload (data, including user information)
3. Signature (to verify the token hasn't been altered)

Using tools like jwt.io, I was able to decode the token and examine its contents. The token's payload included a `sub` (subject) claim set to "admin", indicating this token was for an administrator user.

### Step 3: Accessing the Admin Panel

To validate that the token was used for authorization, I sent a request to the `/admin` endpoint, including the JWT in the request header:
```
Authorization: Bearer [JWT token]
```

The server responded with:
```json
{"message":"Welcome, admin! You have access to the admin panel."}
```

This confirmed that the application was using JWTs for authorization and that the token was granting admin privileges.

### Step 4: JWT Forgery Attack

Based on the challenge description mentioning "unusual activity" where a standard user performed admin actions, I suspected a JWT signature vulnerability.

After examining the available endpoints, I noticed a `/flag` endpoint that might contain the flag. However, it likely required special privileges beyond regular admin access.

I decided to attempt a JWT forgery attack by:
1. Modifying the `sub` claim from "admin" to "flag" to represent a different type of user
2. Adding a `secret` claim with the value "supersecretkey" (a common default or hardcoded secret)
3. Recalculating the signature using the guessed secret

Using jwt.io, I created a new token with these modifications.

### Step 5: Retrieving the Flag

With the forged JWT, I sent a request to the `/flag` endpoint:
```
Authorization: Bearer [forged JWT token]
```

The server accepted the forged token and responded with:
```json
{"flag":"TGFrc2h5YUNURnt1X3BFckZvTWVEX2pXdF9mT3JHZVJ5fQ=="}
```

### Step 6: Decoding the Flag

The returned flag was Base64 encoded. After decoding it, I obtained the final flag:

```
LakshyaCTF{u_pErFoMeD_jWt_fOrGeRy}
```

## Vulnerability Explanation

This challenge demonstrated a common security issue with JWT implementations:

1. **Weak Secret Key**: The application was using a predictable secret key ("supersecretkey") to sign JWTs
2. **Improper Authorization Checks**: The application relied solely on the `sub` claim to determine user roles without additional verification
3. **Insecure JWT Handling**: The application allowed arbitrary claims to be added to the token

In a secure implementation:
- Secret keys should be long, random, and properly secured
- Multiple factors should be used for authorization decisions
- Token integrity should be carefully verified
- Claims should be validated against expected values

## Tools Used

- Browser for initial access
- Burp Suite for intercepting and modifying requests
- jwt.io for JWT analysis and modification
- Base64 decoder for the final step
