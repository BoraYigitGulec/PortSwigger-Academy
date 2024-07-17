# Lab: User ID controlled by request parameter with password disclosure
# https://portswigger.net/web-security/learning-paths/server-side-vulnerabilities-apprentice/access-control-apprentice/access-control/lab-user-id-controlled-by-request-parameter-with-password-disclosure
```bash
# Login as wiener

# Go to my account page

https://0a5a00520306218b8015df1d00300079.web-security-academy.net/my-account?id=wiener

# Change url to:

https://0a5a00520306218b8015df1d00300079.web-security-academy.net/my-account?id=administrator
```
```bash
# Check /my-account?id=administrator from http history.

# We found password:

teyv39ochha08gkg94xn
```
```bash
# Login as administrator

# Go to admin panel and delete carlos to solve the lab.
```
