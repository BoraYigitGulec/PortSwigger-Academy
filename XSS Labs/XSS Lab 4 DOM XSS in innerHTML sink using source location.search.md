# Lab: DOM XSS in innerHTML sink using source location.search
# https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-innerhtml-sink
```bash
# Search
abc1234

# We are getting this results by inspecting abc1234 search result.

<span id="searchMessage">abc1234</span>

<script>function doSearchQuery(query) { document.getElementById('searchMessage').innerHTML = query; }
var query = (new URLSearchParams(window.location.search)).get('search'); if(query) {doSearchQuery(query); }</script>
```

```bash
# Let's start checking this part of the script.
var query = (new URLSearchParams(window.location.search)).get('search');

# window.location.search: Gets the query string part of the current URL (everything after the ?).
# new URLSearchParams(window.location.search): Creates a new URLSearchParams object from the query string.
# .get('search'): Retrieves the value of the search parameter from the query string.
# So in our search  query will have the value of abc1234.

```
```bash

function doSearchQuery(query) { document.getElementById('searchMessage').innerHTML = query; }

# It selects the HTML element with the id searchMessage using document.getElementById('searchMessage')
# and It sets the innerHTML (the content) of this element to the value of the query parameter.
```
```bash
if(query) {doSearchQuery(query);

# If query exist calls the doSearchQuery function.
# In our example first  we set query as abc1234.
# After that if statement calls do searchQuery and sets searchMessage's innerHTML to abc1234

```bash
# Search

<img src=9999  onerror=alert()>
# 9999 is not a valid URL for an image, so it will cause an error.(value can be 0 ,1 ...)

```

