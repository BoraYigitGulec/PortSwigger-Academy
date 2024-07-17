# Lab: User ID controlled by request parameter, with unpredictable user IDs 
# https://portswigger.net/web-security/learning-paths/server-side-vulnerabilities-apprentice/access-control-apprentice/access-control/lab-user-id-controlled-by-request-parameter-with-unpredictable-user-ids#

```bash
# Login as wiener

# Check all posts until you find carlos as writer.

# In my case it was favours post.

# After that click on his name and you will see a link like this:

https://0a9e00280444711285f209140039000d.web-security-academy.net/blogs?userId=199ce287-20b6-487f-bc78-7793f7291351
```

```bash
# Go to my account and put carlos's user id :
https://0a9e00280444711285f209140039000d.web-security-academy.net/my-account?id=199ce287-20b6-487f-bc78-7793f7291351

```
```bash
# Now we can see Carlos's API Key copy and paste it to submit solution.

```
