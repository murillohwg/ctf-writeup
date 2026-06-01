# Writeup — Local Authority
> Web Exploitation - client-side login bypass

## Overview

A web-based CTF challenge featuring a login page where authentication credentials were hardcoded in a publicly accessible JavaScript file, allowing full bypass of the login mechanism.

![homepage](assets/1-homepage.png)

---

## Methodology

By inspecting the source code of the login error page, a reference to an external JS file (`secure.js`) was identified. That file contained a `checkPassword()` function with hardcoded admin credentials in plaintext, which were then used to successfully authenticate and retrieve the flag.

---

## Exploitation

### Step 1 — Login Attempt (Failed)

**Method:** Submitting arbitrary credentials on the login form  
**Location:** Homepage login form  
**Finding:** Login failed — but the error page became a new attack surface.

![login-failed](assets/2-login-page-failed.png)

---

### Step 2 — Inspecting the Login Page Source Code

**Method:** Viewing the page source (`view-source:`) on the login error page  
**Location:** HTML source — login logic and linked JS files  
**Found:**

![source-login-logic](assets/3-source-code-login-page-logic.png)

**Observation:** The source code revealed the authentication logic and a reference to an external file: `secure.js`.

---

### Step 3 — Accessing `secure.js`

**Method:** Directly navigating to the linked `secure.js` file in the browser  
**Location:** JavaScript source file referenced in the HTML  
**Found:**

![secure-js](assets/4-hidden-source-code-securejs.png)

**Exposed code:**
```javascript
function checkPassword(username, password) {
  if( username === 'admin' && password === 'strongPassword098765' ) {
    return true;
  }
}
```

**Credentials leaked:** `admin` / `strongPassword098765`

---

### Step 4 — Logging In with Leaked Credentials

**Method:** Submitting the harvested credentials on the login form  
**Location:** Homepage login form  
**Found:**

![login-success](assets/5-tried-login-w-securejs-data.png)

**Result:** Authentication succeeded.

---

### Step 5 — Flag Retrieved

**Method:** Successful login granting access to the protected page  
**Location:** Post-login page  
**Found:**

![flag](assets/6-found-the-flag.png)

---

## Completed Flag

**`picoCTF{j5_15_7r4n5p4r3n7_a8788e61}`**

---

## Tools Used

- Browser DevTools (source code inspection via `view-source:`)
- Direct URL access to linked JS files

## Concepts

- **Never trust client-side authentication** — any logic running in the browser can be read by the user
- Always inspect referenced external files (`<script src="...">`) found in page source
- Hardcoded credentials in JavaScript are trivially discoverable and a critical vulnerability
- Login error pages are still attack surfaces — inspect their source too
- Client-side password checks can always be bypassed; authentication must be enforced server-side
