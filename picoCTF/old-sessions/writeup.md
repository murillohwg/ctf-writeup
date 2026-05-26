# Old Sessions — picoCTF Writeup

## Challenge Information

- **CTF:** picoCTF
- **Challenge Name:** Old Sessions
- **Category:** Web Exploitation
- **Difficulty:** Easy/Beginner
- **Technique Used:** Session Hijacking / Broken Session Management / Vertical Privilege Escalation

---

# Description

This challenge involved abusing improperly exposed session data left accessible on the web application. By discovering an old administrator session token and replacing my own session cookie with it, I was able to escalate privileges and access the administrator account.

---

# Initial Recon

After registering a normal user account and logging in, I landed on the homepage where several comments were displayed.

While reading the comments, one of them referenced something unusual related to a `/sessions` directory.

This immediately suggested:
- exposed session files
- insecure directory exposure
- possible session leakage

---

# Discovering the Sessions Directory

I manually modified the URL in the browser from the homepage to:

```text
/sessions
```

This technique is commonly called:
- **Forced Browsing**
- **Directory Enumeration**
- **Direct URL Access**

The directory was publicly accessible and exposed active session tokens.

Inside the directory, I found what appeared to be an administrator session token still active on the server.

---

# Capturing the Admin Session

The exposed session token looked similar to:

```text
<admin-session-token>
```

At this point, the attack path became clear:

1. Copy the admin token
2. Replace my current session cookie
3. Refresh the application
4. Inherit the administrator session

---

# Session Hijacking

Using the browser DevTools:

1. Opened:
   - `F12` → Application/Storage → Cookies

2. Located my current session cookie

3. Replaced my user token with the administrator token obtained from `/sessions`

4. Refreshed the page

After refreshing, the application recognized me as the administrator user.

This resulted in a successful:
- **Vertical Privilege Escalation**
- **Session Hijacking Attack**

---

# Flag Capture

Once authenticated as admin, the flag became accessible.

```text
picoCTF{REDACTED}
```

---

# Vulnerability Analysis

The application suffered from multiple security issues.

## 1. Exposed Session Storage

Sensitive session data was directly accessible through a public directory.

This should never happen in production systems.

---

## 2. Improper Session Management

Old administrator sessions remained valid instead of expiring.

This allowed reuse of privileged tokens.

---

## 3. Missing Authorization Controls

The application trusted the session token blindly without validating:
- IP address
- device
- session age
- privilege changes

---

# Concepts Learned

This challenge demonstrates important real-world concepts:

- Session Hijacking
- Cookie Manipulation
- Broken Access Control
- Forced Browsing
- Vertical Privilege Escalation
- Insecure Session Management

---

# Mitigations

Proper mitigations would include:

- Store session files outside the web root
- Expire old sessions automatically
- Use secure session handling
- Restrict directory access
- Rotate privileged tokens
- Validate session integrity server-side

---

# Conclusion

This was a beginner-friendly but realistic web exploitation challenge demonstrating how dangerous exposed session data can be.

By performing simple reconnaissance and manipulating cookies through browser DevTools, it was possible to fully compromise the administrator account without exploiting any complex vulnerability.

The challenge reinforces how critical secure session management is in web applications.
