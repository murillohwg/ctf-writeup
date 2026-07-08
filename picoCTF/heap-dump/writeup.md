

![Status](https://img.shields.io/badge/Status-Solved-success) ![Category](https://img.shields.io/badge/Category-Web%20Exploitation-blue) ![Topic](https://img.shields.io/badge/Topic-API%20Misconfiguration-red)

## WriteUp - heap dump

> Web Explotation - API misconfiguration

### Challenge Description

This challenge explore a web application and find an endpoint that exposes a file containing a hidden flag.

Hints:

* Explore backend development with us
* The head was dumped

### Enumeration

#### Homepage Analysis

The challenge presents a simple news website called **picoCTF News**.

![Homepage](assets/1-homepage.png)

While browsing the website, one article references API documentation, suggesting that additional functionality may be available through backend endpoints.

#### Source Code Review

Inspecting the page source revealed references to API-related resources and documentation.

![Source Code](assets/2-source-code.png)

This indicated that the application exposes a backend API that could be explored further.

#### API Documentation Discovery

Navigating to the API documentation endpoint exposed a Swagger interface.

![API Documentation](assets/3-api-docs-module.png)

The Swagger page listed several available endpoints, including routes for managing blog posts and diagnostic functionality.

#### Endpoint Enumeration

Reviewing the available API routes revealed the following modules:

* `/api/posts`
* `/api/posts/{id}`
* `/heapdump`

![API Endpoints](assets/4-api-posts-module.png)

The endpoint `/heapdump` immediately stood out because of the challenge hint:

> The head was dumped.

This strongly suggested that a memory dump might be exposed.

### Exploitation

#### Accessing the Heap Dump

The `/heapdump` endpoint was accessed directly.

The server responded by generating a downloadable file named:

```
heapdump.heapsnapshot
```

![Heapdump Download](assets/5-heapdump-download.png)

Heap snapshots are commonly used in Node.js applications for debugging memory issues. However, exposing them publicly can leak sensitive information stored in memory.

#### Inspecting the Dump

After downloading the heap snapshot, the file was inspected locally.

Using simple string searches against the dump revealed sensitive application data stored in memory.

Example:

```bash
grep -a "picoCTF{" heapdump
```

This quickly located the flag embedded within the heap snapshot contents.

### Flag Retrieval

Searching through the heap dump revealed the flag.

![Flag Found](assets/6-found-flag.png)

### Root Cause

The application exposed a diagnostic endpoint that generated a heap snapshot of the running Node.js process.

Heap dumps frequently contain:

* API keys
* Session tokens
* User information
* Secrets
* Application state
* Flags (in CTF environments)

Because the endpoint was publicly accessible, an attacker could download the server's memory contents and extract sensitive information without authentication.

### Concepts

* Debugging endpoints should never be exposed to untrusted users.
* Heap snapshots may contain highly sensitive information.
* Swagger documentation can reveal hidden functionality and administrative routes.
* Publicly accessible diagnostic endpoints can lead to severe information disclosure vulnerabilities.
