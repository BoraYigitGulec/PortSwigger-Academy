# Lab: Username enumeration via different responses
# https://portswigger.net/web-security/learning-paths/server-side-vulnerabilities-apprentice/authentication-apprentice/authentication/password-based/lab-username-enumeration-via-different-responses

```bash
# Open login page and login with username: abc password: a,
# Copy candidate usernames and only mark abc,

username=§abc§&password=a

# Paste the payload and start attack.

# Check Response length to find suited username.

username: ag
```

```bash
# Now change username part to ag and only mark password.

username=ag&password=§a§

# Copy candidate password paste it to payload and start attack.

# Check response length to find suited password.(i found password with length 184 also status code 302)

password: 11111111

# Login to account to solve the lab.

```
