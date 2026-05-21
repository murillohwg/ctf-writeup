# Hidden Deep Into My Heart — Writeup

> A detailed write-up of a TryHackMe challenge, focusing on web enumeration, analysis of exposed files, and credential exploitation.
---

##  Overview

- **Platform:** TryHackMe  
- **Challenge:** Hidden Deep Into My Heart  
- **Category:** Web Security  
- **Difficulty:** Easy / Medium  
- **Objective:** Identify vulnerabilities and retrieve the flag  

---

## Methodology

A structured approach was used to solve the challenge:

1. Reconnaissance  
2. Directory and file enumeration  
3. Analysis of exposed resources  
4. Credential discovery  
5. Authentication and flag retrieval  

---

## Reconnaissance

After connecting to the TryHackMe VPN, the target machine became accessible via a private IP address (`10.67.184.5`) and a specific port.

![HOMEPAGE](./images/home-page.png) 


Initial access was performed through a web browser.

---

## Enumeration

Directory and file brute-forcing was performed using `gobuster`:

![gobuster](./images/gobuster-wordlist.png) 

```bash
gobuster dir -u http://10.67.184.5:5000/ \
-w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt \
-x txt,bak,zip 
``` 
The use of file extensions (`-x`) enabled the discovery of hidden files in addition to directories.

---

## Analysis of robots.txt

During enumeration, the following file was discovered:

![robotstxt](./images/robotstxt-dir.png) 

```bash
/robots.txt
```

Although typically used to guide search engine crawlers, this file contained sensitive information.

![psswd](./images/possivel-psswd.png) 

The content revealed a string that was later used as a valid password.

---

## Administrative Panel Discovery

Further enumeration revealed an administrative endpoint:

![loginpage](./images/login-page.png) 

```bash
/administrator
```


Accessing this endpoint presented a login interface.

---

##  Exploitation

Using previously gathered information:

![tryinglogin](./images/trying-login-page.png) 

- **Username:** `admin`  
- **Password:** extracted from `robots.txt`  

Authentication was successful, granting access to the application.

---

##  Flag Retrieval

Upon successful login, the application redirected directly to a page containing the flag.

![flag](./images/flag.png) 

>  The flag has been omitted to avoid spoilers.

