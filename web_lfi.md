# Web Security Challenge - LFI (Local File Inclusion)

## Challenge Description

A web application exposes certain files to users, but someone was able to retrieve sensitive information that wasn't meant to be public.

Figure out how they did it and extract the flag.

**Hint**: Secret.txt is main ingredient

**URL**: https://lakshyactf-web2.onrender.com

**Flag Format**: LakshyaCTF{...}

## Solution Approach

### Initial Reconnaissance

When first accessing the website, I was presented with what appeared to be a simple file download application. The first step was to understand how this application worked and what potential vulnerabilities it might have.

I started by examining the basic functionality - the site seemed to allow users to download files by specifying their names or paths.

### Identifying the Vulnerability

After testing a few inputs, I suspected this might be vulnerable to Local File Inclusion (LFI). LFI is a vulnerability that allows attackers to include files on the server through the web application.

To confirm this theory, I attempted to access system files by using path traversal techniques. I tried to retrieve the `/etc/passwd` file, which is a common target for testing LFI vulnerabilities:

```
../../../../../etc/passwd
```

When I submitted this path to the downloader, it successfully displayed the contents of the passwd file. This confirmed that the application was vulnerable to LFI, as it was blindly accepting file paths without proper validation and accessing files outside of its intended directory.

### Finding Additional Clues

To find more information, I examined the source code of the web page. In the HTML comments, I discovered an interesting hint:

```html
<!-- hmm maybe there is a public.txt here -->
```

Following this lead, I requested the `public.txt` file and received the following message:

```
Welcome to our website!  
Enjoy your stay and download the files you need. 
Sometimes, all it takes is knowing where to look for some "secret". Maybe in /files?
```

### Retrieving the Flag

The message in `public.txt` suggested that I should look for a "secret" file in the `/files` directory. Combining this with the hint from the challenge description mentioning "Secret.txt", I attempted to access:

```
../files/secret.txt
```

Upon submitting this path to the downloader, I successfully retrieved the content of the file, which contained the flag:

```
LakshyaCTF{yOu_sOlVeD_FiLe_TrAvErSaL}
```
