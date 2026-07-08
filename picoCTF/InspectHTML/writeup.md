# writeup

![Platform](https://img.shields.io/badge/platform-picoCTF-blue) ![Category](https://img.shields.io/badge/category-Web%20Exploitation-orange) ![Status](https://img.shields.io/badge/status-Solved-success)

## WriteUp - Inspect HTML

> Web exploitation - source-code

***

### Challenge Overview

When opening the challenge, the website displayed a very simple HTML page containing a short text about Histiaeus.

At first glance, nothing suspicious appeared on the page itself.

![Homepage](<../../.gitbook/assets/1-homepage (4).png>)

The challenge behavior suggested that the flag might be hidden somewhere in the webpage source.

***

### Initial Analysis

The page looked completely normal:

* Basic HTML structure
* No forms or inputs
* No JavaScript functionality
* No visible content

Since this was a beginner web challenge, the next logical step was to inspect the page source.

***

### Viewing the Source Code

Using:

```bash
CTRL + U
```

(or manually accessing `view-source:`)

I inspected the HTML source code of the page.

Near the bottom of the file, there was an HTML comment containing the flag.

![Source Code](<../../.gitbook/assets/2-source-code (1).png>)

The following comment revealed the flag:

```html
<!--picoCTF{in5p3t0r_0f_h7ml_8113f7e2}-->
```

***

### Flag

```txt
picoCTF{in5p3t0r_0f_h7ml_8113f7e2}
```

***

### Concepts

> Always inspect the source code.

Developers sometimes leave sensitive information inside:

* HTML comments
* JavaScript files
* Hidden elements
* Metadata
* Debug information

Even when nothing is visible on the webpage itself.

***
