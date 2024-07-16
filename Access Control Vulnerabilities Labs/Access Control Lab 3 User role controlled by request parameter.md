# Lab: User role controlled by request parameter
# https://portswigger.net/web-security/learning-paths/server-side-vulnerabilities-apprentice/access-control-apprentice/access-control/lab-user-role-controlled-by-request-parameter#

```bash
# We know admin panel url so let's try to visit it:

https://0a14004904ecc36283df8c34006a002a.web-security-academy.net/admin

# Response:

 Admin interface only available if logged in as an administrator
```

```bash
# Open intercept and login to wiener peter.

# Change Admin value to:
Admin=true;

# Keep Interception on and visit:
https://0a14004904ecc36283df8c34006a002a.web-security-academy.net/admin

```

```bash
# Keep changing admin=false to admin=true in all request.
# Click to delete next to carlos and still don't close intercept.
# Keep changing admin value to true and you will complete the lab.

```
