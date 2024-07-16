
# Lab: Unprotected admin functionality
# https://portswigger.net/web-security/learning-paths/server-side-vulnerabilities-apprentice/access-control-apprentice/access-control/lab-unprotected-admin-functionality#


```bash
# Go to:
https://0a230049043ea7aa8abbe9de00bf0044.web-security-academy.net/robots.txt

# Response:

User-agent: *
Disallow: /administrator-panel

```
```bash
# Go to:
https://0a230049043ea7aa8abbe9de00bf0044.web-security-academy.net/administrator-panel

# Delete Carlos to solve the lab.

```

```bash

# robots.txt is a simple text file placed at the root of a website that tells web crawlers (robots) which pages or files the crawler can or cannot request from the site.
# It is part of the Robots Exclusion Protocol (REP), a group of web standards that regulate how robots crawl the web, access, and index content, and serve that content to users.
```
